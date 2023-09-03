---
creation date: 2023-08-24 08:55
modification date: Thursday 24th August 2023 08:55:21
---
#splunk 
# About Splunk Enterprise deployments

Splunk Enterprise indexes data from the servers, applications, databases, network devices, and virtual machines. It can collect the data whether it is local, remote or in the cloud.

Splunk Enterprise performs three main functions as it processes data:
- It ingests data from files, the network or other resources.
- It parses and indexes the data.
- It runs searches on the indexed data.
## Types of deployments

Depending on the needs Splunk Enterprise can be deployed as a single instance or create a deployment that spans multiple instances.
### Single Instance deployments

In small deployments, one instance of Splunk Enterprise Handles all aspects of processing data, from input through indexing to search. It can be useful for testing and evaluation purposes and might serve the needs of department-sized environments.
### Distributed deployments

To support larger environments where data originates on many machines, where you need to process large volumes of data, or where many users need to search the data, the deployment can be scaled by distributing Splunk Enterprise instances across multiple machines.

In a typical distributed deployment, each Splunk Enterprise instance performs a specialized task and resides on one of three processing tiers corresponding to the main processing functions:
- Data input tier
- Indexer tier
- Search management tier
### Splunk Enterprise components and processing tiers
This table lists the processing components and the tiers that they occupy. It also describes the functions that each component performs.

| Component   | Tier              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Forwarder   | Data input        | A forwarder consumes data and then forwards the data onwards, usually to an indexer. <br> Forwarders usually require minimal resources, allowing them to reside lightly on the machine generating the data.                                                                                                                                                                                                                                                         |
| Indexer     | Indexing          | An indexer indexes incoming data that it usually receives from a group of forwarders. <br> The indexer transforms the data into events and stores the events in an index. <br> The indexer also searches the indexed data in response to search requests from a search head.<br><br> To ensure high data availability and protect against data loss, or just to simplify the management of multiple indexers, you can deploy multiple indexers in indexer clusters. |
| Search Head | Search management | A search head interacts with users, directs search requests to a set of indexers, and merges the results back to the user.<br> <br> To ensure high availability and simplify horizontal scaling, it can be deployed multiple search heads in search head clusters.                                                                                                                                                                                                  | 

This diagram illustrates the type of deployment that might support the needs of a small enterprise.

![[Pasted image 20230824094207.png]]