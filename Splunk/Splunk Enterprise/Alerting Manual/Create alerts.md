---
creation date: 2023-08-24 15:27
modification date: Thursday 24th August 2023 15:27:06
tag: splunk
---
# Create alerts

## Create scheduled alerts

### Using cron expressions

You can use a cron expression to customize alert scheduling.
### Create a scheduled alert

**Prerequisites**
+ Use cron expressions for scheduling
+ Alert scheduling tips
+ Configure alert trigger conditions
+ Monitor triggered alerts

**Steps**
1. Navigate to the **Search** page in the **Search and Reporting** app.
2. Create a search.
3. Select **Save as > Alert**.
4. Enter a title and optional description.
5. Specify permissions.
6. Configuring alert scheduling. There are two options for scheduling.

| Option                                                                                              | Next steps for this option                                                                                                                                                                                                                                                                                                                                                              |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Select one of the available scheduling options and set a time.                                      | None.                                                                                                                                                                                                                                                                                                                                                                                   |
| For further customization, select **Run on Cron Schedule** to use a time range and cron expression. | **a.** Enter the **Earliest** and **Latest** values for the search time range. These values override the original search time range. To avoid overlaps or gaps, the execution schedule should match the search time range. For example, to run a search every 20 minutes the search time range should also be 20 minutes (-20m).<br> **b.** Enter a cron expression to schedule the search. | 

7. (Optional) Change the **Expires** setting. This setting control the lifespan of triggered alert records, which appear on the **Triggered Alerts** page.
8. Configure trigger conditions.
9. (Optional) Configure a trigger throttling period.
10. Select one or more alert actions that should happen when the alert triggers.
11. Click Save.

## Use cron expressions for alert scheduling

The Splunk cron analyzer defaults to the timezone where the search head is configured. This can be verified or changed by going to **Settings > Searches, reports and alerts > Scheduled time**.
## Alert scheduling tips

Best practices and suggestions for working with scheduled alerts.

---
#### Best Practices

***Coordinate an alert schedule and search time range*

Coordinate an alert schedule with the search time range prevents event data from being evaluated twice by the search. If search time range exceeds the search schedule, event data sets can overlap.

When a search time range is shorter than the time range for the scheduled alert, an event might never be evaluated.

***Schedule alerts with at least one minute of delay*

This practice is important in distributed search deployments where event data might not reach the indexer immediately. A delay ensures that you are counting all events, not just the events that were indexed first.
#### Manage concurrent scheduled search priority

Depending on the deployment, only one scheduled alert might be able to run at a time. In this case, multiple scheduled searches set to run at the same time are run consecutively.

#### Differences between scheduled reports and alerts

A scheduled report is like a scheduled or real-time alert in certain ways. A scheduled report can be set up with an action to run each time the scheduled report runs.

Scheduled reports are different from alerts because a scheduled report's action runs every time the report is run. The report action does not depend on trigger conditions.
+ **Scheduled report**: runs its action every time the report completes.
+ **Scheduled alert**: only runs alert action when it is triggered by search results.
## Create real-time alerts

Use a real-time alert to monitor events or event patterns as they happen. You can create real-time alerts with per-result triggering or rolling time window triggering. Real-time alerts can be costly in terms of computing resources.