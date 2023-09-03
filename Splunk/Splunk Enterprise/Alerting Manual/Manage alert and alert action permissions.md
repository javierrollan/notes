---
creation date: 2023-08-24 15:35
modification date: Thursday 24th August 2023 15:35:19
tag: splunk
---
# Manage alert and alert action permissions

## Alert permissions

Alerts are knowledge objects with defined permissions. User roles and capabilities determine alert creation, usage, editing, and other permissions.

By default, only users with the Admin or Power roles can do the following:
+ Create alerts.
+ Run real-time searches.
+ Schedule searches.
+ Save searches.
+ Share alerts.

Authorized users can share an alert with other app users by editing the alert level permissions. When sharing an alert with a user without the Admin or Power role, the user needs permission to access the alerting features.

Admins can configure alert action permissions to change what alerta actions are available to users in a particular app. 
### Sharing an alert

You can configure sharing preferences when creating an alert or editing alert permissions later. Here are the steps for editing alert permissions.
1. Navigate to the **Alerts** page in the **Search and Reporting** app.
2. Find the alert you want to share and select **Edit > Edit Permissions**.
3. Share the alert by configuring which users can access it. Here are the options.

| Option       | Sharing description                                               |
| ------------ | ----------------------------------------------------------------- |
| **Owner**    | Makes the alert private to the alert creator.                     |
| **App**      | Display the alert for all of the users of the app.                |
| **All apps** | Display the alert for all of the users of this Splunk deployment. | 

4. Select read and write permissions for the user roles listed.
	* **Read**: Users can see the alert on the **Alerts** page and run the alert in the app.
	* **Write**: users with appropriate permissions can modify, enable, and disable the alert.
## Alert action permissions

Depending on the user **roles** that you have, you can configure alert action permissions for available alerts.

To review and change alert actions permissions, use the **Alert actions** manager page.

Alert actions are **knowledge objects.**
## Configure webhook allow list

The webhook allow list is a list of authorized URL endpoints to which a webhook alert action can send HTTP POST requests. Before a triggered alert can send a request to a specified webhook URL, Splunk Enterprise checks to ensure that the URL is on the allow list. You can add URLs to the webhook allow list by configuring the `alert_actions.conf` file.
#### Requirements

To configure the webhook allow list, you must have:
+ Splunk Enterprise version 9.0 or higher.
+ The admin role.
+ The `edit_webhook_allow_list` capability. The admin role has this capability by default.

### Add URL endpoints to the webhook allow list

The webhook allow list is located in the `alert_actions.conf` file under the `[webhook]` stanza.

To add a URL to the webhook allow list, you can directly edit the `alert_actions.conf` file as follows:
1. In `$SPLUNK_HOME/etc/system/local`, edit `alert_actions.conf`. If the `alert_actions.conf` file does not exist, you can create it.
2. Under the `[webhook]` stanza, add the webhook URL definition. Each webhook allow list definition must start with the prefix `allowlist.` and be of the form `allowlist.webhook = URL`. For example:

```
[webhook]
allowlist.webhook1 = "https://www.google.com"
allowlist.webhook2 = "https://www.splunk.com"
```

Where "webhook1" and "webhook2" are the names of the webhooks.
3. Set `enable_allowlist` to "true"

For more information on `[webhook]` stanza settings in `alert_actions.conf`, see the `alert_actions.conf.spec` file located in `$SPLUNK_HOME/etc/apps/alert_webhook/README`. 

***Specify URLs using restrictive regular expressions*

Splunk Enterprise does a regular expression match against URLs in the allow list. If there is a string match, then an alert (HTTP POST request) is sent to the specified webhook URL. When adding a URL to the webhook allow list, make sure to define the URL as completely as possible to achieve the most restrictive match.
### Troubleshoot alert failures due to URL no in allow list

Upon upgrade to version 9.1, Splunk Enterprise automatically adds all URLs currently associated with a webhook alert action to the webhook allow list. However, after upgrade to 9.1 or higher, you must manually add any URL associated with a webhook alert action to the webhook allow list, or the alert will fail.

To see which webhook alerts will fail because the webhook URL is missing from the allow list, run the following search:

```SPL
index="_internal" source=*splunkd.log* "did not match an entry" URL=*
| stats values(URL) by sid
```
