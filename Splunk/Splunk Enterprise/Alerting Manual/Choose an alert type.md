---
creation date: 2023-08-24 15:25
modification date: Thursday 24th August 2023 15:25:22
tag: splunk
---
# Choose an alert type

## Alert types

There are two alert types, scheduled and real-time. Depending on the scenario you can configure the behavior for either alert type.

| Alert type    | When It searches for events                                                                                                    | Triggering options                                                                                                                                                                                                 | Throttling options                                               |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| **Scheduled** | Searches according to a schedule.<br> Choose from the available timing options or use a cron expression to schedule the search | Specify conditions for triggering the alert based on result or result fields counts.<br> When a set of search results meets the trigger conditions the alert can trigger one time or once for each of the results. | Specify a time period for suppression.                           |
| **Real-time** | Searches continuously.                                                                                                         | **Per-result**: Triggers every time there is a search result.                                                                                                                                                      | Specify a time period and optional field values for suppression. |
| **Real-time** | Searches continuously.                                                                                                         | **Rolling time window**: Specify conditions for triggering the alert based on result or result field counts within a rolling time window.                                                                          | Specify a time period for suppression.                                                                 |

## Alert type and triggering scenarios

Depending on the events monitored, it may be needed a real-time alert that triggers with every result or a scheduled alert that only triggers if results meet certain conditions.
### Scheduled Alert

Use a scheduled alert to search for events on a regular basis and monitor whether they meet specific conditions. A scheduled alert is useful if immediate or real-time monitoring is not a priority.
### Real-time alert

Real-time alerts search for events continuously. They can be useful in situations where ==immediate monitoring and responses are important==.
#### Per-result triggering

A real-time with a per-result triggering condition is sometimes known as a "per-result alert".

> [!warning] **Caution:**
> In a high availability deployment, use per-result triggering with caution. If a peer is not available, a real-time search does not warm that the search might be incomplete. It is recommended to use a scheduled alert for this deployment.
#### Rolling time window triggering

A real-time alert with time window triggering is sometimes known as a "rolling window alert". This alert type and triggering are useful when a specific time window is an important part of the event pattern you are monitoring in real time.

