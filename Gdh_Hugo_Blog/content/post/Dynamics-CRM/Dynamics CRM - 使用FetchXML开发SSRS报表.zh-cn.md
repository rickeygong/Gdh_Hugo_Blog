---
date: '2024-10-17T20:00:00+08:00'
title: 'Dynamics CRM - 使用Fetch开发SSRS报表'
description: '使用FetchXML开发SSRS报表：1.环境准备；2.开发实例'
slug: 'dynamics-crm-developing-ssrs-reports-using-fetch'
image: 'post/images/dynamics-crm-logo.png'
categories:
    - Dynamics-CRM
tags:
    - CRM
    - SSRS
draft: false
keywords:
    - dynamics
    - crm
    - dynamics-crm-developing-ssrs-reports-using-fetch
    - crm-reports
    - ssrs
toc: true
---

## 简述

本文介绍如何在Dynamics CRM使用FetchXML进行自定义的报表开发，包括：

- 准备环境

- 实例演练

## 准备环境

P.S 下列的软件，请按照顺序进行操作，否则会出现意想不到的问题

1. Visual studio 2019

2. SQL Server Data Tools

3. Microsoft Reporting Services Projects

4. 重启电脑

5. 安装Dynamics 365 Report Authoring Extension

下面是下载地址：

- [Microsoft Reporting Services Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)
- [Dynamics 365 Report Authoring Extension](https://www.microsoft.com/en-US/download/details.aspx?id=56973)

> 2024-01-22
> 我曾尝试使用Visual studio 2022进行报表开发，但提示组件异常，未能解决。
>
> 所以还是建议继续使用Visual studio 2019。

## 开发实例

### 实例1 ：用户最后一次登录时间

#### 创建项目

首先，我们先打开Visual studio 2019，创建报表项目

- 新建项目

- 搜索"报表"，选择 "报表服务器项目"，点击 "下一步"

![SnipastePro_2024_11_13_10_17_37.png](post/images/SnipastePro_2024_11_13_10_17_37.png)

- 填写 "项目名称" ，点击 "创建"

至此，我们已经完成了报表项目的创建，结构如下：

![SnipastePro_2024_11_13_10_19_37.png](post/images/SnipastePro_2024_11_13_10_19_37.png)

#### 创建报表

- 选中 "报表" 文件夹 ， 右击它

- 选中 "添加" ， 再选择 "新建项"

- 选择报表 ，输入报表名称，点击添加

![SnipastePro_2024_11_13_10_23_55.png](post/images/SnipastePro_2024_11_13_10_23_55.png)

至此，报表添加完成，界面如下：

![SnipastePro_2024_11_13_10_25_16.png](post/images/SnipastePro_2024_11_13_10_25_16.png)

#### 添加数据源

- 选中 "数据源" 文件夹 ， 右击它 ， 选中 "添加数据源"

![SnipastePro_2024_11_13_10_28_02.png](post/images/SnipastePro_2024_11_13_10_28_02.png)

> 如果“报表数据”选项卡被你不小心关掉了，可以通过快捷键 `Ctrl + Alt + D` 打开

- 填写 "添加数据源名称"

> 关于数据源名称，可以根据个人习惯进行命名；我习惯写 "DynamicsCRMDataSouce"
>
> 这个名称无所谓，你用默认的也可以，后面都可以修改的

- 类型 选择 `Microsoft Dynamics 365 Fetch`

- 输入 "连接字符串" ，点击 "确定"

> 连接字符串怎么获取，请参考本文 获取连接字符串 部分

![SnipastePro_2024_11_13_10_52_59.png](post/images/SnipastePro_2024_11_13_10_52_59.png)

#### 准备FetchXML

```xml
<fetch aggregate="true">
  <entity name="audit">
    <attribute name="createdon" alias="LastLoginDate" aggregate="max" />
    <filter>
      <condition attribute="operation" operator="eq" value="4" />
    </filter>
    <link-entity name="systemuser" from="systemuserid" to="objectid" link-type="inner" alias="SystemUser">
      <attribute name="fullname" alias="FullName" groupby="true" />
      <attribute name="domainname" alias="DomainName" groupby="true" />
      <attribute name="isdisabled" alias="IsDisabled" groupby="true" />
      <attribute name="accessmode" alias="AccessMode" groupby="true" />
      <attribute name="userlicensetype" alias="UserLicenseType" groupby="true" />
    </link-entity>
  </entity>
</fetch>
```

#### 添加数据集

1. 填写 "数据集名称"，选择 "使用在我的报表中嵌入的数据集" ，选择刚刚我们添加的DynamicsCRMDataSouce数据源

2. 查询类型选择“文本”，填写Fetch，最后点击“确定”

 注：点击“确定”后如果弹出登录框，登录自己的开发账号即可

![SnipastePro_2024_11_13_10_53_39.png](post/images/SnipastePro_2024_11_13_10_53_39.png)

![SnipastePro_2024_11_13_10_56_53.png](post/images/SnipastePro_2024_11_13_10_56_53.png)

#### 报表设计

- 标题

选择工具箱中的“文本框”，拖到报表设计界面，然后填写标题

![SnipastePro_2024_11_13_11_00_52.png](post/images/SnipastePro_2024_11_13_11_00_52.png)

选择工具箱中的“表”，拖到报表设计界面，在输入列标题，样式可以根据自己需求进行调整

![SnipastePro_2024_11_13_11_01_16.png](post/images/SnipastePro_2024_11_13_11_01_16.png)

#### 数据绑定

用“用户名称”列举例：右击用户名下边的空格，选择“表达式”

![SnipastePro_2024_11_13_11_01_57.png](post/images/SnipastePro_2024_11_13_11_01_57.png)

选择“字段”，然后双击“FullName”，双击后表达式会自动更新。

当然，表达式你也可以自己手写进去，最后点击 "确定"

![SnipastePro_2024_11_13_11_02_37.png](post/images/SnipastePro_2024_11_13_11_02_37.png)

然后依次为其他列绑定数据

![SnipastePro_2024_11_13_11_04_20.png](post/images/SnipastePro_2024_11_13_11_04_20.png)

#### 测试(预览)报表

![SnipastePro_2024_11_13_11_05_00.png](post/images/SnipastePro_2024_11_13_11_05_00.png)

效果：

![SnipastePro_2024_11_13_11_05_16.png](post/images/SnipastePro_2024_11_13_11_05_16.png)

#### 发布报表

进入Power Apps ，新建解决方案（使用现有的也可以，注意是非托管的就行）。

点击 "新建" ，选择 "报表"

![SnipastePro_2024_11_13_11_07_00.png](post/images/SnipastePro_2024_11_13_11_07_00.png)

报表类型选择 “现有文件” ，然后选择开发完成的报表：`用户最后一次登录时间.rdl`，

填写 “报表名称” ，最后点击“保存”

![SnipastePro_2024_11_13_11_07_58.png](post/images/SnipastePro_2024_11_13_11_07_58.png)

至此，实例已经完成。你可以到菜单栏的报表中打开并预览它。

![SnipastePro_2024_11_13_11_21_42.png](post/images/SnipastePro_2024_11_13_11_21_42.png)

> 在Dynamics CRM中，一般需要自定义开发的报表，我一般归为两类：
>
> - "全局类报表" : 本次实例做的就是这类报表，这类报表的执行位置通常放在报表实体、某业务实体的视图按钮栏上
>
> - "单记录类报表" : 这类报表通常放在业务记录的表单上，参数主要取某条业务记录的Guid

## 获取连接字符串

连接字符串的格式 ： {环境URL}/{环境唯一名称}

例如：

- 环境URL：`https://sample.crm.dynamics.cn`

- 环境唯一名称：`123456789`

- 连接字符串：`https://sample.crm.dynamics.cn/123456789`

> **如何获取环境唯一名称？**
>
> UCI界面
>
> - 打开Power Apps `https://make.powerapps.com/`
>
> - 点击右上角的设置按钮，选择 "开发人员资源"
>
> 经典UI
>
> - 设置 --> 自定义项
>
> - 选择 "开发人员资源"
