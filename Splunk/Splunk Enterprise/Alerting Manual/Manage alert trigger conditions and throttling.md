---
creation date: 2023-08-24 15:30
modification date: Thursday 24th August 2023 15:30:52
tag: splunk
---
# Manage alert trigger conditions and throttling

## Configure alert trigger conditions

An alert can search for events on a schedule or in real time, but it does not have to trigger every time search results appear.

##### Alert triggering and alert throttling

Throttling an alert is different from configuring trigger conditions. Search results are evaluated to check if they match the trigger conditions. Throttling controls whether triggering is suppressed for a period of time. 

#### Alert types and triggering options

Both alert types offer trigger configuration options for working with the alert search results. Here is a comparison:

| Alert type | Trigger options                                        | Specifying trigger conditions                                                                                   | How matching results trigger the alert                                                                                |
| ---------- | ------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Scheduled  | Add trigger conditions to evaluate search results      | Built-in result and field count options or a custom triggering condition.                                       | Trigger the alert once each time search results match the specified condition or one time for every matching result.  |
| Real-time  | Per-result                                             | N/A                                                                                                             | By default, alert triggers one time for every matching result.                                                        |
| Real-time  | Trigger conditions that include a rolling time window. | Built-in result and field count options or a custom conditions. Also specify a rolling time window or interval. | Trigger the alert once each time search results match the specified condition, or one time for every matching result. | 

#### How searches and trigger conditions work together

Trigger conditions work as a secondary search to evaluate the alert's initial search results. If the secondary search does not return results, the alert does not trigger. When the secondary search does generate results, the alert triggers.

The secondary search for trigger conditions does not determine what information is available for notifications or other alert actions. Result fields and other information come from the initial base search.

Using the alert base search without trigger conditions can limit the information available for notifications.
## Throttle alerts

Use throttling to suppress alert triggering for a specific time period. Alerts can trigger frequently because of similar search results or scheduling.
#### Throttle configuration

Throttling is also known as suppression.

| Alert type | Triggering option   | How to configure throttling                                                                                                                                                                                                                                                           |
| ---------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scheduled  | Once                | Indicate a suppression period using the time value field and dropdown increments. Time values must be greater than zero.                                                                                                                                                              |
| Scheduled  | Per-result          | **1.** Type one or more comma-separate fields to check for matching values in events. Events with the same value for these fields are suppressed.<br> **2.** Indicate a suppression period using the time value field and dropdown increments. Time values must be greater than zero. |
| Real-time  | Rolling time window | Indicate a suppression period using the time value field and dropdown increments. Time values must be greater than zero.                                                                                                                                                              |
| Real-time  | Per-result          | **1.** Type one or more comma-separate fields to check for matching values in events. Events with the same value for these fields are suppressed.<br> **2.** Indicate a suppression period using the time value field and dropdown increments. Time values must be greater than zero. | 

#### Throttle scheduled and real-time searches

Throttling for alerting works similarly to throttling for scheduled and real-time searches.
## Define alert suppression groups to throttle sets of similar alerts
#### Alert suppression group best practices

Alert suppression groups perform best when they are composed of alerts that have the same alert suppression period and set of alerts actions. They should also share the same set of alert suppression fields, if they use suppression fields. This sharing of attributes helps to guarantee predictable behavior.