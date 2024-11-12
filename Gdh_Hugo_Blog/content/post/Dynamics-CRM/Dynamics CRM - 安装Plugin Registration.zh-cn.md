---
date: '2024-10-16T22:55:51+08:00'
title: 'Dynamics CRM - 安装 Plugin Registration 工具'
description: 'dynamics-crm 安装插件注册工具'
slug: 'dynamics-crm-install-plugin-registration'
image: 'post/images/dynamics-crm-logo.png'
categories:
    - Dynamics-CRM
tags:
    - CRM
draft: false
keywords:
    - dynamics
    - crm
    - dynamics-crm-install-plugin-registration
    - crm-plugins
    - crm-tool
toc: true
---

## 前言

Plugin Registration ，用于注册和管理插件，不想单独安装 Plugin Registration 的话，可以直接在 XrmToolBox 安装使用。

## 安装方式 1

### 访问Nuget

[NuGet Gallery | Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool 9.1.0.199](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool/)

### Download package

![SnipastePro_2024_11_12_22_09_23.png](post/images/SnipastePro_2024_11_12_22_09_23.png)

### 修改压缩包后缀名

将下载的文件后缀名更改为`.zip`，然后解压缩，Plugin Registration 就在tool文件夹里

![SnipastePro_2024_11_12_22_10_21.png](post/images/SnipastePro_2024_11_12_22_10_21.png)

## 安装方式 2

### 创建文件夹

例：D:\Dynamics_365_Development_Tools\pluginsTool

### Powershell

PowerShell 进入 D:\Dynamics_365_Development_Tools\pluginsTool

![SnipastePro_2024_11_12_22_13_06.png](post/images/SnipastePro_2024_11_12_22_13_06.png)

### 运行代码

先运行代码：

```Powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$sourceNugetExe = "https://dist.nuget.org/win-x86-commandline/latest/nuget.exe"
$targetNugetExe = ".\nuget.exe"
Remove-Item .\Tools -Force -Recurse -ErrorAction Ignore
Invoke-WebRequest $sourceNugetExe -OutFile $targetNugetExe
Set-Alias nuget $targetNugetExe -Scope Global -Verbose
```

再运行代码：

```Powershell
##
##Download Plugin Registration Tool
##
./nuget install Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool -O .\Tools
md .\Tools\PluginRegistration
$prtFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool.'}
move .\Tools\$prtFolder\tools\*.* .\Tools\PluginRegistration
Remove-Item .\Tools\$prtFolder -Force -Recurse
```

### 安装完成

![SnipastePro_2024_11_12_22_15_44.png](post/images/SnipastePro_2024_11_12_22_15_44.png)

### PowerShell 代码

```Powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$sourceNugetExe = "https://dist.nuget.org/win-x86-commandline/latest/nuget.exe"
$targetNugetExe = ".\nuget.exe"
Remove-Item .\Tools -Force -Recurse -ErrorAction Ignore
Invoke-WebRequest $sourceNugetExe -OutFile $targetNugetExe
Set-Alias nuget $targetNugetExe -Scope Global -Verbose 
##
##Download Plugin Registration Tool
##
./nuget install Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool -O .\Tools
md .\Tools\PluginRegistration
$prtFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool.'}
move .\Tools\$prtFolder\tools\*.* .\Tools\PluginRegistration
Remove-Item .\Tools\$prtFolder -Force -Recurse 
##
##Download CoreTools
##
./nuget install  Microsoft.CrmSdk.CoreTools -O .\Tools
md .\Tools\CoreTools
$coreToolsFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.CoreTools.'}
move .\Tools\$coreToolsFolder\content\bin\coretools\*.* .\Tools\CoreTools
Remove-Item .\Tools\$coreToolsFolder -Force -Recurse 
##
##Download Configuration Migration
##
./nuget install  Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf -O .\Tools
md .\Tools\ConfigurationMigration
$configMigFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf.'}
move .\Tools\$configMigFolder\tools\*.* .\Tools\ConfigurationMigration
Remove-Item .\Tools\$configMigFolder -Force -Recurse 
##
##Download Package Deployer 
##
./nuget install  Microsoft.CrmSdk.XrmTooling.PackageDeployment.WPF -O .\Tools
md .\Tools\PackageDeployment
$pdFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PackageDeployment.Wpf.'}
move .\Tools\$pdFolder\tools\*.* .\Tools\PackageDeployment
Remove-Item .\Tools\$pdFolder -Force -Recurse 
##
##Remove NuGet.exe
##
Remove-Item nuget.exe
```
