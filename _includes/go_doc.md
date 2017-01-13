# pundun
--
    import "github.com/erdemaksu/pundun"


## Usage

```go
const (
	Second      = 0
	Millisecond = 1
	Microsecond = 2
	Nanosecond  = 3
)
```

```go
const (
	Seconds = 0
	Minutes = 1
	Hours   = 2
)
```

```go
const (
	Megabytes = 0
	Gigabytes = 1
)
```

```go
const (
	Result = 0
	Error  = 1
)
```

```go
const (
	Increment = 0
	Overwrite = 1
)
```

```go
const (
	Leveldb           = 0
	MemLeveldb        = 1
	LeveldbWrapped    = 2
	MemLeveldbWrapped = 3
	LeveldbTda        = 4
	MemLeveldbTda     = 5
)
```

```go
const (
	VirtualNodes = 0
	Consistent   = 1
	Uniform      = 2
	Rendezvous   = 3
)
```

```go
const (
	OK = 0
)
```

#### func  CloseTable

```go
func CloseTable(s Session, tableName string) (interface{}, error)
```

#### func  CreateTable

```go
func CreateTable(s Session, tableName string, key []string, options map[string]interface{}) (interface{}, error)
```

#### func  Delete

```go
func Delete(s Session, tableName string, key map[string]interface{}) (interface{}, error)
```

#### func  DeleteTable

```go
func DeleteTable(s Session, tableName string) (interface{}, error)
```

#### func  Disconnect

```go
func Disconnect(s Session)
```

#### func  First

```go
func First(s Session, tableName string) (interface{}, error)
```

#### func  GetTid

```go
func GetTid(s Session) int32
```

#### func  Last

```go
func Last(s Session, tableName string) (interface{}, error)
```

#### func  Next

```go
func Next(s Session, it []byte) (interface{}, error)
```

#### func  OpenTable

```go
func OpenTable(s Session, tableName string) (interface{}, error)
```

#### func  Prev

```go
func Prev(s Session, it []byte) (interface{}, error)
```

#### func  Read

```go
func Read(s Session, tableName string, key map[string]interface{}) (interface{}, error)
```

#### func  ReadRange

```go
func ReadRange(s Session, tableName string, skey, ekey map[string]interface{}, limit int) (interface{}, error)
```

#### func  ReadRangeN

```go
func ReadRangeN(s Session, tableName string, skey map[string]interface{}, n int) (interface{}, error)
```

#### func  Seek

```go
func Seek(s Session, tableName string, key map[string]interface{}) (interface{}, error)
```

#### func  SendMsg

```go
func SendMsg(s Session, data []byte) []byte
```

#### func  TableInfo

```go
func TableInfo(s Session, tableName string, attrs []string) (interface{}, error)
```

#### func  Update

```go
func Update(s Session, tableName string, key map[string]interface{}, upOps []UpdateOperation) (interface{}, error)
```

#### func  Write

```go
func Write(s Session, tableName string, key, columns map[string]interface{}) (interface{}, error)
```

#### type Client

```go
type Client struct {
}
```


#### type Iterator

```go
type Iterator struct {
	Kvp KVP
	It  []byte
}
```


#### type KVL

```go
type KVL struct {
	List         []KVP
	Continuation map[string]interface{}
}
```


#### type KVP

```go
type KVP struct {
	Key     map[string]interface{}
	Columns map[string]interface{}
}
```


#### type Session

```go
type Session struct {
}
```


#### func  Connect

```go
func Connect(host, user, pass string) (Session, error)
```

#### type SizeMargin

```go
type SizeMargin struct {
	Unit  int
	Value int32
}
```


#### type Tda

```go
type Tda struct {
	NumOfBuckets int32
	TimeMargin   TimeMargin
	TsField      string
	Precision    int
}
```


#### type TimeMargin

```go
type TimeMargin struct {
	Unit  int
	Value int32
}
```


#### type UpdateOperation

```go
type UpdateOperation struct {
	Field        string
	Instruction  int
	Value        interface{}
	DefaultValue interface{}
	Treshold     *uint32
	SetValue     *uint32
}
```


#### type Wrapper

```go
type Wrapper struct {
	NumOfBuckets int32
	TimeMargin   TimeMargin
	SizeMargin   SizeMargin
}
```
