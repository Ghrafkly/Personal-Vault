---
tags:
  - code
  - go
  - functions
link: https://www.golangprograms.com/go-language/variadic-functions.html
---
Variadic functions allow for any number of same type variables to be passed in using the spread operator `...`

```go
package main

import "fmt"

func main() {
	variadicExample("red", "blue", "green", "yellow")
	multiVariadicExample("Rectangle", 20, 30)
	multiTypeVariadicExample(1, "red", true, 10.5, []string{"foo", "bar", "baz"},
		map[string]int{"apple": 23, "tomato": 13})
}

func variadicExample(s ...string) {
	...
}

func multiVariadicExample(str string, y ...int) int {
	...
}

func variadicExample(i ...interface{}) {
	for _, v := range i {
		fmt.Println(v, "--", reflect.ValueOf(v).Kind())
	}
}
```

