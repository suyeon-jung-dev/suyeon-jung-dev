# go-lang convention list

- 각각 import 하기보다 factored import 문을 사용하라
```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Pi)
}
```
