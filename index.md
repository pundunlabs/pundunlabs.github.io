---
layout: default
title: pundun home
overview: true
---

{% capture column0 %}
# Pundun - Data Management Framework with a Distributed Database

#### Pundun is an open source framework project developed in Erlang Programming Language and on OTP. Framework contains a key-value database that is designed suitable for statistical data analysis. Project's purpose is to enable processing high volumes of distributed data streams, thus it can be used to get high throughput in a cost effective way using it's de-centrelized approach of storing and managing data.

 Pundun offers solutions where;
 
 - data is perishable and needs to be processed on time.
 - data availability is significant and should be replicated.
 - data is big and should be partioned.
 - data within context should be processed together.

{% endcapture %}

{% capture column1 %}
### Distributed Database Solution


Pundun stores data on a cluster of nodes where data can be partioned and replicated among the nodes. Pundun nodes communicate with each other using gossip protocol. Data stored in concept of eventual consistency while the consistency level is configurable for read and write operations.


Pundun clusters are dynamic. A node can be removed from or new nodes can be added into a pundun cluster.

Database operations can be done on any node by connecting through a client. Pundun implements its own binary protocol (Pundun Binary Protocol) which uses SCRAM Authentication and runs over TLS connections. Pundun Binary Protocol aka Apollo is defined in protocol buffers format. Client implementations can get use of asn1 and protobuf compilers. Currently an erlang client (PBPC) exists that implements the Apollo protocol.

{% endcapture %}

{% capture column2 %}
### Contextual Optimization

Pundun database supports compound keys that consist of multiple data fields. Partiotioning of data is based on key values and Pundun optimizes the movement of data by contextual partitioning. 

One very common example of this is time series data where database keys are compound and contain timestamp values. In such context, Pundun database tables can be configured to exclude timestamp values while partioning, thus it keeps contextually related data close to each other. This approach optimizes the movement of data within a cluster and improves data processing performance.

Contextual optimization is not limited to time series data but it can be used by configuring database tables through excluding any number of fields in compound keys.

Pundun implements iterators and additionally a set of data can be read within a key range or in chunks.

{% endcapture %}

{% capture column3 %}
### Inbuilt Data Purge Mechanism

Most of the streaming big data solutions are focused on event, transaction, telemetry or similar data where the value of the data is lost by time and the data eventually parishes.

Pundun offers seemless data purge for old data. A database table can be configured to purge data after a period of time and/or size of table exceeds some limit.
 
We call these tables wrapping since they actually consist of a number of buckets that wraps by time or size. Purge of data is not done one database entry a time but one bucket at a time. This approach enables faster purge of chunks of parished data.

Partioning and replication of wrapping tables are supported. Wrapping tables use same API as any Pundun table and operations like iteration and reading key ranges are still supported for wrapping tables.

{% endcapture %}

{% include home_template.html %}
