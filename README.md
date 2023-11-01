# gocache

This library is a fork of [patrickmn/go-cache](https://github.com/patrickmn/go-cache) 
enhanced with the support for Go's new generics feature introduced in Go 1.18. 
Gocache with Generics provides a simple and effective in-memory cache solution 
while leveraging the type safety and other advantages brought by generics.

### Installation

`go get github.com/graydovee/gocache`

### Feature
- Type-safe caching with Go generics.
- Simple API for setting, getting, and deleting values.
- Optional expiration for cached values.

### Requirements

- Go version 1.18 or higher.

### Usage


```go
import (
    "github.com/graydovee/gocache/v3"
    "time"
)

func main() {
    // Create a cache with a default expiration time of 5 minutes, and which
    // purges expired items every 10 minutes
    c := gocache.New[string, int](5*time.Minute, 10*time.Minute)

    // Set the value of the key "foo" to 41, with the default expiration time
    c.Set("foo", 41, gocache.DefaultExpiration)

    // Set the value of the key "baz" to 42, with no expiration time
    // (the item won't be removed until it is re-set, or removed using
    // c.Delete("baz")
    c.Set("baz", 42, gocache.NoExpiration)
	
    // Get a value from the cache
    baz, found := c.Get("baz")
    if found {
        println(baz)
    }
	
    // Add the value of the key "baz" by 1, now the value of "baz" is 44
    gocache.Increment(c, "baz", 2)

    // Subtract the value of the key "baz" by 1, now the value of "baz" is 43
    gocache.Decrement(c, "baz", 1)
	
    // Delete a value from the cache
    c.Delete("baz")
}
```
