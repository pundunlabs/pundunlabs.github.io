---
layout: default
title: enterdb
group: "navigation"
order: "210"
---
### enterdb Application
EnterDB is a key/value database under development and there is no stable release yet.
It does not support distributed partitioning and replication yet and it not decided to add this support at enterdb application level or on a higher application level.
Currently it can be used as a local store.

enterdb has the traditional erlan/otp application directory structure.

```sh
$ tree
.
├── ebin
├── include
│   └── enterdb.hrl
├── Makefile
├── priv
│   └── enterdb.json
├── src
│   ├── enterdb_app.erl
│   ├── enterdb.app.src
│   ├── enterdb_db.erl
│   ├── enterdb.erl
│   ├── enterdb_ldb_worker.erl
│   ├── enterdb_lib.erl
│   ├── enterdb_server.erl
│   ├── enterdb_simple_sup.erl
│   ├── enterdb_sup.erl
│   └── Makefile
├── test
│   ├── enterdb_test.erl
│   └── Makefile
└── vsn.mk
```

### Configuration of enterdb
>For basics of configuration in Growbeard Framework, see: [gb_conf](/applications/gb_conf) application.

Configuration of enterdb is stored in the json file under priv dir.
Content of enterdb.json:

```json
{
    "app_name": "enterdb",
    "notify_cb" : ["enterdb_server", "notify"],
    "verify_cb" : ["enterdb_server", "verify"],
    "params" : {
        "db_path" : "data/enterdb",
        "num_of_local_shards" : "32"
    }
}
```
#### Configuration Parameters
- db_path ::
    -- type: erlang string()
    -- definition: path to the desired directory where the database files will be stored.
- num_of_local_shards ::
    -- type: erlang pos_integer()
    -- definition: number of local shards that is going to be created for a database. This value is applied to all databases created.

### API

#### Function Index

- close_db/1:	Close an existing enterdb database.
- create_table/5:	Creates a table that is defined by Name, Key, Columns and optionally Indexes.
- delete/2:	Delete Key from table with name Name.
- delete_db/1:	Delete a database completely.
- open_db/1:	Open an existing enterdb database.
- read/2:	Reads Key from table with name Name.
- read_range/3:	Reads a Range of Keys from table with name Name and returns mac Limit items.
- write/3:	Writes Key/Columns to table with name Name.

#### Type Definitions
```erlang
-type key() :: [{atom(), term()}].
-type key_range() :: {key(), key()}.
-type value() :: term().
-type kvp() :: {key(), value()}.
-type column() :: {atom(), term()}.

-type backend() :: leveldb | ets_leveldb.
-type data_model() :: binary | array | hash.

-type file_margin() :: pos_integer().
-type time_margin() :: pos_integer().
-type wrapper() :: {file_margin(), time_margin()}.

-type table_option() :: [{time_ordered, boolean()} |
                         {wrapped, wrapper()} |
                         {backend, backend()} |
                         {data_model, data_model()}].

-type timestamp() :: {pos_integer(),
                      pos_integer(),
                      pos_integer()}.

```

#### Close Database
```erlang
close_db(Name::string()) -> ok | {error, Reason::term()}
```
Close an existing enterdb database.

#### Create Table
> TODO: Change the function name to create_db!

```erlang
create_table(Name::string(), KeyDef::[atom()], ColumnsDef::[atom()], IndexesDef::[atom()], Options::[table_option()]) -> ok | {error, Reason::term()}

Creates a table that is defined by Name, Key, Columns and optionally Indexes. Key is a list and if list has more than one element, then the key will ba a compound key. Columns list consist of name of each column as atom and inclusion of key columns are optional. Indexes list are optional and an index table will be created for each coulmn provided in this argument. Any given index column is not neccesarly included in Columns.

```

#### Delete 
```erlang
delete(Name::string(), Key::key()) -> ok | {error, Reason::term()}
```
Delete Key from database with name Name.

#### Delete DB
```erlang
delete_db(Name::string()) -> ok | {error, Reason::term()}
```
Delete a database completely. Ensures the database is closed before deletion.

#### Open DB
```erlang
open_db(Name::string()) -> ok | {error, Reason::term()}
```
Open an existing enterdb database.

#### Read
```erlang
read(Name::string(), Key::key()) -> {ok, value()} | {error, Reason::term()}
```
Reads Key from database with name Name.

#### Read Range
```erlang
read_range(Name::string(), Range::key_range(), Limit::pos_integer()) -> {ok, [kvp()]} | {error, Reason::term()}
```
Reads a Range of Keys from database with name Name and returns mac Limit items.
Note that the Limit is the maximum number of consequtive reads from a local shard. If the limit is low, resulting list of entries will be incomplete. 

#### Write
```erlang
write(Name::string(), Key::key(), Columns::[column()]) -> ok | {error, Reason::term()}
```
Writes Key/Columns to database with name Name.


### Example Use
{% raw %}
```erlang
test_db() ->
    Name = "test",
    Keys = [ts, imsi],
    Columns = [value],
    Indexes = [],
    Options = [{backend, leveldb},
               {data_model,binary},
               {time_ordered, true},
               {wrapped, {16, 60}}], 
    enterdb:create_table(Name, Keys, Columns, Indexes, Options).
    
    Ts = now(),
    IMSI = {imsi, "240020000000001"},
    Key = [{ts, Ts}, IMSI],
    {{YYYY, MM, DD}, {HH, Mm, SS}} = calendar:now_to_local_time(Ts),
    ValueData = lists:concat([YYYY,"-",MM,"-",DD," ",HH,":",Mm,":",SS]),
    Value = [{value, ValueData}],
    enterdb:write(Name, Key, Value),
    
    enterdb:read(Name, Key),

    enterdb:delete(Name, Key),

    enterdb:write(Name, [{ts, now()}, IMSI], Value),
    enterdb:write(Name, [{ts, now()}, IMSI], Value),
    enterdb:write(Name, [{ts,now()}, IMSI], Value),
    
    StartKey = Key,
    EndKey =  [{ts, now()}, {imsi, "FFFFFFFFFFFFFFFF"}],
    enterdb:read_range(Name, {StartKey, EndKey}, Limit).

```


#### eDocs
> More and up-to-date documentation can be obtained as generated edoc.

```sh
$enterdb$ make edoc
```
{% endraw %}
