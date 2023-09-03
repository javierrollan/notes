---
creation date: 2023-08-31 13:28
modification date: Thursday 31st August 2023 13:28:08
tag: splunk
---
# Welcome to knowledge management

## What is Splunk Knowledge?

Splunk software provides a powerful search and analysis engine that helps you to see both the details and the larger patterns in your IT data.

The knowledge Manager manual shows you how to maintain sets of knowledge objects for your organization through Splunk Web and configuration files, and it demonstrates ways that you can use Splunk knowledge to solve your organization's real-world problems.

Splunk software knowledge is grouped into five categories:
+ **[[Fields and field extractions|Data integration: Fields and field extractions]]** - Fields and field extractions make up the first order of Splunk software knowledge. The fields that Splunk software automatically extracts from your IT data help bring meaning to your raw data, clarifying what can at first glance seem incomprehensible. The fields that you extract manually expand and improve upon this layer of meaning.
+ **[[Event types|Data classification: Event types and transactions]]** - You use event types and transactions to group together interesting sets of similar events. Event types group together sets of events discovered through searches, while transactions are collections of conceptually-related events that span time.
+ **[[Tags|Data normalization: Tags and aliases]]** - Tags and aliases are used to manage and normalize sets of field information. You can use tags and alisases to group sets of related field values together, and to give extracted fields tags that reflect different aspects of their identity.
+ **[[Build a data model|Data models]]** - Data models are representations of one or more datasets, and they drive the Pivot tool, enabling Pivot users to quickly generate useful tables, complex visualizations, and robust reports without needing to interact with the Splunk software search language. Data models are designed by knowledge managers who fully understand the format and semantics of their indexed data.
## Why manage Splunk Knowledge?

Splunk knowledge managers provide centralized oversight of Splunk Software knowledge. The benefits that knowledge managers can provide include:
+ **Oversight of knowledge object creation and usage across teams, departments, and deployments**. 
+ **Normalization of event data**. 
+ **Management of knowledge objects through configuration files**.
+ **Creation of data models for Pivot users**.
+ **Manage setup and usage of summary-based search and pivot acceleration tools**.
## Prerequisites for knowledge management

Most knowledge management tasks are centered around **search time** event manipulation. In other words, a typical knowledge manager usually don't focus their attention on work that takes place before events are indexed, such as setting up data inputs, adjusting event processing activities, correcting default field extraction issues, creating and maintaining indexes, setting up forwarding and receiving.

Here are some topics that knowledge managers should be familiar with:
+ **Inherit a Splunk Enterprise deployment**.
+ **Working with Splunk apps**.
+ **Configuration file management**.
+ **Indexing incoming data**.
+ **Getting event data into your Splunk deployment**.
+ **Understand your forwarding and receive setup**.
+ **Understand event processing**.
+ **Default field extraction**.
+ **Managing users and roles**.