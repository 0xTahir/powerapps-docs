---
title: "updateView| MicrosoftDocs"
manager: kvivek
ms.date: 04/23/2019
ms.service: "powerapps"
ms.topic: "reference"
applies_to: "Dynamics 365 (online)"
ms.assetid: 899d6eb3-62b4-4c1f-947c-aed1f8643caa
ms.author: "nabuthuk"
---
# updateView

[!INCLUDE[./includes/updateview-description.md](./includes/updateview-description.md)]

## Syntax

`updateView(context)`

## Parameters

| Parameter Name|Type|Required|Description|
| ------------- |----|--------|-----------|
|context|`Inputs`|yes|Contains values as set up by the customizer mapped to the name defined in the manifest, as well as in the utility functions|

## Example

```JavaScript
MyNameSpace.JSHelloWorldControl.prototype.updateView = function (context) {
	this._labelElement.innerText = "Hello World! (JS)";
};
```

## Remarks

Set the value of the field control to the raw value from the configured field


### Related topics

[Control](../control.md)<br/>
[PowerApps component framework API Reference](../../reference/index.md)<br/>
[PowerApps component framework Overview](../../overview.md)