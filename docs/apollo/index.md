---
layout: docs
title: Apollo
group: "navigation"
order: "120"
---
# Apollo

ASN.1 Defined Binary Protocol implementing Pundun Framework Procedures.

## Scope
This document specifies the Apollo Protocol between the Pundun - The Soft Real Time Analytics Framework - and the Clients that run database operations on Pundun..
Procedures, Messages, Information elements and the ASN.1 Definitions are described in this document.

## Definitions and Abbreviations

- Client: Any entity that interacts with Pundun through Appolo protocol.

## General
The procedures defined int his document specifies Pundun Framework behaviour during interaction with clients.
## Apollo Procedures

### Connection Procedure

TODO: Define procedure

### Database Operation Procedure

TODO: Define procedure

### Abort

TODO: Define procedure


## Elements for Apollo Communications 

### Message Functional Definition and Content

#### ConnectionRequest

TODO: Define message

#### ConnectionResponse

TODO: Define message

#### CreateTable

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |
| Keys | M | (1..maxNoOfKeyFields) | 5.2 | List of FieldNames that compose the table key. |
| Columns | M | (1..maxNoOfColumns) | 5.2 | List of FieldNames that compose the columns of the table. |
| Indexes | O | (1..maxNoOfIndexes) | 5.2 | List of FieldNames that compose the indexes of the table. |
| TableOptions | M |  | 5.2 | List of TableOption. |

#### OpenTable

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |

#### CloseTable

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |

#### DeleteTable

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |

#### Read

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |
| Key | M |  | 5.2 | The Key to be read from the Table. |

#### Write

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |
| Key | M |  | 5.2 | The Key to be written to the Table. |
| Columns | M |  | 5.2 | The Columns to be written to the Table. |

#### Delete

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |
| Key | M |  | 5.2 | The Key to be deleted from the Table. |

#### RangeRead

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |
| KeyRange | M |  | 5.2 | The KeyRAnge to be read from the Table. |
| Limit | M | | 5.2 | Maximum number of entries to be read from each local shard of the Table. |

#### BatchWrite

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| TableName | M | | 5.2 | String representation of the database table name. |
| DeleteKeys | M |  | 5.2 | The Keys to be deleted from the Table. |
| WriteKVPs | M |  | 5.2 | The KVPs to be written to the Table. |

Note that deletion of specified keys will be performed before writing the specified KVPs.

### Information Element Functional Definition and Content

#### TableOption

| IE Name | Precence | Range | Reference | Description |
|:------- |:--------:|:-----:|:---------:|:-----------:|
| CHOICE TableOption | M | | 5.2 |  |
| > time_ordered |  |  | 5.2 | BOOLEAN |
| > wrapped |  |  | 5.2 | Wrapper |
| > backend |  |  | 5.2 | Backend |

#### KeyDefinition

#### ColumnDefinition

#### IndexDefinition

#### Error


### Message And Information Element Abstract Syntax

Below code block is a copy of APOLLO-PDU-Descriptions.asn1 file.


```
-- **************************************************************
--
-- Apollo PDU Descriptions.
--
-- **************************************************************
APOLLO-PDU-Descriptions {
}

DEFINITIONS AUTOMATIC TAGS ::=

BEGIN

APOLLO-PDU	    ::= SEQUENCE {
    version		INTEGER (0..127),
    transactionId	INTEGER (0..65535),
    procedure		Procedure
}

Procedure	    ::= CHOICE {
    connectionRequest	ConnectionRequest,
    connectionResponse	ConnectionResponse,
    createTable		CreateTable,
    deleteTable		DeleteTable,
    openTable		OpenTable,
    closeTable		CloseTable,
    read		Read,
    write		Write,
    delete		Delete,
    readRange		ReadRange,
    batchWrite		BatchWrite
}

-- **************************************************************
--
-- Apollo Procedure Definitions.
--
-- **************************************************************
BatchWrite	    ::= SEQUENCE {
    tableName		FieldName,
    deleteKeys		SEQUENCE OF Key,
    writeKvps		SEQUENCE OF KeyColumnsPair
}

CloseTable	    ::= SEQUENCE {
    tableName		FieldName
}

ConnectionRequest   ::= SEQUENCE {
    dummy		INTEGER
}

ConnectionResponse  ::= SEQUENCE {
    dummy		INTEGER
}

CreateTable	    ::= SEQUENCE {
    tableName		FieldName,
    keys		SEQUENCE OF FieldName,
    columns		SEQUENCE OF FieldName,
    indexes		SEQUENCE OF FieldName,
    tableOptions	SEQUENCE OF TableOption
}


Delete		    ::= SEQUENCE {
    tableName		FieldName,
    key			Key
}

DeleteTable	    ::= SEQUENCE {
    tableName		FieldName
}

OpenTable	    ::= SEQUENCE {
    tableName		FieldName
}

Read		   ::=	SEQUENCE {
    tableName		FieldName,
    key			Key
}

ReadRange	    ::= SEQUENCE {
    tableName		FieldName,
    keyRange		KeyRange,
    limit		INTEGER
}

Response	    ::= SEQUENCE {
    result		Result,
    moreDataToBeSent	BOOLEAN
}

Result		    ::= SEQUENCE { 
    error		Error OPTIONAL
}

Write		    ::= SEQUENCE {
    tableName		FieldName,
    key			Key,
    columns		Columns
}

-- **************************************************************
--
-- Common IE Definitions.
--
-- **************************************************************

Backend		    ::= ENUMERATED {
    leveldb		(0),
    etsLeveldb		(1)
}

Columns		    ::= SEQUENCE OF Field

DataModel	    ::= ENUMERATED {
    binary		(0),
    array		(1),
    hash		(2)
}

Error		    ::= CHOICE {
    transport		IA5String (SIZE(1..64)),
    protocol		IA5String (SIZE(1..64)),
    system		IA5String (SIZE(1..64)),
    misc		IA5String (SIZE(1..64))
}

Field		    ::= SEQUENCE {
    name		FieldName,
    value		Value
}

-- Limit Fieldname Chars to (a..z)
FieldName	    ::= IA5String (SIZE(1..128))

FileMargin	    ::= INTEGER (1..128)

Key		    ::= SEQUENCE OF Field

KeyRange	    ::= SEQUENCE {
    start		Key,
    end			Key
}

KeyColumnsPair	    ::= SEQUENCE {
    key			Key,
    columns		Columns
}

TableOption	    ::= CHOICE {
    timeOrdered		BOOLEAN,
    wrapped		Wrapper,
    backend		Backend
}

TimeMargin	    ::= INTEGER (0..4294967295)

Value		    ::= OCTET STRING

Wrapper		    ::= SEQUENCE {
    fileMargin		FileMargin,
    timeMargin		TimeMargin
}

maxNumOfKeyFields   INTEGER ::= 16

maxNumOfColumns	    INTEGER ::= 255

maxNumOfIndexes	    INTEGER ::= 8

--ProcedureCode	    ::= INTEGER (0..255)

END


```

## History

### Publication History

| Version | Date       | Note          |
|:------- |:-----------|:--------------|
| 0.1.0     | 2015-05-01 | Not published |

### Change History

| Date       | ChangeID | Comment   | Old Version | New Version |
|:-----------|:---------|:----------|:------------|:------------|
| 2015-05-01 | -        | Dummy Row | v0.1.0      | v0.1.1      |

