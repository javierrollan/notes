---
creation date: 2023-08-28 12:52
modification date: Monday 28th August 2023 12:52:11
tag: splunk
---
# Get Started with Visualizations

## Visualization Reference

Compare options and select a visualization to show the data insights that you need.

| Visualization         | Usage                                                                                                                                                                                                                                                               |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Events List           | Show the events that a search generates.<br> <ul><li>Show events without additional processing.</li><li>Show extracted fields and values directly in the dashboard.</li><li>Users can click on event fields or timestamps to open a more specific search.</li></ul> |
| Table                 | Compare and aggregate field values.<br> <ul><li>Isolate one or more specific fields from search results.</li><li>Add formatting to highlight trends or patterns in specific fields.</li></ul>                                                                       |
| Charts                | Visualize one or more dimensions in a data set. Use one of the following chart types depending on how many dimensions, or fields, you are visualizing.<br> <ul><li>Pie</li><li>Area, line, column, bar</li><li>Bubble and scatter</li></ul>                         |
| Single value          | Show an aggregated metric in context.<br> <ul><li>Track recent changes or trends in real-time.</li><li>Use colors to add context dynamically</li></ul>                                                                                                              |
| Gauges                | <ul><li>Show an aggregated metric against a range.</li><li>Track a metric as it approaches a specific target.</li></ul>                                                                                                                                             |
| Maps                  | Visualize data with geographic coordinates.<br> <ul><li>Use a chloropeth map to show and compare regional trends or concentrations.</li><li>Use a marker map to plot geographic data.</li></ul>                                                                                                                                                                                                                         |
| Custom visualizations | Analyze and represent unique data sets.<br> An admin must install custom visualization apps to make them available for Splunk users.                                                                                                                                | 
## Data Structure requirements for visualizations

Visualizations require search results in specific formats or data structures. Write queries to generate results in the correct format for the visualization that you are building.
### Data and formatting requirements

Depending on the visualization that your are creating, you can use specific search commands to generate results in the correct format.

Charts visualize one or more data **series**, or related data points. Depending on the chart type or complexity, the number and ordering of data series can vary.

Single value and gauge visualizations represent a single numerical value.

Maps combine a query and other data components, including data with coordinates or place information, lookup definitions, and geographical markup files.
#### Using the statistics table

When creating a visualization, you can check the **Statistics** table after running a search to make sure that results fields are generated correctly. The number and order of **Statistics** table columns show you the data structure that a search generated.
### Additional information

Review specific visualization topics to check data format requirements and query recommendations.