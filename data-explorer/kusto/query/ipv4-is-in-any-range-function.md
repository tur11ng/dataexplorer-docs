---
title:  ipv4_is_in_any_range()
description: Learn how to use the ipv4_is_in_any_range() function to check if the IPv4 string address is in any of the IPv4 address ranges.
ms.reviewer: alexans
ms.topic: reference
ms.date: 08/11/2024
---
# ipv4_is_in_any_range()

> [!INCLUDE [applies](../includes/applies-to-version/applies.md)] [!INCLUDE [fabric](../includes/applies-to-version/fabric.md)] [!INCLUDE [azure-data-explorer](../includes/applies-to-version/azure-data-explorer.md)] [!INCLUDE [monitor](../includes/applies-to-version/monitor.md)] [!INCLUDE [sentinel](../includes/applies-to-version/sentinel.md)]

Checks whether IPv4 string address is in any of the specified IPv4 address ranges.

## Performance tips

[!INCLUDE [index-performance-tip-note](../includes/multi-arg-index-performance-note.md)]

## Syntax

`ipv4_is_in_any_range(`*Ipv4Address* `,` *Ipv4Range* [ `,` *Ipv4Range* ...] `)`

`ipv4_is_in_any_range(`*Ipv4Address* `,` *Ipv4Ranges* `)`

[!INCLUDE [syntax-conventions-note](../includes/syntax-conventions-note.md)]

## Parameters

| Name | Type | Required | Description |
|--|--|--|--|
| *Ipv4Address*| `string` |  :heavy_check_mark: | An expression representing an IPv4 address.|
| *Ipv4Range*| `string` |  :heavy_check_mark: | An IPv4 range or list of IPv4 ranges written with [IP-prefix notation](#ip-prefix-notation).|
| *Ipv4Ranges*| `dynamic` |  :heavy_check_mark: | A dynamic array containing IPv4 ranges written with [IP-prefix notation](#ip-prefix-notation).|

> [!NOTE]
> Either one or more *IPv4Range* strings or an *IPv4Ranges* dynamic array is required.

[!INCLUDE [ip-prefix-notation](../includes/ip-prefix-notation.md)]

## Returns

* `true`: If the IPv4 address is in the range of any of the specified IPv4 networks.
* `false`: Otherwise.
* `null`: If conversion for one of the two IPv4 strings wasn't successful.

## Examples

### Syntax using list of strings

:::moniker range="azure-data-explorer"
> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAysoyswrUQhKLS7NKbHNLCgzic8sjs/Mi0/Mq4wvSsxLT9VQN7Q00jM0s9Az1DNT11FA4hrqG5mARQz0QNBQ3wLMMzIHyoG4hmbqmgA/iDq/YAAAAA==" target="_blank">Run the query</a>
::: moniker-end

```kusto
print Result=ipv4_is_in_any_range('192.168.1.6', '192.168.1.1/24', '10.0.0.1/8', '127.1.0.1/16')
```

**Output**

|Result|
|--|
|true|

### Syntax using dynamic array

:::moniker range="azure-data-explorer"
> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAysoyswrUQhKLS7NKbHNLCgzic8sjs/Mi0/Mq4wvSsxLT9VQMjQy1zMAQkMlHYWUyrzE3MxkjWgUUSVDSyM9QzMLPUMgN1ZTEwBpBE7bVQAAAA==" target="_blank">Run the query</a>
::: moniker-end

```kusto
print Result=ipv4_is_in_any_range("127.0.0.1", dynamic(["127.0.0.1", "192.168.1.1"]))
```

**Output**

|Result|
|--|
|true|

### Extend table with IPv4 range check

:::moniker range="azure-data-explorer"
> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAA1WP0QqCMBSG7/cUwysFmR4ts8QHECK8l5ClQ0ZrhhuV0MN3lFh0/ruPc/6Po4Slx7Hj6iTsc5yupuxnzW+y8xtCcTzYJwyynAGDCDIv/NJkx2IMRLlDsSPkHBREYXNVYx+3mIsSflUfjJ2kHgLauBtgCUtdh5Ntf6Z0ceMaOMTWoKYgaCBvKl5W6J5WZn2llPfHppWmlbrlem4nrofFHv5/GnwAOfWtJ/wAAAA=" target="_blank">Run the query</a>
::: moniker-end

```kusto
let LocalNetworks=dynamic([
    "192.168.1.1/16",
    "127.0.0.1/8",
    "10.0.0.1/8"
]);
let IPs=datatable(IP:string) [
    "10.1.2.3",
    "192.168.1.5",
    "123.1.11.21",
    "1.1.1.1"
];
IPs
| extend IsLocal=ipv4_is_in_any_range(IP, LocalNetworks)
```

**Output**

|IP|IsLocal|
|---|---|
|10.1.2.3|true|
|192.168.1.5|true|
|123.1.11.21|false|
|1.1.1.1|false|

## Related content

* Overview of [IPv4/IPv6 functions](scalar-functions.md#ipv4ipv6-functions)
* Overview of [IPv4 text match functions](scalar-functions.md#ipv4-text-match-functions)
