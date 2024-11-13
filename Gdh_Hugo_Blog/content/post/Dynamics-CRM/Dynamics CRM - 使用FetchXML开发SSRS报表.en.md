---
date: '2024-10-17T20:00:00+08:00'
title: 'Dynamics CRM - Developing SSRS Rreports Using Fetch'
description: ''
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

## Brief Description

This article explains how to develop custom reports in Dynamics CRM using FetchXML, including:

- Preparing the environment

- Practical example

## Preparing the Environment

P.S. Please follow the steps for the software listed below in order;

otherwise, unexpected issues may arise.

1. Visual studio 2019

2. SQL Server Data Tools

3. Microsoft Reporting Services Projects

4. Restart the computer

5. Install Dynamics 365 Report Authoring Extension

Here is the download link:

- [Microsoft Reporting Services Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)
- [Dynamics 365 Report Authoring Extension](https://www.microsoft.com/en-US/download/details.aspx?id=56973)

> Date: 2024-01-22
>
> I attempted to use Visual Studio 2022 for report development, but I encountered a component exception that I couldn't resolve.Therefore, I still recommend continuing to use Visual Studio 2019

## Development Example

### Example 1: User's Last Login Time

#### Create a Project

First, open Visual Studio 2019 and create a report project:

- Create a new project

- Search for "Report" and select "Report Server Project," then click "Next"

![SnipastePro_2024_11_13_10_17_37.png](post/images/SnipastePro_2024_11_13_10_17_37.png)

- Fill in the "Project Name" and click "Create"

At this point, we have completed the creation of the report project, and the structure is as follows:

![SnipastePro_2024_11_13_10_19_37.png](post/images/SnipastePro_2024_11_13_10_19_37.png)

#### Create a Report

- Select the "Reports" folder and right-click on it.

- Choose "Add" , then select "New Item".

- Select "Report" , enter the report name, and click "Add".

![SnipastePro_2024_11_13_10_23_55.png](post/images/SnipastePro_2024_11_13_10_23_55.png)

At this point, the report has been added, and the interface is as follows:

![SnipastePro_2024_11_13_10_25_16.png](post/images/SnipastePro_2024_11_13_10_25_16.png)

#### Add Data Source

- Select the "Data Sources" folder and right-click on it, then choose "Add Data Source".

![SnipastePro_2024_11_13_10_28_02.png](post/images/SnipastePro_2024_11_13_10_28_02.png)

> If the "Report Data" tab has been accidentally closed, you can reopen it using the shortcut `Ctrl + Alt + D`.

- Fill in the "Name for Data Source".

> You can name the data source according to your personal preference; I usually name it "DynamicsCRMDataSource".
>
> This name is not critical; you can use the default name as well, and it can be changed later.

- For **Type**, select `Microsoft Dynamics 365 Fetch`

- Enter the "Connection String" and click "OK."

> To learn how to obtain the connection string,
>
> please refer to the "Getting the Connection String" section of this article.

![SnipastePro_2024_11_13_10_52_59.png](post/images/SnipastePro_2024_11_13_10_52_59.png)

#### Prepare Fetch

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

#### Add Data Set

1. Fill in the "Data Set Name", select "Use a dataset embedded in my report", and choose the DynamicsCRMDataSource data source we just added.

2. For Query Type, select "Text", fill in the Fetch, and finally click "OK".

> Note: If a login prompt appears after clicking "OK," log in with your development account.

![SnipastePro_2024_11_13_10_53_39.png](post/images/SnipastePro_2024_11_13_10_53_39.png)

![SnipastePro_2024_11_13_10_56_53.png](post/images/SnipastePro_2024_11_13_10_56_53.png)

#### Report Design

- Report Title

Select the "Text Box" from the toolbox, drag it to the report design area, and then fill in the title.

![SnipastePro_2024_11_13_11_00_52.png](post/images/SnipastePro_2024_11_13_11_00_52.png)

Select the "Table" from the toolbox, drag it to the report design area, and enter the column headers.

P.S. The styles can be adjusted according to your needs.

![SnipastePro_2024_11_13_11_01_16.png](post/images/SnipastePro_2024_11_13_11_01_16.png)

#### Data Binding

Using the "User Name" column as an example: right-click the empty space below the user name and select "Expression".

![SnipastePro_2024_11_13_11_01_57.png](post/images/SnipastePro_2024_11_13_11_01_57.png)

Select "Fields," then double-click "FullName." The expression will automatically update after double-clicking.

Of course, you can also manually enter the expression. Finally, click "OK".

![SnipastePro_2024_11_13_11_02_37.png](post/images/SnipastePro_2024_11_13_11_02_37.png)

Then bind data for the other columns in sequence.

![SnipastePro_2024_11_13_11_04_20.png](post/images/SnipastePro_2024_11_13_11_04_20.png)

#### Test (Preview) the report

![SnipastePro_2024_11_13_11_05_00.png](post/images/SnipastePro_2024_11_13_11_05_00.png)

Effect:

![SnipastePro_2024_11_13_11_05_16.png](post/images/SnipastePro_2024_11_13_11_05_16.png)

#### Publish report

Enter Power Apps and create a new solution (you can also use an existing one, as long as it is unmanaged).

Click "New", then select "Report".

![SnipastePro_2024_11_13_11_07_00.png](post/images/SnipastePro_2024_11_13_11_07_00.png)

For the report type, choose "Existing File", and then select the completed report: `UserLastLoginTime.rdl`.

Fill in the "Report Name", and finally click "Save".

![SnipastePro_2024_11_13_11_07_58.png](post/images/SnipastePro_2024_11_13_11_07_58.png)

At this point, the example is complete. You can open and preview it from the Reports section in the menu bar.

![SnipastePro_2024_11_13_11_21_42.png](post/images/SnipastePro_2024_11_13_11_21_42.png)

> In Dynamics CRM, reports that typically require custom development can generally be categorized into two types:
>
> - "Global Reports": The report created in this example falls into this category. These reports are usually executed from the report entity or the button bar of a specific business entity's view.
>
> - "Single Record Reports": These reports are typically placed on the business record forms, with parameters mainly taking the GUID of a specific business record.

## Get the Connection String

The format of the connection string is: 

`{Environment URL}`/`{Environment Unique Name}`

For example

- Environment URL：`https://sample.crm.dynamics.cn`

- Environment Unique Name：`123456789`

- Connection String：`https://sample.crm.dynamics.cn/123456789`

> **How to obtain the Environment Unique Name?**
>
> UCI Interface
>
> - Open Power Apps `https://make.powerapps.com/`
>
> - Click the settings button in the upper right corner and select "Developer Resources"
>
> Classic UI
>
> - Settings --> Customizations
>
> - Select "Developer Resources"
