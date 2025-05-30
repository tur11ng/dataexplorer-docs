---
title:  Table visualization
description:  This article describes the table visualization.
ms.reviewer: alexans
ms.topic: reference
ms.date: 01/28/2025
---
# Table

> [!INCLUDE [applies](../includes/applies-to-version/applies.md)] [!INCLUDE [fabric](../includes/applies-to-version/fabric.md)] [!INCLUDE [azure-data-explorer](../includes/applies-to-version/azure-data-explorer.md)] [!INCLUDE [monitor](../includes/applies-to-version/monitor.md)] [!INCLUDE [sentinel](../includes/applies-to-version/sentinel.md)]

Default - results are shown as a table.

> [!NOTE]
> This visualization can only be used in the context of the [render operator](render-operator.md).

## Syntax

*T* `|` `render` `table` [`with` `(`*propertyName* `=` *propertyValue* [`,` ...]`)`]

[!INCLUDE [syntax-conventions-note](../includes/syntax-conventions-note.md)]

## Parameters

| Name | Type | Required | Description |
| -- | -- | -- | -- |
| *T* | `string` |  :heavy_check_mark: | Input table name.
| *propertyName*, *propertyValue* | `string` | | A comma-separated list of key-value property pairs. See [supported properties](#supported-properties).|

### Supported properties

All properties are optional.

::: moniker range="microsoft-fabric  || azure-data-explorer"

|*PropertyName*|*PropertyValue*                                                                   |
|--------------|----------------------------------------------------------------------------------|
|`accumulate`  |Whether the value of each measure gets added to all its predecessors. (`true` or `false`)|
|`legend`      |Whether to display a legend or not (`visible` or `hidden`).                       |
|`series`      |Comma-delimited list of columns whose combined per-record values define the series that record belongs to.|
|`ymin`        |The minimum value to be displayed on Y-axis.                                      |
|`ymax`        |The maximum value to be displayed on Y-axis.                                      |
|`title`       |The title of the visualization (of type `string`).                                |
|`xaxis`       |How to scale the x-axis (`linear` or `log`).                                      |
|`xcolumn`     |Which column in the result is used for the x-axis.                                |
|`xtitle`      |The title of the x-axis (of type `string`).                                       |
|`yaxis`       |How to scale the y-axis (`linear` or `log`).                                      |
|`ycolumns`    |Comma-delimited list of columns that consist of the values provided per value of the x column.|
|`ytitle`      |The title of the y-axis (of type `string`).                                       |

::: moniker-end

::: moniker range="azure-monitor || microsoft-sentinel"

|*PropertyName*|*PropertyValue*                                                                   |
|--------------|----------------------------------------------------------------------------------|
|`series`      |Comma-delimited list of columns whose combined per-record values define the series that record belongs to.|
|`title`       |The title of the visualization (of type `string`).                                |
  
::: moniker-end

## Example

This query outputs a snapshot of the first 10 storm event records, displayed in a table format.

[!INCLUDE [help-cluster-note](../includes/help-cluster-note.md)]

:::moniker range="azure-data-explorer"
> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAwsuyS/KdS1LzSsp5qpRKEnMTlUwNFAAMotS81JSi4AiSTmpAB5OWY8lAAAA" target="_blank">Run the query</a>
::: moniker-end

```kusto
StormEvents
| take 10 
| render table 
```

:::image type="content" source="media/visualization-table/table-visualization.png" alt-text="Screenshot of table visualization output." lightbox="media/visualization-table/table-visualization.png":::
