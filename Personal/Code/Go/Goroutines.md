---
tags:
  - code
  - go
  - goroutines
  - multithreading
  - concurrency
link: https://www.golangprograms.com/goroutines.html
related: "[[Channels]]"
---
Goroutines can be initialised by using the `go` keyword in front of a function.

```go
sum()    // A normal function call that executes sum synchronously and waits for completing it
go sum() // A goroutine that executes sum asynchronously and doesn't wait for completing it
```

#### Example 1: Use goroutines to get the size of webpages

```go
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
	"time"
)

func responseSize(url string) {
	fmt.Println("Step1: ", url)
	response, err := http.Get(url)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println("Step2: ", url)
	defer response.Body.Close()

	fmt.Println("Step3: ", url)
	body, err := ioutil.ReadAll(response.Body)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("Step4: ", len(body))
}

func main() {
	go responseSize("https://www.golangprograms.com")
	go responseSize("https://coderwall.com")
	go responseSize("https://stackoverflow.com")
	time.Sleep(10 * time.Second) // Used to ensure that main does not exit before the goroutines
}
```

## WaitGroup
WaitGroup is used to wait for the program to finish all goroutines launched from the main function. A counter is used to define how many goroutines it needs to wait for and blocks execution until the counter reaches 0. 

| Method | Description                                 |
| ------ | -------------------------------- |
| `Add`    | Add a counter to the WaitGroup   |
| `Done`   | Decrement the WaitGroup counter |
| `Wait`   | Waits for the counter to reach 0 |

The above code can be changed like so with add, done, wait

```go
package main

import ...

// WaitGroup is used to wait for the program to finish goroutines.
var wg sync.WaitGroup

func responseSize(url string) {
	// Schedule the call to WaitGroup's Done to tell goroutine is completed.
	defer wg.Done()
	...
}

func main() {
	// Add a count of three, one for each goroutine.
	wg.Add(3)
	fmt.Println("Start Goroutines")

	go responseSize("https://www.golangprograms.com")
	go responseSize("https://stackoverflow.com")
	go responseSize("https://coderwall.com")

	// Wait for the goroutines to finish.
	wg.Wait()
	fmt.Println("Terminating Program")
}
```

## Fetch values from goroutines
The easiest way to fetch a value from a goroutine is to use channels. Channels are pipes that connect concurrent goroutines.

```go
package main

import ...

// WaitGroup is used to wait for the program to finish goroutines.
var wg sync.WaitGroup

func responseSize(url string, nums chan int) {
	...
	nums <- len(body)
}

func main() {
	nums := make(chan int) // Declare a unbuffered channel
	wg.Add(1)
	go responseSize("https://www.golangprograms.com", nums)
	fmt.Println(<-nums) // Read the value from unbuffered channel
	wg.Wait()
	close(nums) // Closes the channel
}
```

## Race Conditions and Atomic Functions
Atomic functions provide low-level locking mechanisms for synchronising access to integers and pointers.

```go
package main

import (
	"fmt"
	"runtime"
	"sync"
	"sync/atomic"
)

var (
	counter int32          // counter is a variable incremented by all goroutines.
	wg      sync.WaitGroup // wg is used to wait for the program to finish.
)

func main() {
	wg.Add(3) // Add a count of two, one for each goroutine.

	go increment("Python")
	go increment("Java")
	go increment("Golang")

	wg.Wait() // Wait for the goroutines to finish.
	fmt.Println("Counter:", counter)

}

func increment(name string) {
	defer wg.Done() // Schedule the call to Done to tell main we are done.

	for range name {
		atomic.AddInt32(&counter, 1)
		runtime.Gosched() // Yield the thread and be placed back in queue.
	}
}
```

## Mutex
A mutex is used to create a critical section around code that ensures only one goroutine at a time can execute that code section.

```go
package main

import (
	"fmt"
	"sync"
)

var (
	counter int32          // counter is a variable incremented by all goroutines.
	wg      sync.WaitGroup // wg is used to wait for the program to finish.
	mutex   sync.Mutex     // mutex is used to define a critical section of code.
)

func main() {
	wg.Add(3) // Add a count of two, one for each goroutine.

	go increment("Python")
	go increment("Go Programming Language")
	go increment("Java")

	wg.Wait() // Wait for the goroutines to finish.
	fmt.Println("Counter:", counter)

}

func increment(lang string) {
	defer wg.Done() // Schedule the call to Done to tell main we are done.

	for i := 0; i < 3; i++ {
		mutex.Lock()
		{
			fmt.Println(lang)
			counter++ // Don't need atomic as the variable can only be accessed by one goroutine at a time due to mutex
		}
		mutex.Unlock()
	}
}
```

