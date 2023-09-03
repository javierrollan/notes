---
creation date: 2023-08-28 12:52
modification date: Monday 28th August 2023 12:52:41
tag: splunk
---
# Table Visualizations
## Table Visualizations Overview

Tables can help compare and aggregate field values. Use a table to visualize patterns for one or more metrics across a data set. Start with a query to generate a table an use formatting to highlight values, add context, or create focus for the visualization.
## Generate a table

To generate a table, write a search that includes a transforming command. From the **Search** page, run the search and select the **Statistics** tab to view and format the table.
#### Table sparklines

Sparklines show data patterns or trends in a results set. To generate a table sparkline, use `stats` or `chart` with the `sparkline` function in a search.

Sparkline width is determined by default data binning. You can adjust data binning as a parameter of the `sparkline` command.
## Format table visualizations

Use the **Format** menu to configure a table visualization.
### Add summary statistics

Use the **Format** menu **Summary** tab to include column totals and percentages. For each statistic, a highlighted summary row appears at the bottom of the table. Column totals and/or percentages appear at the bottom of each column that contains numeric values.

**Note**: Values in a summary row reflect statistics for the complete search result set. For tables with more than one page of results, summary row values do not apply only to the currently displayed page.
#### Summary and data row differences

There are some behavior and formatting differences between summary rows and data rows table.

| Behavior or format                                                | Summary rows | Data rows |
| ----------------------------------------------------------------- | ------------ | --------- |
| Static highlight color                                            | Yes          | No        |
| Values in the row can skew table color formatting or data overlay | No           | Yes       |
| Column number formatting applied to the row                       | Yes          | Yes       |
| Drilldown available for the row                                   | No           | Yes       |
| Included in PDF or CSV export                                     | No           | Yes       | 
#### Totals data row behavior

A static summary row fits most use cases. if you generate a totals data row using the `addcoltotals` SPL command in a search, note the following table behavior impacts.
+ An `addcoltotals` row is treated as a data row in the table.
+ Because they are handled as data rows, `addcoltotals` rows are included in a PDF or CSV dashboard export.
+ Color scales or data overlay cab be skewed if a table includes an `addcoltotals` data row.
+ Tables should not include an `addcoltotals` data row and a column totals summary row. If you opt to include a totals summary row, adjust the search to remove the `addcoltotals` command.
## Format table columns

You can format individual table columns to add context or focus to the visualization. Click on the paintbrush icon at the top of each column to customize color and number formatting.

**Note**: Column formatting is not available for columns representing the `_time` field or for sparkline columns.
### Column color

Select and configure one of the following color modes for the column.

**Note**: Column color formatting overrides existing heat map or high/low value data overlay settings.
### Scale

Use a sequential or divergent color scale on column cells. You can choose a preset scale or custom configuration to manage how colors in the scale are applied to column cells.

Depending on search results and data distribution, column color gradation can vary. Columns with relatively similar values will show the most color gradation. Outlying values can limit the gradation.
### Color scale options

| Scale type | Description                                                                    |
| ---------- | ------------------------------------------------------------------------------ |
| Sequential | Use a sequential scale to show how results approach a high value in the column |
| Divergent  | A divergent scale can show how results approach high and low values.           | 
### Configure a custom color scale

You can configure custom color handling by indicating minimum, midpoint, and maximum value colors. Use on of the following options to configure the minimum, midpoint, and maximum value interpretations for the color scale.
#### Configuration options

| Option                    | Description                                                                                                           |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Highest and lowest values | This option highlights the highest and lowest values in the column.                                                   |
| Number                    | Indicate numeric values thresholds. Cell color is determined according to how values align with the three thresholds. |
| Percent                   | Determine cell color using percentages of the results value range.                                                    |
| Percentile                | Determine cell color using percentiles of the results value distribution.                                             | 
#### Ranges

Apply color to cells in this column according to value ranges.

Use ranges to compare cell values categorically. Range configuration options:
+ Adjust the default range value and color settings.
+ Add or remove ranges.
#### Values

Apply colors according to cell values.

Use automatic value coloring options or define custom rules. Automatic coloring applies a color to every cell in the column. Cells with the same value appear in the same color. Custom rules can help highlight specific values that you are monitoring.
#### Number format

Enable and adjust number formatting for each column. The number format settings panel includes the following options:
+ Enable or disable number formatting.
+ Set decimal precision.
+ Opt to use thousand separators.
+ Specify a measurement unit to add context to the values in this column.
### Configure table properties

After generating a table, use the **Format** menu to configure one or more of the following table components.
+ The number of rows shown in each table page.
+ Wrapping.
+ Table row number display.
#### Data overlay

The **Format** menu also includes the following data overlay options.
#### Heat map

Add different shades of a particular color to the table to show value variation over table rows.
#### High and low value

Add high and low value colors to the table to highlight the highest and lowest values. Use data overlay only if you are not adding column color formatting to the table. Column color formatting overrides data overlay configurations.
#### Drilldown

By default, drilldown is disabled when you save visualizations to a dashboard. You can use the drilldown editor or Simple XML to enable and configure drilldown options.
#### Simple XML drilldown options

In simple XML, you can set the drilldown option to one of the following values. Use the `<drilldown>` element to change the drilldown behavior.

| Option | Behavior                                                                                            |
| ------ | --------------------------------------------------------------------------------------------------- |
| Cell   | By default, opens a secondary search using the field and value in the selected cell.                |
| Row    | By default, opens a secondary search using the field and values from the cells in the selected row. |
| None   | Disables drilldown.                                                                                                    |
## Table column Simple XML

Use format rules to configure tables columns in Simple XML. Indicate color scale and color palette rules to manage column color formatting. You can also use a number format rule to manage the appearance of numeric cell values.