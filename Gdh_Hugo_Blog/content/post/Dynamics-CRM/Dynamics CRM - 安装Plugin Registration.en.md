---
date: '2024-10-16T22:55:51+08:00'
title: 'Dynamics CRM - Install Plugin Registration Tool'
description: 'dynamics-crm-install-plugin-registration'
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

## Introduction

Plugin Registration is used to register and manage plugins.

If you don't want to install Plugin Registration separately, you can directly install and use it in XrmToolBox.

## Installation Method 1

### Access NuGet

[NuGet Gallery | Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool 9.1.0.199](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool/)

### Download package

![SnipastePro_2024_11_12_22_09_23.png](post/images/SnipastePro_2024_11_12_22_09_23.png)

### Change the file extension of the downloaded archive

Rename the downloaded file to have a `.zip` extension, then extract it.

The Plugin Registration will be in the tool folder.

![SnipastePro_2024_11_12_22_10_21.png](post/images/SnipastePro_2024_11_12_22_10_21.png)

## Installation Method 2

### Create a Folder

For example：D:\Dynamics_365_Development_Tools\pluginsTool

### Powershell

Enter PowerShell. D:\Dynamics_365_Development_Tools\pluginsTool

![SnipastePro_2024_11_12_22_13_06.png](post/images/SnipastePro_2024_11_12_22_13_06.png)

### Run the code

Run the code first:

```Powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$sourceNugetExe = "https://dist.nuget.org/win-x86-commandline/latest/nuget.exe"
$targetNugetExe = ".\nuget.exe"
Remove-Item .\Tools -Force -Recurse -ErrorAction Ignore
Invoke-WebRequest $sourceNugetExe -OutFile $targetNugetExe
Set-Alias nuget $targetNugetExe -Scope Global -Verbose
```

Run the code again:

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

### Installation completed

![SnipastePro_2024_11_12_22_15_44.png](post/images/SnipastePro_2024_11_12_22_15_44.png)

### PowerShell Code

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
