# Learn GO

### **Introduction to Go**

#### **What is Go? Why Go? How it's Different?**

- **What is Go?**  

Go is a statically typed, compiled language designed for simplicity, efficiency, and scalability.  

- **Why Go?**  
  - Easy to learn.
  - Concurrency support built-in (Goroutines).
  - Strong performance due to its compiled nature.  
- **How it’s Different?**  
  - No classes or inheritance; uses structs and interfaces.
  - Lightweight threads called Goroutines.
  - Minimalistic design philosophy.

### **Local Setup - Install Go & Editor**

1. Download Go from the official website: [https://golang.org/](https://golang.org/).  
2. Install and verify:
   ```bash
   go version
   ```
3. Set up an editor like VS Code and install the Go extension.

### **Write Our First Program**

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

- **Explanation**:
  - `package main`: Entry point of the application.
  - `import "fmt"`: Imports the standard library package for formatted I/O.
  - `main()` function: Program execution starts here.

### **Variables and Constants**

#### **Variables**

```go
package main

import "fmt"

func main() {
    var name string = "Alice"
    age := 30 // shorthand declaration
    fmt.Println("Name:", name, "Age:", age)
}
```

#### **Constants**

```go
package main

import "fmt"

func main() {
    const Pi = 3.14159
    fmt.Println("Value of Pi:", Pi)
}
```

### **Data Types**

```go
package main

import "fmt"

func main() {
    var num int = 10
    var price float64 = 99.99
    var active bool = true
    var message string = "Hello, Go!"
    
    fmt.Printf("Num: %d, Price: %.2f, Active: %t, Message: %s\n", num, price, active, message)
}
```

### **Pointers**

```go
package main

import "fmt"

func main() {
    x := 42
    ptr := &x // Pointer to x
    fmt.Println("Value of x:", x)
    fmt.Println("Address of x:", ptr)
    fmt.Println("Value via pointer:", *ptr) // Dereference
}
```

### **Functions**

#### Basic Functions

```go
package main

import "fmt"

func greet(name string) string {
    return "Hello, " + name
}

func main() {
    message := greet("Alice")
    fmt.Println(message)
}
```

#### Multiple Return Values

```go
package main

import "fmt"

func divide(a, b int) (int, int) {
    return a / b, a % b
}

func main() {
    quotient, remainder := divide(10, 3)
    fmt.Println("Quotient:", quotient, "Remainder:", remainder)
}
```

### **Loops**

#### For Loop

```go
package main

import "fmt"

func main() {
    for i := 0; i < 5; i++ {
        fmt.Println("Count:", i)
    }
}
```

#### Range Loop

```go
package main

import "fmt"

func main() {
    fruits := []string{"Apple", "Banana", "Cherry"}
    for index, fruit := range fruits {
        fmt.Println("Index:", index, "Fruit:", fruit)
    }
}
```

### **Slices**

```go
package main

import "fmt"

func main() {
    numbers := []int{1, 2, 3}
    numbers = append(numbers, 4, 5)
    fmt.Println("Numbers:", numbers)
}
```

### **Maps**

```go
package main

import "fmt"

func main() {
    capitals := map[string]string{"France": "Paris", "Japan": "Tokyo"}
    capitals["India"] = "New Delhi"
    fmt.Println("Capitals:", capitals)
}
```

### **Structs**

```go
package main

import "fmt"

type Person struct {
    Name string
    Age  int
}

func main() {
    person := Person{Name: "Alice", Age: 30}
    fmt.Println("Person:", person)
}
```

### **Interfaces**

```go
package main

import "fmt"

type Animal interface {
    Speak() string
}

type Dog struct{}

func (d Dog) Speak() string {
    return "Woof!"
}

func main() {
    var animal Animal = Dog{}
    fmt.Println("Dog says:", animal.Speak())
}
```

---

### **Concurrency with Goroutines**

```go
package main

import (
    "fmt"
    "time"
)

func printNumbers() {
    for i := 1; i <= 5; i++ {
        fmt.Println(i)
        time.Sleep(1 * time.Second)
    }
}

func main() {
    go printNumbers() // Goroutine
    fmt.Println("Main function")
    time.Sleep(6 * time.Second) // Wait for Goroutine to finish
}
```

### **Channels**

```go
package main

import "fmt"

func main() {
    ch := make(chan string)

    go func() {
        ch <- "Hello from Goroutine"
    }()

    message := <-ch
    fmt.Println(message)
}
```

### **Mutexes**

```go
package main

import (
    "fmt"
    "sync"
)

var counter = 0
var mutex sync.Mutex

func increment(wg *sync.WaitGroup) {
    mutex.Lock()
    counter++
    mutex.Unlock()
    wg.Done()
}

func main() {
    var wg sync.WaitGroup

    for i := 0; i < 10; i++ {
        wg.Add(1)
        go increment(&wg)
    }

    wg.Wait()
    fmt.Println("Final Counter Value:", counter)
}
```

### **Generics**

```go
package main

import "fmt"

func printSlice[T any](s []T) {
    for _, v := range s {
        fmt.Println(v)
    }
}

func main() {
    printSlice([]int{1, 2, 3})
    printSlice([]string{"Go", "Generics"})
}
```
