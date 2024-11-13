---
date: '2024-10-16T20:00:00+08:00'
title: 'Dynamics CRM – 在Plugin中使用ILMerge打包多个程序集'
description: ''
slug: 'dynamics-crm-plugins-using-ilmerge'
image: 'post/images/dynamics-crm-logo.png'
categories:
    - Dynamics-CRM
tags:
    - CRM
draft: false
keywords:
    - dynamics
    - crm
    - dynamics-crm-plugin
    - crm-plugins
    - crm-tool
toc: true
---

## 简述

实施项目的时候，难免在插件中会引用到外部的 dll，比如

- 处理文档的MiniExcel

- 用于序列化和反序列化的 Netonsoft.Json

- 等等...

如果我们不将引用的外部 dll 和编译生成的 plugin.dll 文件打包，

直接将编译生成 plugin.dll 部署到环境中的话，插件运行时会报错：xxxxxx 未定义、找不到。

为了解决这个问题，可以使用 ILMerge 来进行打包。

> 另外，现在 MS 还出了另外一种方法，做法是将外部引用上传到 Dataverse 服务器，
>
>其中文件包含了实现 IPlugin 接口类的所有程序集都关联上，以后只需更新 PluginPackage 就可以，
>
>当插件执行时，Dataverse 就会从 PluginPackage 中拿到 dll 执行，这样插件所需的 dll 都能用得上。

![SnipastePro_2024_11_13_13_40_55.png](post/images/SnipastePro_2024_11_13_13_40_55.png)

## ILMerge使用示例

假设: 在插件中我将引用MiniExcel.

### 安装ILMerge

选中插件项目，使用 Nuget 安装 ILMerge

![SnipastePro_2024_11_13_13_43_46.png](post/images/SnipastePro_2024_11_13_13_43_46.png)

ILMerge 安装完成后，解决方案的 package 文件夹中会新增两个文件夹

![SnipastePro_2024_11_13_13_44_24.png](post/images/SnipastePro_2024_11_13_13_44_24.png)

### 设置引用属性

把除了第三方引用的 dll 之外的 dll “复制到本地” 属性设置为 false。

比如我引用的是 Mini Excel，那么我将 Mini Excel 的 “复制到本地” 设置为 true，其余的都设置为 false

![SnipastePro_2024_11_13_13_45_41.png](post/images/SnipastePro_2024_11_13_13_45_41.png)

### 编译

编译 Plugin 项目，编译完成后 bin 文件夹中能看到，只有一个 dll，

将这个 plugin.dll 通过PluginRegistration发布到目标环境中就可以了。

![SnipastePro_2024_11_13_13_47_18.png](post/images/SnipastePro_2024_11_13_13_47_18.png)

## 遇到的问题

通过PluginRegistration注册插件时，提示：

“PluginType not found in PluginAssembly which has a total of [0] plugin/workflow activity types.”

这是没有将 Microsoft.Crm.Sdk 和 Microsoft.Crm.Sdk.Proxy “复制到本地” 属性设置为false导致
