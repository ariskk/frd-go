# frd-go

A client for SSE (server-sent events) events sent by Flashbots Relayers which follows the 
[Flashbots Relay API specification](https://flashbots.notion.site/Relay-API-Spec-5fb0819366954962bc02e81cb33840f5#286c858c4ba24e58ada6348d8d4b71ec).

## How does it work ?

Using the [sse package](https://github.com/r3labs/sse) made by r3labs, it connects to the 
provided relayer and subscribe to incoming events: `BidTrace`.

These bids are forwarded (along with an optional error that may have happened during parsing) in a 
channel you can use in your own application.

## Getting started !

### Installation

```shell
# Probably a bash command here
```

### Quickstart

Below is an example of how you can create a client:
```go
package main

import (
	"context"
	"fmt"
	"github.com/0xpanoramix/frd-go/client"
	"log"
)

func main() {
	opts := []client.Option{
		client.WithRelay("http://127.0.0.1:8080"),
		client.WithTopics(client.BuilderBidValid),
		client.WithContext(context.Background()),
	}
	clt, err := client.New(opts...)
	if err != nil {
		log.Fatal(err)
	}

	res, err := clt.Subscribe("messages")

	data := <-res
	// This will print a Flashbots BidTrace.
	fmt.Println(data.Message.EventData)

	clt.Unsubscribe()
}
```

## Author

Made with ❤️ by 🤖 [Luca Georges François](https://github.com/0xpanoramix) 🤖
