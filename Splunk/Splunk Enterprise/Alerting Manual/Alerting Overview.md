---
creation date: 2023-08-24 15:23
modification date: Thursday 24th August 2023 15:23:48
tag: splunk
---
# Alerting Overview

## The alerting workflow

Alerts combine a saved search, configurations for type and trigger conditions, and alert actions.
- **Search**: search of the events you want to track. Save the search as an alert.
- **Alert type**: Adjust the type to configure how often the search runs. Scheduled vs real-time.
- **Alert trigger conditions and throttling**: set trigger conditions to manage when an alert triggers, also throttle an alert to control how soon the next alert can trigger after the initial one.
- **Alert action**: when an alert triggers it can initialize one or more actions.

