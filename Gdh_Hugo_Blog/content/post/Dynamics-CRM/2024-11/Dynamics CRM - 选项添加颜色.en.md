---
date: '2024-11-14T20:00:00+08:00'
title: 'Dynamics CRM - Optionset add colors'
description: 'Optionset add colors'
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

## Effects

- View
![Add color view effects for options](post/images/SnipastePro_2024_11_15_12_59_25.png)

- Form
![Add color form effects for options](post/images/SnipastePro_2024_11_15_13_02_05.png)

- Subgrid
![Add color subgrid effects for options](post/images/SnipastePro_2024_11_15_13_01_31.png)

- Quick create form
![Add color quick create form effects for options](post/images/SnipastePro_2024_11_15_13_03_44.png)

## Steps

**Whether adding globally or "locally," you need to set the option colors first.**

![Set Option Colors](post/images/SnipastePro_2024_11_15_12_28_49.png)

> The colors I commonly use are:
>
> - Bule `#70b6ff`
> - Green `#67c23a`
> - Red `#f8a2a2`
> - Gray `#909399`
> - Orange `#e7a544`

### Global Addition

Global addition means that you only need to set it in one place, and the option colors will display in views, forms, and subgrids.

#### Open the Solution

> Use the Classic UI to open it; I haven't found where to set this in the new UCI interface.
>
> If you know, feel free to leave a comment below so we can learn from each other.

#### Add control

Select the entity and add the control.

![Add Power Apps grid control 1](post/images/SnipastePro_2024_11_15_12_35_30.png)

Select **Power Apps grid control**
![Add Power Apps grid control 2](post/images/SnipastePro_2024_11_15_12_36_42.png)

Set **Enable OptionSet Color** to "Yes," and then enable the **Power Apps grid control** on the web side.
![Add Power Apps grid control 3](post/images/SnipastePro_2024_11_15_12_38_09.png)

Then save and publish.

### Local Addition

Local addition means you only want to add colors to options at a specific location:

- Subgrid

- Quick Create Form

- Main Form

- And so on...

The steps are the same. Below, I will use adding to the Quick Create Form as an example:

1. Open the Quick Create Form.

2. Select the option field and click "Change Properties.

3. In the Field Properties tab, select the "Controls" tab.

4. Add the **OptionSet Wrapper** control, then enable the **OptionSet Wrapper** control on the web side.

5. Save and publish.

![Add Controls Locally](post/images/SnipastePro_2024_11_15_12_51_49.png)
