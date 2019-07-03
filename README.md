# go-altibase
An Altibase for Go's [database/sql](https://golang.org/pkg/database/sql/) package

---------------------------------------
  * [Features](#features)
  * [Requirements](#requirements)
  * [Installation](#installation)
  * [Configuration](#configuration)
  * [Usage](#usage)
    * [Example](#example)
  * [License](#license)

---------------------------------------

## Features
  * Connect Altibase using Altibase ODBC Driver

## Requirements
  * Altibase ODBC Driver

## Installation
1. Install Altibase ODBC Driver
2. Install go Altibase ODBC package
```bash
go get github.com/bsshin71/alticli
```

## Configuration
  * Must be check api/mksyscall_unix.pl, api/api_unix.go files because cgo options (LDFLAGS, CFLAGS)

## Usage
Go Altibase Driver is an implementation of Go's database/sql/driver interface using Altibase ODBC Driver.

```go
import (
    "database/sql"
    _ "github.com/bsshin71/alticli"
)
    
db, _ := sql.Open("alticli", "SERVER=ip;PORT=port;USER=user;PASSWORD=passwd")
```

### Example
```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/bsshin71/alticli"
)

func main() {
    // tcp socket
    // SERVER=%s;PORT=%s;USER=%s;PASSWORD=%s
    db, err := sql.Open("alticli", "SERVER=127.0.0.1;PORT=20300;USER=foo;PASSWORD=bar")
    
    if err != nil {
        fmt.Println(err)
        return
    }
    
    defer db.Close()
}
```

## License
BSD 3-Clause "New" or "Revised" License
