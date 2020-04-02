logs-go-gorm
-----------

Logger fo gorm

## Usage

Initiate new [logger](https://github.com/spacetab-io/logs-go) with filled `logs.Config` and use it to initiate new gorm logger

```go
package main

import (
    "time"
	
    "github.com/jinzhu/gorm"
    "github.com/spacetab-io/logs-go"
    "github.com/spacetab-io/logs-go-gorm"
)

func main() {
	// initiate logs-go
	conf := &logs.Config{
		Level:"warn",
		Debug: true,
		Sentry: &logs.SentryConfig{
			Enable: true,
			DSN: "http://dsn.sentry.com",
		},
	}
	
    l, err := logs.NewLogger(conf)
    if err != nil {
        panic(err)
    }
    
    db, _ := gorm.Open("sqlite3", "./db.sqlite")
    db.SetLogger(gormLogger.NewLogger(l))
    db.LogMode(true)
}
```

## Licence

The software is provided under [MIT Licence](LICENCE).