# go-amber - API Client for Amber Electric

A minimal API client for [Amber Electric](https://www.amber.com.au/). The API is documented at [https://app.amber.com.au/developers/](https://app.amber.com.au/developers/).

## Usage

```go
package main

import (
  "fmt"
  "log"
  "os"

  "github.com/yob/go-amber"
)

func main() {
	client := amber.NewClient(os.GetEnv("AMBER_TOKEN"))

	ctx := context.Background()
	sites, err := client.GetSites(ctx)
	if err != nil {
		log.Fatal(fmt.Sprintf("error fetching sites - %v", err))
	}

	if len(sites) != 1 {
		log.Fatal(fmt.Sprintf("found %d sites, need 1", len(sites)))
		return
	}
	site := sites[0]

	prices, err := client.GetCurrentPrices(ctx, site)

	if err != nil {
		log.Fatal(fmt.Sprintf("error fetching prices - %v", err))
	}

	for _, price := range prices {
    fmt.Printf("%+v\n", price)
  }
}
```
