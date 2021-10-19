# tikvstore

[![Go](https://github.com/ryicoh/tikvstore/actions/workflows/go.yml/badge.svg)](https://github.com/ryicoh/tikvstore/actions/workflows/go.yml)


A session store backend for [gorilla/sessions](http://www.gorillatoolkit.org/pkg/sessions) - [src](https://github.com/gorilla/sessions).

## Installation

    go get github.com/ryicoh/tikvstore

## Documentation

See http://www.gorillatoolkit.org/pkg/sessions for full documentation on underlying interface.

### Example
``` go
package main

import (
	"github.com/ryicoh/tikvstore"
)
func main() {
	ctx := context.TODO()
	cli, err := rawkv.NewClient(ctx, []string{endpoint}, config.DefaultConfig().Security)
	if err != nil {
		panic(err)
	}
	defer cli.Close()

	// Fetch new store.
	store, err := tikvstore.NewTiKVStore(client, []byte("secret-key"))
	if err != nil {
		panic(err)
	}

	// Get a session.
	session, err = store.Get(req, "session-key")
	if err != nil {
		log.Error(err.Error())
	}

	// Add a value.
	session.Values["foo"] = "bar"

	// Save.
	if err = sessions.Save(req, rsp); err != nil {
		t.Fatalf("Error saving session: %v", err)
	}

	// Delete session.
	session.Options.MaxAge = -1
	if err = sessions.Save(req, rsp); err != nil {
		t.Fatalf("Error saving session: %v", err)
	}

	// Change session storage configuration for MaxAge = 10 days.
	store.SetMaxAge(10 * 24 * 3600)
}
```
