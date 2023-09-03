---
creation date: 2023-08-31 13:45
modification date: Thursday 31st August 2023 13:45:50
tag: splunk
---
# Get started with knowledge objects

## Manage knowledge objects through Settings pages

As your organization uses Splunk software, people add **knowledge** to the base set of **event data** indexed within it. You and your colleagues might:
+ Save and schedule **searches**.
+ Add **tags** to fields.
+ Define **event types** and **transactions** that group together sets of events.
+ Create **lookups** and **workflow actions**.

Knowledge managers can use the **Knowledge** pages in **Settings** to control knowledge objects in their Splunk deployment. With **Settings** you can easily:
+ Create knowledge objects when you need to, either from "scratch" or through object cloning.
+ Review knowledge objects as others creates them, in order to reduce redundancy and ensure that people are following naming standards.
+ Delete unwanted or poorly-defined knowledge objects before they develop downstream dependencies.
+ Ensure that knowledge objects worth sharing beyond a particular working group, role, or app are made available to other groups, roles, and users of other apps.

This chapter contains topics that will explain how to:
+ [[#Monitor and organize knowledge objects|Keep your knowledge object collections normalized and orderly]].
+ [[#Develop naming conventions for knowledge objects|Develop naming conventions for your knowledge objects]] that will make them easier to understand and use.
+ [[#Understand and use the Common Information Model Add-on|Use the Common Information Model Add-on to normalize your event data]].
+ [[#Manage knowledge object permissions|Manage your knowledge object permissions]]. Make a knowledge object available to users of a specific app, users with a specific role, or users of all apps ("global" permissions).
+ [[#Disable or delete knowledge objects|Disable or delete knowledge objects]]. Understand the restrictions on deleting knowledge objects, and know the risks of deleting knowledge objects that have downstream dependencies.
### Managing knowledge using configuration files instead of Settings

In previous releases, Splunk Enterprise users edited configuration files directly to add, update, or delete knowledge objects. Now they can use the **Knowledge** pages in Settings, which provide a graphical interface for updating those configuration files.

**Note**: Splunk Cloud users must use the Splunk Web Knowledge pages in Settings to maintain knowledge objects.

Splunk recommends that Splunk Enterprise administrators learn how to modify configuration files. Understanding configuration files is beneficial for the following reasons:
+ Some Splunk Web features make more sense if you understand how things work at the configuration file level. This is specially true for the [[Use the settings pages for field extractions in Splunk web|Field extractions]] and [[#Use the Field transformations page|Field transformations]] pages in Splunk Web.
+ Managing certain knowledge object types requires changes to configuration files.
+ Bulk deletion of obsolete, redundant, or improperly-defined knowledge objects is only possible with configuration files.
## Monitor and organize knowledge objects

As a knowledge manager, you should periodically check up on the knowledge object collections in your Splunk deployment. You should be on the lookout for knowledge objects that:
+ Fail to adhere to naming standards.
+ Are duplicates/redundant.
+ Are worthy of being shared with wider audiences
+ Should be disabled or deleted due to obsolescence or poor design.

Regular inspection of the knowledge objects in your system will help you detect anomalies that could become problems later on.
### Using naming conventions to head off object nomenclature issues

If you set up naming conventions for your knowledge objects early in your Splunk deployment you can avoid some of the thornier object naming issues.
## The sequence of search-time operations

When you run a search, Splunk software runs several operations to derive various knowledge objects and apply them to the events returned by the search. These knowledge objects include extracted fields, calculated fields, lookup fields, field aliases, tags, and event types.

Splunk software perform these operations in a specific sequence. This sequence can cause problems if you configure something at the top of the process order with a definition that references the result of a configuration that is farther down in the process order.

### Search-time operation sequence

The following table presents the search-time operation sequence as a list. Each operation can have configurations that reference fields derived by operations that precede them in the sequence. However, those same configurations cannot contain fields that are derived by operations that follow them in the sequence.

> [!note]
> This list does not include index-time operations, such as default and indexed field extraction. Index-time operations precede all search-time operations.

| Search-time operation order | Operation name                               | Configurable in Splunk Web | Location of file configuratution                                                                                                                                               |
| --------------------------- | -------------------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1                           | Role-based field filtering                   | No                         | `fieldFilter-<fieldname>` in a stanza in the authorize.conf file.                                                                                                              |
| 2                           | Inline field extraction (no field transform) | Yes                        | `Extract-<class>` in a stanza in the props.conf file.                                                                                                                          |
| 3                           | Field extraction that uses a field transform | Yes                        | `REPORT-<class>` in a stanza in the props.conf file.                                                                                                                           |
| 4                           | Automatic key-value field extraction         | No                         | In stanzas in the props.conf file, where `KV_MODE` is set to a valid value other than `none`. If no `KV_MODE` value is specified for a stanza, it is set to `auto` by default. |
| 5                           | Field aliasing                               | Yes                        | `FIELDALIAS-<class>` in a stanza in the props.conf file.                                                                                                                       |
| 6                           | Calculated fields                            | Yes                        | `EVAL-<fieldname>` in a stanza in the props.conf file.                                                                                                                         |
| 7                           | Lookups                                      | Yes                        | `LOOKUP-<class>` in a stanza in the props.conf file.                                                                                                                           |
| 8                           | Event types                                  | Yes                        | In a stanza in the everything.conf file                                                                                                                                        |
| 9                           | Tags                                         | Yes                        | I a stanza in the tags.conf file.                                                                                                                                                                               |

### Role-based field filtering

Role-based field filtering controls the search results that are visible to specific users at search time. You can apply a field filter to a specific role, which then affects the results of searches run by users assigned with that role. Field filters retain the event, but remove or replace specific indexed or default fields and their values at search time when those fields appear in the results. You can remove specific fields and their values by redacting them with a null value. Alternatively, you can redact the value of a specific field by replacing it with a custom string such as xxxx, or you can obfuscate the field value by replacing it with a hash using SHA-256 or SHA-512 (SHA-2 family) hash functions.
#### Splunk Web management

This feature is not supported in Splunk Web.
#### Configure role-based field filtering

To configure role-based field filtering on a role, you must be able to update the settings in a role using one of the following methods:
+ Update the authorize.conf file by adding `fieldFilter-<fieldname> = <option>` to the role.
+ Use a Splunk platform REST API **authorization/roles/{name}** endpoint to update settings for the role. You must hold a role with the edit_field_filter capability, such as the predefined "admin" role, to use the endpoint to configure role-based field filtering.
#### Restrictions

Because role-based field filtering is at the top of the search-time operation sequence, it affects search-time operations that come later for fields that are filtered. This process has particular implications for downstream operations that depende on the value of the field that is changed by a role-based field filter.

The following are operations that can be affected by field-value obfuscation and break existing searches when used with role-based field filtering:

| Operation         | Description                                                                                                                                                                                                                            |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Field extraction  | The field-extracting `regex` expression might depend on field values that are now xxx                                                                                                                                                  |
| Calculated fields | The `eval` expression that calculates the field might break when it gets field values that are now xxx                                                                                                                                 |
| Lookups           | **Lookups** add field-value combinations from lookup tables to **event data** and can break if Splunk software is unable to match field-value combinations in your event data with field-value combinations in external lookup tables. |
| Event types       | The search that defines the event type might be looking to match field values that are now xxx.                                                                                                                                        |
| tag command       | If  the value of a field for a tag's field-value pair is replaced with xxx, the tag is no longer applied.                                                                                                                              | 
### Inline field extractions

Inline field extractions are explicit field extractions that do not include a field transform reference. An explicit field extraction is a field extraction that is configured to extract a specific field or set of fields.

Each inline field extraction configuration is specific to events belonging to a particular host, source, or source type.

This operation does not include automatic key-value field extractions. Automatic key-value field extractions are their own  operation category.
#### Splunk Web management

To create and manage 
## Give knowledge objects of the same type unique names

aa
## Develop naming conventions for knowledge objects

aa
## Understand and use the Common Information Model Add-on

aa
## Manage knowledge object permissions

aa
## Manage orphaned knowledge objects

aa
## Disable or delete knowledge objects

aa
## About Splunk regular expressions

aa