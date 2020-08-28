# go-telegraf

[Doc](https://godoc.org/github.com/mdaffin/go-telegraf)
[Source Repo](https://github.com/mdaffin/go-telegraf)
[License](https://github.com/mdaffin/go-telegraf/blob/master/LICENSE)

A golang library to write metrics to telegraf.

## Installation

```
go get -u "github.com/CumulusCare/go-telegraf"
```

## Example

```
package main

import (
	"log"
	"time"

	"github.com/CumulusCare/go-telegraf"
)

func main() {
	client, err := telegraf.NewTCP("127.0.0.1:8094")
	if err != nil {
		log.Fatal("could not connect:", err)
	}
	defer client.Close()

	m := telegraf.MeasureFloat64("cpu", "load_avg", 0.5)

	if err := client.Write(m); err != nil {
		log.Fatal("failed to write metric:", err)
	}
}
```
