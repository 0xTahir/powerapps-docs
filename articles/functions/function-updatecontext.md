<properties
	pageTitle="PowerApps: UpdateContext function"
	description="Reference information for the UpdateContext function in PowerApps, including syntax and examples"
	services="powerapps"
	documentationCenter="na"
	authors="gregli-msft"
	manager="dwrede"
	editor=""
	tags=""/>

<tags
   ms.service="powerapps"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="11/08/2015"
   ms.author="gregli"/>

# UpdateContext function in PowerApps #

Creates or updates [context variables](file-name.md) of the current [screen](file-name.md).

## Overview ##

Use the **UpdateContext** function to create a context variable, which temporarily holds a piece of information such as the number of times the user has clicked a button or the result of a data operation.

Context variables are scoped to a screen, which means that a formula on one screen can't access the value of a context variable on another screen.  In this way, context variables are similar to local variables in other programming tools. If you want the equivalent of a global variable, create a [collection](file-name.md) by using the **[Collect](function-collect.md)** or **[ClearCollect](function-clearcollect.md)** function.

PowerApps isn't a traditional programming tool.  At its core, PowerApps has a [data-flow model](file-name.md) that's automatically kept up to date, similar to how Excel automatically recalculates when a cell changes value. A context variable doesn't benefit from the data-flow model and isn't automatically updated. You must manage the state of each variable explicitly, which can be tedious and error prone.  Before you create a context variable, consider carefully whether you can achieve the same effect more efficiently by building a formula that's based on control, screen, or system state, as [Working with state](file-name.md) describes.

## Description ##

 To create or update context variables, pass a single [record](file-name.md) to the **UpdateContext** function. In each record, specify the name of a column, which defines or matches the name of the variable, and the value to which you want to set that variable.

- If you specify the name of a variable that you've previously defined, **UpdateContext** sets the value of the variable to the value that you specify.
- If you specify the name of a variable that doesn't yet exist, **UpdateContext** creates a variable with that name and sets the value of that variable to the value that you specify.
- If you previously defined a variable but don't specify it in this particular **UpdateContext** formula, its value remains the same.

You can't remove a context variable after you define it.

You reference a context variable in a formula by using the variable's column name. For example, **UpdateContext( { ShowLogo: true } )** creates a context variable, named **ShowLogo**, and sets its value to **true**. You can then use the value of this context variable by using the name **ShowLogo** in formulas.  You can write "**ShowLogo**" as the formula for the **Visible** property of an image control and show or hide that image control based on the value of the context variable.

As the examples later in this topic show, context variables can hold several kinds of information, including these:

- a single value
- a record
- a collection
- an object reference
- any result from a formula

A context variable holds its value until the user closes the app.  If you define a context variable and set its value on a particular screen, that information remains intact even if the user switches to a different screen.

Every context variable is scoped to a screen. If you want to define a context variable on one screen and modify that variable from another screen, you must build a formula that's based on the **[Navigate](function-navigate.md)** function.

**UpdateContext** has no return value, and you can use it only within a [behavior formula](file-name.md).

## Syntax ##

**UpdateContext**( *UpdateRecord* )

- *UpdateRecord* – Required. A record that contains the name of at least one column and a value for that column. A context variable is created or updated for each column and value that you specify.

**UpdateContext**( { *ContextVariable1*: *Value1* [, *ContextVariable2*: *Value2* [, ... ] ] } )

- *ContextVariable1* - Required.  The name of a context variable to create or update.

- *Value1* - Required.  The value to assign to the context variable.

- *ContextVariable2*: *Value2*, ... - Optional. Additional context variables to create or update and their values.

## Examples ##

| Formula | Description | Result |
|---------|-------------|--------|
| **UpdateContext( {&nbsp;Counter:&nbsp;1&nbsp;} )** | Creates or modifies the context variable **Counter**, setting its value to **1**.  | **Counter** has the value **1**. You can reference that variable by using the name **Counter** in a formula. |
| **UpdateContext( {&nbsp;Counter:&nbsp;2&nbsp;} )** | Sets the value of the **Counter** context variable from the previous example to **2**. | **Counter** has the value **2**.  |
| **UpdateContext( {&nbsp;Name:&nbsp;"Lily",&nbsp;Score:&nbsp;10&nbsp;} )** | Creates or modifies the context variables **Name** and **Score**, setting their values to **Lily** and **10** respectively.| **Name** has the value **Lily**, and **Score** has the value **10**. |
| **UpdateContext( {&nbsp;Person:&nbsp;{&nbsp;Name:&nbsp;"Milton", Address:&nbsp;"1&nbsp;Main&nbsp;St"&nbsp;}&nbsp;} )** | Creates or modifies the context variable **Person**, setting its value to a record. The record contains two columns, named **Name** and **Address**. The value of the **Name** column is **Milton**, and the value of the **Address** column is **1 Main St**.|**Person** has the value of record **{&nbsp;Name:&nbsp;"Milton", Address:&nbsp;"1&nbsp;Main&nbsp;St"&nbsp;}&nbsp;}**.<br><br>Reference this record as a whole with the name **Person**, or reference an individual column of this record with **Person!Name** or **Person!Address**. |
| **UpdateContext( {&nbsp;Person: Patch(&nbsp;Person,&nbsp;{Address:&nbsp;"2&nbsp;Main&nbsp;St"&nbsp;}&nbsp;) }&nbsp;)** | Works with the **[Patch](function-patch.md)** function to update the **Person** context variable by setting the value of the **Address** column to **2 Main St**.  | **Person** now has the value of record **{&nbsp;Name:&nbsp;"Milton", Address:&nbsp;"2&nbsp;Main&nbsp;St"&nbsp;}&nbsp;}**.  |

### Step-by-step example ###

1. Name the default screen **Source**, add another screen, and name it **Target**.

1. On the **Source** screen, add two buttons, and set their **Text** properties so that one says **English** and the other says **Spanish**.

1. Set the **OnSelect** property of the **English** button to this expression:<br>**Navigate(Target, ScreenTransition!Fade, {Language:"English"})**

1. Set the **OnSelect** property of the **Spanish** button to this expression:<br>**Navigate(Target, ScreenTransition!Fade, {Language:"Spanish"})**

1. On the **Target** screen, add a label, and set its **Text** property to this expression:<br>**If(Language="English", "Hello!", "Hola!")**

1. On the **Target** screen, click **Shapes** on the **Insert** tab, and then click the Back arrow.

1. Set the Back arrow's **OnSelect** property to this formula:<br>**Navigate(Source, ScreenTransition!Fade)**

1. From the **Source** screen, press F5, and then click the button for either language.<br>On the **Target** screen, the label appears in the language that corresponds to the button that you clicked.

1. Click the Back arrow to return to the **Source** screen, and then click the button for the other language.<br>On the **Target** screen, the label appears in the language that corresponds to the button that you clicked.

1. Press Esc to return to the default workspace.

[Another example](add-screen-context-variable.md)