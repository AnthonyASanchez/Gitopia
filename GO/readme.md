# Go for people in a rush!

## Table of Contents
1. [Go! where?](#go-where?)


## Go from where?
What is go, why do we need it and how does it help us accomplish tasks better than other languages?<br/>
Built in 2007 by some smart engineers @ Google, Go (formally known as Golang) is a modern programming language that has great features such as:
- Compiled
- Goroutines
- Type Inference
- Pointer Arithmetic
- Garbage collection
- Method and Operator Overloading 

These will be explained below but first, why? Why did the smart engineers feel the need to create Go!?<br/>
### Why?
We claimed it was a law, that [Moore](https://en.wikipedia.org/wiki/Moore%27s_law) was right and would always be right. But unfortunately Moore's law was not so much as a law as it was a trend. But since the early 2000's hardware has stopped drastically increasing in speed. So, with know where left to turn some people decided to Go! and make a new language. Hoping to increase software efficiency to keep up with the demanding speeds of the 21st century.<br/>
### What makes it better?
In a distributed world we need a distributed minded language. Other languages such as C++, Java, Python were never built for concurrency. They have concurrency as features with multithreading interfaces,etc.. but they did not have concurrency in mind when they built the language. This is where Go's goroutines come in handy (will be explained below).<br/>
### How?
Lets talk a little about concurrency...<br/>
Concurrency is when multiple processes are being executed at the same time. This is not the same as parellelism, parallelism is the simultaneous execution of (possibly related) computations<br/>
One perfect example is Ford's assembly line when they first open in the early 1900's. While some people made the doors, others made the seats, and others made the engine. All these concurrent processes increasing the throughput, the amount of cars the assembly line could make in a given hour.<br/>
Notice, Ford added more workers, more labor but it made the process faster. Meaning More work != More time spent. That may be very simple to you and dumb to even say but in computer science we are always throwing the word efficiency around and here effeciency equates to throughput, the time spent for car to be made.<br/>
#### Goroutines
Like threads they execute things concurrently but they are different, they are much lighter. i.e They take up around 2Kb in comparison to 1 MB that Java uses for threads. They dynamically grow on a stack allowing for thousands even millions of goroutines to be used simultaneously. They are very simple to create in fact in only takes one word `go`, the keyword go will set off a goroutine to execute. Below is an example with a defined function and an anonymous function.
```
package main
import (
    "fmt"
)
//Regular function
func foo() {
    fmt.Println("Make window.")
}

func main() {
  go foo()
  //Anonymous function.
  go func() {
        fmt.Println("Make car door.")
    }()
}
```
This is great! We can now do things at the same time just like the assembly line...but wait a minute, we have these assembly workers (goroutines) working at the same time but how do they hand off task to each other, how does the window maker talk to the door installer (made up job titles). Well in go we use wait groups and channels.<br/>
#### Wait Groups
Wait groups in Go are constructs that allow for synchronization in the language for goroutines. You can think of wait groups as a 'wait room' that all the assembly line workers meet at once they are finished(Only certian amount of people can be in the room at a certian time). Wait groups are created with an amount of goroutines that it will wait for with the Add function, the wait group will 'wait' until all goroutines call Done on the wait group, (effectively each done mimicking a car worker waiting in the 'wait room'). 
```
package main
import (
    "fmt"
    "sync"
)
// Initialize the wait group
var wg sync.WaitGroup
//Regular function
func foo() {
    fmt.Println("Make window.")
    // Signaling, this gorountine is finished.
    wg.Done()
}
func main() {
  wg.Add(2)
  go foo()
  //Anonymous function.
  go func() {
      fmt.Println("Make car door.")
      // Signaling, this gorountine is finished.
      wg.Done()
  }()
  // Wait until goroutines are finished
  wg.Wait()
  fmt.Println("All car parts are ready to be made!")
}
```

#### Channels
Channels are types values that allow goroutines to synchronize and exchange information. Just like the assembly worker would need a time to come together in the assembly line (synchronize) to hand the other the window (exchange information). A channel serves this exact purpose. In the example with the wait groups, although we saw synchronization, we didn't see any exhange of information, the workers did not hand off car parts. In the example below, the car door make, needs the car window from the car window maker(...I know I should be a project manager at Ford...)</br>
```
package main
import (
    "fmt"
    "sync"
)
// Initialize the wait group
var wg sync.WaitGroup
var part_chan = make(chan string)
//Regular function
func foo() {
    fmt.Println("Make window.")
    // Seding the window part through the channel
    part_chan <- "Window part"
    // Signaling, this gorountine is finished.
    wg.Done()
}
func main() {
  wg.Add(2)
  go foo()
  //Anonymous function.
  go func() {
      // Receiving the window part through the channel.
      window_part := <-part_chan
      fmt.Println("Make car door that has ", window_part)
      // Signaling, this gorountine is finished.
      wg.Done()
  }()
  // Wait until goroutines are finished
  wg.Wait()
  fmt.Println("All car parts are ready to be made!")
}
```
And just like magic, the seperate goroutines can talk to each other through channels.
