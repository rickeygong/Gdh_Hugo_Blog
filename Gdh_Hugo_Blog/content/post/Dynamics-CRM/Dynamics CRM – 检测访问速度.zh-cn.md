---
date: '2024-10-15T12:55:51+08:00'
title: 'Dynamics CRM - 检查访问速度'
description: ''
slug: 'dynamics-crm-check-access-speed'
image: 'post/images/dynamics-crm-logo.png'
categories:
    - Dynamics-CRM
tags:
    - CRM
draft: false
keywords:
    - dynamics
    - crm
    - check-access-speed
---

## 检测访问速度

假设你的环境链接是：[https://sample.dynamics.cn/main.aspx]

在链接后面追加 `/tools/diagnostics/diag.aspx`，然后访问

```xml

# Url sample
https://sample.dynamics.cn/tools/diagnostics/diag.aspx

```

访问后才会出现 "Dynamics 365 Diagnostics" (Dynamics 365 诊断)，

点击 "Run" ，稍等片刻就会出现诊断结果。

![dynamics-365-diagnostics](post/images/SnipastePro_2024_11_12_20_58_02.png)
