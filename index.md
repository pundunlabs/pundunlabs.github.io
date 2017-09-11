---
layout: default
title: pundun home
overview: true
---

{% capture column00 %}
# Pundun - Data Management Framework with a Distributed Database
{% endcapture %}

{% capture column10 %}
### Pundun at a glance:
> - Distributed, Wide Column, NoSQL database.
> - Fault tolerance through replication and auto recovery.
> - High throughput, persistent storage.
> - In-built data retention policy management.
> - In-built text analysis and term indexing per table column.
> - Data localization through configurable consistent hashing.
> - Horizontal scalability by adding and removing nodes.

{% endcapture %}

{% capture column11 %}
### Pundun offers solutions where; 
> - data is perishable and needs to be processed on time.
> - fault tolerance is significant and data should be replicated.
> - system should be scalable and data can be partitioned.
> - data within context should be processed together.
> - streaming data should be kept for a configurable amount of time and processed on demand.
> - column data with text or terms needs to be analyzed and indexed in close to real-time manner.

{% endcapture %}

{% capture column20 %}
#### Pundun is an open source framework project developed in Erlang Programming Language and on OTP. Framework contains a key-value database that is designed suitable for statistical data analysis. Project's purpose is to enable processing high volumes of distributed data streams, thus it can be used to get high throughput in a cost effective way using it's decentralized approach of storing and managing data.
{% endcapture %}


{% capture column30 %}
### Distributed Database Solution

Pundun stores data on a cluster of nodes where data can be partitioned and replicated among the nodes. Pundun nodes communicate with each other using gossip protocol. Data stored in concept of eventual consistency while the consistency level is configurable for read and write operations.

Pundun clusters are dynamic. A node can be removed from or new nodes can be added into a Pundun cluster.


{% endcapture %}

{% capture column31 %}
### Data Localization

Pundun database supports compound keys that consist of multiple data fields. Partitioning of data is based on key values and Pundun optimizes the transferring of data by contextual partitioning. 

Contextual optimization excludes any desired number of fields from compound keys when partitioning the data. By keeping contextually similar data close to each other, data analysis and processing will require less data transfer on network.

{% endcapture %}

{% capture column32 %}
### Inbuilt Data Purge Mechanism

Most of the streaming big data solutions are focused on event, transaction, telemetry or similar data where the value of the data is lost by time and the data eventually parishes.

Pundun offers seamless data purge for old data. A database table can be configured to purge data after a given TTL value (Time To Live).

{% endcapture %}

{% capture column40 %}
### APIs and Security
Database operations can be done on any node by connecting through a client. Pundun implements its own binary protocol (Pundun Binary Protocol) which uses SCRAM Authentication and runs over TLS connections.

Pundun Binary Protocol aka Apollo is defined in protocol buffers format. Client implementations can get use of protobuf compilers. Currently, Erlang (pbpc), Go (pundun) and Javascript (pundunjs) clients exist that implement the Apollo protocol.

{% endcapture %}

{% capture column41 %}
### Indexing and Text Analysis
Pundun has in-built indexing support per column data. A column may store any type of data. To index columns, a table can be configured per it's columns, to define how to analyse and index the column data.

Column data can be analysed as a singular term or as a text. Text can be, Unicode normalized, tokenized, transformed, and filtered according to given configuration. Indexed terms can be analyzed according to occurrence frequencies and their positions in the text.

{% endcapture %}

{% capture column42 %}
### Time Series Support
Applying data localization together with in-built data purge mechanism optimizes management of time series data.

When database keys contain time-stamp values, and input is a continuous data stream, Pundun database tables can be configured to exclude time-stamp values while partitioning, and a desired TTL value can be given to purge perished data.

{% endcapture %}

{% include home_template.html %}
