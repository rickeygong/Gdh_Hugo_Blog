---
date: '2024-11-14T20:00:00+08:00'
title: 'Dynamics CRM - 选项添加颜色'
description: '选项添加颜色'
slug: '/2024-11/dynamics-crm-optionset-add-colors'
image: 'post/images/dynamics-crm-logo.png'
categories:
    - Dynamics-CRM
tags:
    - CRM
draft: false
keywords:
    - dynamics
    - crm
    - dynamics-crm-optionset-add-colors
    - option-set
toc: true
---

## 效果

- 视图
![选项添加颜色视图效果](post/images/SnipastePro_2024_11_15_12_59_25.png)

- 表单
![选项添加颜色表单效果](post/images/SnipastePro_2024_11_15_13_02_05.png)

- 子网格
![选项添加颜色子网格效果](post/images/SnipastePro_2024_11_15_13_01_31.png)

- 快速创建表单
![选项添加颜色快速创建表单效果](post/images/SnipastePro_2024_11_15_13_03_44.png)

## 步骤

**无论是全局添加还是“局部”添加，都需要先设置选项颜色。**

![设置选项颜色](post/images/SnipastePro_2024_11_15_12_28_49.png)

> 我常用的颜色：
>
> - 蓝 `#70b6ff`
> - 绿 `#67c23a`
> - 红 `#f8a2a2`
> - 灰 `#909399`
> - 橙 `#e7a544`

### 全局添加

全局添加的意思是只需要在一个地方设置，那么选项的颜色就会在视图、表单、子网格上显示。

#### 打开解决方案

> 使用经典UI界面打开，新版UCI界面我没有找到在哪个位置进行设置。
>
> 如果您知道，欢迎在下方评论留言，互相学习。

#### 添加组件

选择实体， 添加控件。

![添加控件1](post/images/SnipastePro_2024_11_15_12_35_30.png)

选择 **Power Apps 网格控件**
![添加控件2](post/images/SnipastePro_2024_11_15_12_36_42.png)

将 **启用选项集颜色** 设置为 “是” ，然后设置**Power Apps 网格控件**在Web端等启用。
![添加控件3](post/images/SnipastePro_2024_11_15_12_38_09.png)

然后保存并发布即可。

### “局部添加”

局部添加的意思是你只想在某个位置为选项添加颜色：

- 子网格

- 快速创建表单

- 常规表单

- 等等...

其步骤都是一样的，下面我以在快速创建表单添加为例：

1. 打开快速创建表单

2. 选中选项字段，点击“更改属性”

3. 在字段属性选项卡上选择“控件”Tab

4. 添加**OptionSet Wrapper**控件，然后设置**OptionSet Wrapper**控件在Web端等启用。

5. 保存并发布即可。

![局部添加控件](post/images/SnipastePro_2024_11_15_12_51_49.png)
