---
tags:
  - code
  - go
  - channels
  - multithreading
  - concurrency
link: https://www.golangprograms.com/go-language/what-are-channels-in-golang.html
related: "[[Goroutines]]"
---
Channels can be created using the following syntax

```go
ch := make(chan int)
```

To send value to into the channel the `<-` operator is used. The same operator is used to receive values from the channel

```go
ch <- 42 // send 42 into the channel
x := <-ch // recieve a value from the channel and assign it to x
```
## Buffered Channels
A buffered channel is a type of channel that has a buffer that can store a certain number of values. They are useful when there are multiple producers or consumers, or when the producers and consumers operate at different rates.

A buffered channel is initialised with a capacity i.e. the maximum number of values that can be stored in the buffer. Below is a code snippet that creates a buffered channel with a capacity of 3.

```go
buffered := make(chan int, 3)
```

Once a buffer is full, it will block any further send operations until a value is received from the channel. Once the buffer reaches one value remaining it will block any receive operations until a value is sent to the channel.

```go
ch <- 1
ch <- 2
ch <- 3
ch <- 4 // Blocked as the buffer is full
x := <-ch // x = 1
y := <-ch // y = 2
z := <-ch // Blocked as operation would fully empty buffer
```
#### Example 1: Fibonacci Sequence with buffered channels

```go
package main

import "fmt"

// ch is recieve only, enforced by ch chan<- int
func fib(n int, ch chan<- int) {
    x, y := 0, 1
    for i := 0; i < n; i++ {
        ch <- x 
        x, y = y, x+y
    }
    close(ch) // close channel to prevent indefinite blocking
}

func main() {
    ch := make(chan int, 10) // create a buffered channel with a capacity of 10
    go fib(10, ch) // generate the first 10 Fibonacci numbers in a separate goroutine

    // read values from the channel until it's closed
    for x := range ch {
        fmt.Println(x)
    }
}
```

## Unbuffered Channels
An unbuffered channel has no buffer is used for synchronous communication between goroutines. When a value is sent on an unbuffered channel, the sending goroutine blocks until another goroutine receives the value from the channel. Likewise, when a goroutine attempts to receive a value from an unbuffered channel, it blocks until another goroutine sends a value to the channel.

It ensures synchronize3d communication and reliable transference of data
#### Example 2: Send and receiving with unbuffered channels

```go
package main

import "fmt"

func doSomething(ch chan int) {
    x := 42
    ch <- x // send x on the channel
}

func main() {
    ch := make(chan int) // create an unbuffered channel

    go doSomething(ch) // launch a goroutine to do something with x

    x := <-ch // receive x from the channel
    fmt.Println(x)
}
```
#### Example 3: Fibonacci Sequence with unbuffered channels

```go
package main

import "fmt"

func fib(n int, ch chan<- int) {
    x, y := 0, 1
    for i := 0; i < n; i++ {
        ch <- x
        x, y = y, x+y
    }
}

func main() {
    ch := make(chan int) // create an unbuffered channel
    go fib(10, ch) // generate the first 10 Fibonacci numbers in a separate goroutine

    // read values from the channel until it's closed
    for i := 0; i < 10; i++ {
        x := <-ch
        fmt.Println(x)
    }
}
```

You can check if a buffered channel is full using `len()` to get the current numbers of elements on the channel and `cap()` to get the buffer size.

```go
channel := make(chan int, 10)

// Check if channel is full
if len(channel) == cap(channel) {
    fmt.Println("Channel is full")
}
```
## Closing Channels
1. Only the sender should close the channel: It is important to remember that only the sender should close the channel. Closing a channel indicates that no more values will be sent on the channel, and any attempts to send on the channel will result in a panic
2. Use the range loop to receive values from the channel: The range loop can be used to receive values from the channel until the channel is closed. The loop will automatically terminate when the channel is closed, and any values sent before the channel was closed will be received.
3. Check if the channel is closed before receiving a value: It is possible to check if the channel is closed before receiving a value by using a comma ok idiom. The idiom returns two values, the value received from the channel and a boolean value that is true if the channel is open or false if the channel is closed.
4. Use a select statement to receive values from multiple channels: If you are receiving values from multiple channels, you can use a select statement to receive values until all channels are closed. The select statement will block until a value is received from one of the channels or all channels are closed.
#### Example 4: Closing a channel in Go

```go
func worker(input chan int, output chan int, done chan bool) {
  for {
    select {
	case n := <-input:
	  // Do some work on n
	  output <- n * 2
	case <-done:
	  close(output)
	  return
    }
  }
}

func main() {
  input := make(chan int)
  output := make(chan int)
  done := make(chan bool)

  go worker(input, output, done)

  // Send some values on the input channel
  for i := 0; i < 10; i++ {
    input <- i
  }

  // Close the input channel to signal the end of input
  close(input)

  // Receive values from the output channel
  for n := range output {
    fmt.Println(n)
  }

  // Signal the worker to exit
  done <- true
}
```
#### Example 5: Receive data from multiple channels

```go
func main() {
    ch1 := make(chan int)
    ch2 := make(chan int)

    go func() {
        for i := 0; i < 10; i++ {
            ch1 <- i
        }
        close(ch1)
    }()

    go func() {
        for i := 10; i < 20; i++ {
            ch2 <- i
        }
        close(ch2)
    }()

    for {
        select {
        case x, ok := <-ch1:
            if ok {
                fmt.Println("Received from ch1:", x)
            } else {
                fmt.Println("ch1 closed")
            }
        case x, ok := <-ch2:
            if ok {
                fmt.Println("Received from ch2:", x)
            } else {
                fmt.Println("ch2 closed")
            }
        }
    }
}
```
#### Example 6: Receive data from a closed channel

```go
ch := make(chan int)
go func() {
    ch <- 1
    ch <- 2
    close(ch)
}()

for {
    i, ok := <-ch
    if !ok {
        fmt.Println("Channel closed")
        break
    }
    fmt.Println("Received", i)
}
```


