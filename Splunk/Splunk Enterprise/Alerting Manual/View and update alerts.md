---
creation date: 2023-08-24 15:36
modification date: Thursday 24th August 2023 15:36:40
tag: splunk
---
# View and update alerts

## Access and update alerts

There are several ways to access and edit alerts. Here is a comparison of typical alert management tasks and where to complete them in Splunk Web.

| Task                                                        | Where to Go                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------------- |
| View all alerts in  the current app context.                | **Alerts** page                                                     |
| Select an alert to review or update.                        | **Alerts** page                                                     |
| View and edit alert details.                                | From the **Alerts** page, select and alert to open its detail page. |
| Review available alert actions and browse for more actions. | **Alert Actions** management page.                                  |
| Review recently triggered alerts.                           | **Triggered Alerts** listing page.                                  | 

## Alerts page

The **Alerts** page lists all alerts, for an app. It is available from the top level navigation menu for an app. From the **Alerts** page you can use the following options.

| Option                                          | Description                                                                                                                                                                                                                                                          |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Select a filtering option for displayed alerts. | <ul><li><b>All</b>. View all alerts for which you have view permission.</li><li><b>Yours</b>. View alerts that you own.</li><li><b>This App's</b>. View alerts for the current app. Only alerts for which you have permission to view display in the list.</li></ul> |
| Select any displayed alert                      | Opens the detail page for an alert. You can review and make additional edits to the alert on the detail page.                                                                                                                                                        |
| **Open in Search**                              | View or modify the alert's search string in the **Search** page. Time range updates in Splunk Web are not supported.                                                                                                                                                 |
| **Edit**                                        | Opens the detail page for an alert. You can review and make additional edits to the alert on the detail page.                                                                                                                                                        | 
#### Edit an alert search

1. From the **Alerts page**, locate the alert and click **Open in Search**. The alert search opens in the **Search** page.
2. Edit the search string as needed.
3. Run the edited search.
4. Click **Save** to update the alert. If prompted again, click **Save**.
5. Select from the following options.

| Option             | Description                      |
| ------------------ | -------------------------------- |
| "View alert"       | Opens the alert detail page.     |
| "Continue editing" | Return to the **Search** page.   |
| "Permissions"      | View and edit alert permissions. | 
#### Access alert details

From the **Alerts** page, select an alert to review and update its settings. Authorized users can change the following alert settings.
+ Enable or disable the alert
+ App context
+ Permissions
+ Alert type and timing
+ Trigger conditions
+ Alert actions
## Using the alerts action manager

You can review and configure settings for available alert actions on the alert actions manager page.
#### Prerequisites

(Optional) Review Alert action permissions.
#### Steps

1. From the top-level navigation bar, select **Settings > Alert Actions**.
2. Depending on your permissions, you can do the following for an alert action.
	+ Enable or disable the alert action
	+ Update permissions
	+ Check usage stats
	+ View log events
3. (Optional) Click **Browse More** to find apps with built-in custom alert actions.
## Triggered alerts

Review all recently triggered alerts on the **Triggered Alerts** page.
### Triggered alert listing

Alerts appear on the **Triggered Alerts** page under the following conditions.
+ The "Add to Triggered Alerts" action is enabled for the alert.
+ The alert triggered recently.
+ The alert retention time is not complete.
+ The triggered alert listing has not been deleted.

On the **Triggered Alerts** page, details appear in the following categories.

| Category         | Description                                                                                                                                                                       |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Time**         | Trigger date and time.                                                                                                                                                            |
| **Fired alerts** | Triggered alert name(s).                                                                                                                                                          |
| **App**          | Alert app context.                                                                                                                                                                |
| **Type**         | Alert type.                                                                                                                                                                       |
| **Severity**     | Assigned alert severity level. Severity levels can help you sort or filter alerts on this page.                                                                                   |
| **Mode**         | Alert triggering configuration mode. "Per-result" means that the alert triggered because of a single event. "Digest" means that the alert triggered because of a group of events. | 

Records of triggered alerts are available for twenty-four hours by default. You can configure this expiration time on a per-alert basis.

### Access and update triggered alerts

Here are steps for accessing and using the **Triggered Alerts** page.
#### Prerequisites

(Optional) Review Triggered alert listing.
#### Steps

1. From the top-level navigation bar, select **Activity > Triggered Alerts**.
2. Filter any displayed alerts according to **App, Owner, Severity, and Alert** (alert name).
3. (Optional) Use the keyword search to find triggered alerts by alerts name or app context.
4. (Optional) Take the following actions from the Alert Manager.
	+ View alert search results.
	+ Edit the alert search.
	+ Delete a triggered alert listing.

### Delete a triggered alert listing

By default, triggered alert records on the **Triggered Alerts** page expire after twenty-four hours. There are a few ways to change whether a triggered alert listing appears on this page.
+ Update triggered alert listing expiration time.
+ Delete a triggered alert listing from the **Triggered Alerts** page.
+ Disable an alert to prevent it from triggering.
## Additional alert configuration options

It is recommended to create alerts in the **Search** page and edit them from the **Alerts** page. In rare cases, authorized users might access the **Searches, Reports and Alerts** page for the following configurations.
### Enable summary indexing

Summary indexing is available on scheduled alerts. It can help you perform analysis or report on large amounts of data over long time ranges. Typically, this is a time consuming and can impact performance if several users ar running similar searches on a regular basis.
#### Prerequisites

Ensure that the alert's search generates statistical or summary data.
#### Steps

1. Using the top-level navigation bar, select **Settings > Searches, Reports and Alerts**.
2. Click **Edit > Advanced Edit** for the alert you'd like to modify.
3. To enable the summary indexing to gather data on a regular interval, search for "alert_type" in the search window in the upper-left section of the window. Set **alert_type** to **always**.
4. For a scheduled alert, search for "summary" to view the summary index options. Set **actions.summary_index** to **true**. If not already specified, this sets the **Alert condition** to "Always". This option is not available for real-time alerts.
5. Click **Save**.
### Searches and summary indexing

To use summary indexing with an alert, create a search that computes statistics or a summary for events over a period of time. Search results are saved into a summary index that you designate. You can search over this smaller summary index instead of working with the larger original dataset.

It is typical to use reporting commands in a search that populates a summary index. 
### Update triggered alert record lifespans

By default, each triggered alert record on the **Triggered Alerts** page expires after 24 hours. 

Here are the steps for updating the lifespans of the triggered alert records for a specific alert. These steps apply only to alerts that have the "Add to Triggered Alerts" action enabled.
1. From the top-level navigation bar, select **Settings > Searches, Reports and Alerts**.
2. (optional) Select **Type > Alerts** to filter the list so it displays only alerts.
3. Locate the alert that you want to modify under **Name**.
4. Select **Edit > Edit Alert**.
5. Define the lifespan of the triggered alert record by setting the **Expires** field. Enter an integer and select a time unit from the dropdown.
6. Click **Save**.
