---
layout: docs
title: Erlang API
group: "navigation"
order: "131"
---

# Module pbpc

## Function Index

| [batch_write/4](#batch_write-4) | Batch Write deletes and writes a batch of keys and values from/to table in one operation. |
| [close_table/2](#close_table-2) | Close a pundun table. |
| [connect/4](#connect-4) | Connect to a pundun host at IP:Port with given Username and Password. |
| [create_table/4](#create_table-4) | Create table on pundun nodes/cluster. |
| [delete/3](#delete-3) | Delete Key from the table TabName. |
| [delete_table/2](#delete_table-2) | Delete table from pundun nodes/cluster. |
| [disconnect/1](#disconnect-1) | Disconnect from pundun host by providing Session handler pid. |
| [first/2](#first-2) | Get first key/value pair from the table TabName. |
| [last/2](#last-2) | Get last key/value pair from the table TabName. |
| [next/2](#next-2) | Get the next Key/Value from table that is specified by iterator reference Ref. |
| [open_table/2](#open_table-2) | Open table a pundun table. |
| [prev/2](#prev-2) | Get the prevoius Key/Value from table that is specified by iterator reference Ref. |
| [read/3](#read-3) | Read Key from the table TabName. |
| [read_range/5](#read_range-5) | Read a Range of Keys from table with name Name and returns max Chunk items from each local shard of the table. |
| [read_range_n/4](#read_range_n-4) | Reads N nuber of Keys from table with name Name starting form StartKey. |
| [seek/3](#seek-3) | Get the sought Key/Value from table that is specified by TabName. |
| [table_info/2](#table_info-2) | Get table information for all attributes. |
| [table_info/3](#table_info-3) | Get table information with desired attributes. |
| [update/4](#update-4) | Update Key according to Op on the table TabName. |
| [write/4](#write-4) | Write Key:Columns to the table TabName. |

## <a name="functions">Function Details</a>

### batch_write/4

```erlang
batch_write(Session::pid(), TabName::string(), DeleteKeys::[key()], WriteKvps::[kvp()]) -> ok | {error, Reason::term()}
```

Batch Write deletes and writes a batch of keys and values from/to table in one operation.

### close_table/2

```erlang
close_table(Session::pid(), TabName::string()) -> ok | {error, Reason::term()}
```


Close a pundun table.

### connect/4

```erlang
connect(IP::string(), Port::pos_integer(), Username::string(), Password::string()) -> {ok, Session::pid()} | {error, Reason::term()}
```

Connect to a pundun host at IP:Port with given Username and Password.

### create_table/4


```erlang
create_table(Session::pid(), TabName::string(), KeyDef::[atom()], Options::[table_option()]) -> ok | {error, Reason::term()}
```


Create table on pundun nodes/cluster.

### delete/3


```erlang
delete(Session::pid(), TabName::string(), Key::[key()]) -> ok | {error, Reason::term()}
```


Delete Key from the table TabName.

### delete_table/2


```erlang
delete_table(Session::pid(), TabName::string()) -> ok | {error, Reason::term()}
```


Delete table from pundun nodes/cluster.

### disconnect/1

```erlang
disconnect(Session::pid()) -> ok
```


Disconnect from pundun host by providing Session handler pid.

### first/2

```erlang
first(Session::pid(), TabName::string()) -> {ok, KVP::[kvp()], Ref::pid()} | {error, Reason::invalid | term()}
```

Get first key/value pair from the table TabName.

### last/2

```erlang
last(Session::pid(), TabName::string()) -> {ok, KVP::[kvp()], Ref::pid()} | {error, Reason::invalid | term()}
```

Get last key/value pair from the table TabName.

### next/2

```erlang
next(Session::pid(), Ref::pid()) -> {ok, KVP::[kvp()]} | {error, Reason::invalid | term()}
```

Get the next Key/Value from table that is specified by iterator reference Ref.

### open_table/2

```erlang
open_table(Session::pid(), TabName::string()) -> ok | {error, Reason::term()}
```

Open table a pundun table.

### prev/2

```erlang
prev(Session::pid(), Ref::pid()) -> {ok, KVP::[kvp()]} | {error, Reason::invalid | term()}
```

Get the prevoius Key/Value from table that is specified by iterator reference Ref.

### read/3

```erlang
read(Session::pid(), TabName::string(), Key::[key()]) -> {ok, [value()]} | {error, Reason::term()}
```

Read Key from the table TabName.

### read_range/5

```erlang
read_range(Session::pid(), TabName::string(), StartKey::key(), EndKey::ey(), Chunk::pos_integer()) -> {ok, [[kvp()]], Cont::complete | key()} | {error, Reason::term()}
```

Read a Range of Keys from table with name Name and returns max Chunk items from each local shard of the table

### read_range_n/4

```erlang
read_range_n(Session::pid(), TabName::string(), StartKey::key(), N::pos_integer()) -> {ok, [kvp()]} | {error, Reason::term()}
```

Reads N nuber of Keys from table with name Name starting form StartKey.

### seek/3

```erlang
seek(Session::pid(), TabName::string(), Key::key()) -> {ok, KVP::[kvp()], Ref::pid()} | {error, Reason::invalid | term()}
```

Get the sought Key/Value from table that is specified by TabName.

### table_info/2

```erlang
table_info(Session::pid(), TabName::string()) -> [{atom(), term()}] | {error, Reason::term()}
```

Get table information for all attributes.

### table_info/3

```erlang
table_info(Session::pid(), TabName::string(), Attributes::[string()]) -> [{atom(), term()}] | {error, Reason::term()}
```

Get table information with desired attributes.

### update/4

```erlang
update(Session::pid(), TabName::string(), Key::[key()], Op::update_op()) -> {ok, [value()]} | {error, Reason::term()}
```

Update Key according to Op on the table TabName.
field_name() :: string().

treshold() :: pos_integer().

setvalue() :: pos_integer().

update_instruction() :: increment \| {increment, treshold(), setvalue()} \| overwrite.

data() :: pos_integer() \| term().

default() :: pos_integer() \| term().

Op :: [{field_name(), update_instruction(), data()} \| {field_name(), update_instruction(), data(), default()}].

### write/4

```erlang
write(Session::pid(), TabName::string(), Key::[key()], Columns::[[column()]]) -> ok | {error, Reason::term()}
```

Write Key:Columns to the table TabName.
