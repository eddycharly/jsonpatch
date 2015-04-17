# jsonpatch
As per http://jsonpatch.com/ JSON Patch is specified in RFC 6902 from the IETF.

```bash
go get github.com/mattbaird/jsonpatch
```

I tried some of the other "jsonpatch" go implementations, but none of them could diff two json documents and 
generate format like jsonpatch.com specifies. For Example:

```json
[
  { "op": "replace", "path": "/baz", "value": "boo" },
  { "op": "add", "path": "/hello", "value": ["world"] },
  { "op": "remove", "path": "/foo"}
]

```
The API is super simple

#example
```go
package main

import (
	"fmt"
	"github.com/mattbaird/jsonpatch"
)

var simpleA = `{"a":100, "b":200, "c":"hello"}`
var simpleB = `{"a":100, "b":200, "c":"goodbye"}`

func main() {
	patch, e := jsonpatch.CreatePatch([]byte(simpleA), []byte(simpleA))
	if e != nil {
		fmt.Printf("Error creating JSON patch:%v", e)
		return
	}
	for _, operation := range patch {
		fmt.Printf("%s\n", operation.Json())
	}
}
```
