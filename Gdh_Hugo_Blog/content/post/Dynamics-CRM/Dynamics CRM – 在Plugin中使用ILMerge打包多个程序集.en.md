---
date: '2024-10-16T20:00:00+08:00'
title: 'Dynamics CRM – Use ILMerge to package multiple assemblies in a Plugin'
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

## Brief Description

During project implementation, it is common to reference external DLLs in plugins, such as

- `MiniExcel` for document processing

- `Newtonsoft.Json` for serialization and deserialization

- And so on...

If we do not package the referenced external DLLs with the compiled plugin.dll file,

and simply deploy the compiled plugin.dll to the environment,

the plugin will throw errors at runtime: "xxxxxx is undefined" or "cannot be found".

To solve this problem, we can use ILMerge to package the assemblies.

> Additionally, Microsoft has introduced another method, which involves uploading external references to the Dataverse server.
>
> All assemblies containing the classes that implement the IPlugin interface are associated, and in the future, you only need to update the PluginPackage.
>
>When the plugin executes, Dataverse will retrieve the DLLs from the PluginPackage, ensuring that all required DLLs are available for the plugin.

![SnipastePro_2024_11_13_13_40_55.png](post/images/SnipastePro_2024_11_13_13_40_55.png)

## ILMerge Usage Example

Assuming: I will reference MiniExcel in the plugin.

### Install ILMerge

Select the plugin project and use NuGet to install ILMerge.

![SnipastePro_2024_11_13_13_43_46.png](post/images/SnipastePro_2024_11_13_13_43_46.png)

After ILMerge is installed, two new folders will be added to the package folder in the solution.

![SnipastePro_2024_11_13_13_44_24.png](post/images/SnipastePro_2024_11_13_13_44_24.png)

### Set Reference Properties

Set the "Copy to Local" property of all DLLs, except for third-party references, to false.

For example, if I reference MiniExcel, I will set "Copy to Local" for MiniExcel to true, while setting it to false for all others.

![SnipastePro_2024_11_13_13_45_41.png](post/images/SnipastePro_2024_11_13_13_45_41.png)

### Compile

Compile the Plugin project. After the compilation is complete, you will see only one DLL in the bin folder.

You can then publish this `plugin.dll` to the target environment using Plugin Registration.

![SnipastePro_2024_11_13_13_47_18.png](post/images/SnipastePro_2024_11_13_13_47_18.png)

## Encountered Issues

When registering the plugin through Plugin Registration, the following message appears:

“PluginType not found in PluginAssembly which has a total of [0] plugin/workflow activity types.”

This is caused by not setting the "Copy to Local" property for Microsoft.Crm.Sdk and Microsoft.Crm.Sdk.Proxy to false.
