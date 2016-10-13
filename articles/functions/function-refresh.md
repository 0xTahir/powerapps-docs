<properties
	pageTitle="Refresh function | Microsoft PowerApps"
	description="Reference information, including syntax and an example, for the Refresh function in PowerApps"
	services=""
	suite="powerapps"
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
   ms.date="10/21/2015"
   ms.author="gregli"/>

# Refresh function in PowerApps #

Refreshes the [records](../working-with-tables.md#records) of a [data source](../working-with-data-sources.md).

## Description ##

The **Refresh** function retrieves a fresh copy of a data source.  You'll see changes that other users made.

**Refresh** has no return value, and you can use it only in [behavior formulas](../working-with-formulas-in-depth.md#behavior-formulas).

## Syntax ##

**Refresh**( *DataSource* )

- *DataSource* – Required. The data source that you want to refresh.

## Example ##

In this example, you'll refresh the data source named **IceCream**, which starts with this data:

![](media/function-refresh/icecream.png)

A user on another device changes the **Quantity** in the **Strawberry** record to **400**.  You won't see this change until this formula executes:

**Refresh( IceCream )**

After that formula executes, galleries that are bound to the **IceCream** data source will show the updated value for **Strawberry**:

![](media/function-refresh/icecream-after.png)
