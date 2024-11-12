---
date: '2024-10-15T14:55:51+08:00'
title: 'Dynamics CRM - 获取用户最后一次登录时间'
description: ''
slug: 'dynamics-crm-get-user-last-login-time'
image: 'post/images/dynamics-crm-logo.png'
categories:
    - Dynamics-CRM
tags:
    - CRM
draft: false
keywords:
    - dynamics
    - crm
    - get-user-last-login-time
    - fetch
    - ssrs
    - crm-report
---

我目前主要使用的有如下3种方法：

- 通过Power Platform管理中心获取

- 通过FetchXML查询

- SQL

## 通过Power Platform管理中心获取

通过Power Platform管理中心的 “分析”

![SnipastePro_2024_11_12_21_32_17.png](post/images/SnipastePro_2024_11_12_21_32_17.png)

## 过FetchXML查询

FetchXML如下：

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

示：

![SnipastePro_2024_11_12_21_35_07.png](post/images/SnipastePro_2024_11_12_21_35_07.png)

## SQL

在XrmToolBox里使用“SQL 4 CDS”进行查询，SQL如下

```sql
SELECT   MAX(audit.createdon) AS LastLoginDate,
         SystemUser.fullname AS FullName,
         SystemUser.domainname AS DomainName,
         SystemUser.isdisabled AS IsDisabled,
         SystemUser.accessmode AS AccessMode,
         SystemUser.userlicensetype AS UserLicenseType
FROM     audit
         INNER JOIN
         systemuser AS SystemUser
         ON audit.objectid = SystemUser.systemuserid
WHERE    audit.operation = 4
GROUP BY 
SystemUser.fullname, 
SystemUser.domainname, 
SystemUser.isdisabled, 
SystemUser.accessmode, 
SystemUser.userlicensetype;
```

## 备注

### 审核

如果使用方式2或方式3，需开启“审核功能”

![SnipastePro_2024_11_12_21_38_56.png](post/images/SnipastePro_2024_11_12_21_38_56.png)

### Operation Choices/Options

| Value | Text            |
|-------|-----------------|
| 1     | Create          |
| 2     | Update          |
| 3     | Delete          |
| 4     | Access          |
| 5     | Upsert          |
| 115   | Archive         |
| 116   | Retain          |
| 117   | RollbackRetain  |
| 118   | Restore         |
| 200   | CustomOperation |
