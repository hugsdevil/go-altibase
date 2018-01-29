# go-altibase
An Altibase for Go's [database/sql](https://golang.org/pkg/database/sql/) package

---------------------------------------
  * [Features](#features)
  * [Requirements](#requirements)
  * [Installation](#installation)
  * [Usage](#usage)
    * [Example](#example)
  * [License](#license)

---------------------------------------

## Features
  * Connect Altibase using unixODBC

## Requirements
  * unixODBC Driver
  * Altibase ODBC Driver

## Installation
1. Install [unixODBC](http://www.unixodbc.org/)
2. Install go unixODBC package
```bash
go get github.com/alexbrainman/odbc
```
3. Install Altibase ODBC Driver

## Usage
Go Altibase Driver is an implementation of Go's database/sql/driver interface using unixODBC.

```go
import (
    "database/sql"
    _ "github.com/alexbrainman/odbc"
)
    
db, _ := sql.Open("odbc", "driver=driver_name;DSN=ip;CONNTYPE=2;PORT_NO=port;UID=uid;PWD=passwd")
```

### Example
/etc/odbcinst.ini
```bash
[Altibase ODBC 6.1 Driver]
Driver=/altibase/altibase_home/lib/libaltibase_odbc-64bit-ul64.so
SETUP=/altibase/altibase_home/lib/libaltibase_odbc64S.so
UsageCount=1
```

```bash
Driver Name: Altibase ODBC 6.1 Driver
Network:     TCP
IP:          127.0.0.1
Port:        20304
UID:         foo
Password:    bar
```

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/alexbrainman/odbc"
)

func main() {
    // unix socket
    // DSN=%s;CONNTYPE=2;PORT_NO=%s;UID=%s;PWD=%s
    // tcp socket
    // DSN=%s;CONNTYPE=1;PORT_NO=%s;UID=%s;PWD=%s
    db, err := sql.Open("odbc", "driver=Altibase ODBC 6.1 Driver;DSN=127.0.0.1;CONNTYPE=2;PORT_NO=20304;UID=foo;PWD=bar")
    
    if err != nil {
        fmt.Println(err)
        return
    }
    
    defer db.Close()
}
```

## License
BSD 3-Clause "New" or "Revised" License
