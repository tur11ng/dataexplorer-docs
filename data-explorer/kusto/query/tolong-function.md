---
title:  tolong()
description: Learn how to use the tolong() function to convert the input value to a long number representation.
ms.reviewer: alexans
ms.topic: reference
ms.date: 03/09/2025
---
# tolong()

> [!INCLUDE [applies](../includes/applies-to-version/applies.md)] [!INCLUDE [fabric](../includes/applies-to-version/fabric.md)] [!INCLUDE [azure-data-explorer](../includes/applies-to-version/azure-data-explorer.md)] [!INCLUDE [monitor](../includes/applies-to-version/monitor.md)] [!INCLUDE [sentinel](../includes/applies-to-version/sentinel.md)]

Converts the input value to a long (signed 64-bit) number representation.

> [!NOTE]
> When possible, use [long literals](scalar-data-types/long.md#long-literals) instead.

## Syntax

`tolong(`*value*`)`

[!INCLUDE [syntax-conventions-note](../includes/syntax-conventions-note.md)]

## Parameters

| Name | Type | Required | Description |
|--|--|--|--|
| *value* | scalar |  :heavy_check_mark: | The value to convert to a [long](scalar-data-types/long.md).|

## Returns

If conversion is successful, the result is a long number.
If conversion isn't successful, the result is `null`.

## Example

The following example checks if the result of converting the string `"123"` to a long number is equal to the integer 123.

:::moniker range="azure-data-explorer"
> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAysoyswrUSjJz8nPS9dQMjQyVtJUsLVVADIAlTTbCRoAAAA=" target="_blank">Run the query</a>
::: moniker-end

```kusto
tolong("123") == 123
```

## Related content

* [Scalar function types at a glance](scalar-functions.md)
* [The long data type](scalar-data-types/long.md)
* [toint()](toint-function.md)
* [todecimal()](todecimal-function.md)
