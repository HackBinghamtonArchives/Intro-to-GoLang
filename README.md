# Intro-to-GoLang
Repository for HackBU Demo on Go

Most of the code in this demo is adopted from 
[https://www.tutorialspoint.com/go/go_overview.htm](https://www.tutorialspoint.com/go/go_overview.htm).

## Motivation
Go programming implementations use a traditional compile and link model to 
generate executable binaries. The Go programming language was announced in 
November 2009 and is used in some of the Google's production systems.

Some of the most important features of Go programming are listed below −
* Support for environment adopting patterns similar to dynamic languages. 
For example, type inference (x := 0 is valid declaration of a variable x 
of type int)
* Compilation time is fast.
* Built-in concurrency support: lightweight processes (via go routines), 
channels, select statement.
* Go programs are simple, concise, and safe.

## Setting Up
To make it easy for everyone to follow along, just head to
[https://repl.it/languages/go](https://repl.it/languages/go) so you can 
code without installing anything.

To install Go on your machine, head to their main website: 
[https://golang.org/dl/](https://golang.org/dl/)

If you'd like help installing Go or setting anything up, feel free to come
up and ask questions after the talk!

## Starting out
I'll be going through some basic code examples to introduce common programming
practices in Go.

### Hello World
```go
package main

import "fmt"

func main() {
	fmt.Println("Hello World")
}
```


### Types


| Type  | Description |
|-------|-------------|
|Boolean|True or False values|
|Numeric|Integers or floating point values|
|String |Immutable sequences of bytes|
|Derived|Pointer types, Array types, Struct types, Function types, etc. |

| Integer Types |
|---------------|
|uint8|
|uint16|
|uint32|
|uint64|
|int8|
|int16|
|int32|
|int64|

| Floating-Point Types |
|----------------------|
|float32|
|float64|
|complex64|
|complex128|

|Other Numeric Types|
|-------------------|
|byte|same as uint8|
|rune|same as int32|
|uint|32 or 64bit depending on system|
|int|32 or 64bit depending on systme|
|uintptr|special type to consider pointer as a uint for easier arithmetic|

Here we see some different ways to initialize variables of different types
```go
// Note that unused variables will throw an error in Go
var  i, j, k int;
var  c, ch byte;
var  f, salary float32;
var number int = 5
var name string = "Ryan"
inferred_number := 7 // note the :=
// := refers to declaration and assignment, where type can be inferred
// The following two lines of code are equivalent
var d int = 42
inferred_d := 42 // however just inferred_d=42 would throw an error

```
Additionally you can also get the type of a variable with %T format specifier

```go
package main

import "fmt"

func main() {
	var x float64
	x = 20.0
	fmt.Println(x)
	fmt.Printf("x is of type %T\n", x)
}
```

#### Constants

```
package main

import "fmt"

func main() {
	const LENGTH int = 10
	const WIDTH int = 5   
	var area int

	area = LENGTH * WIDTH
	fmt.Printf("value of area : %d", area)   
}
```

#### Channels and Go-Routines
Go has a type called "Channel" which are pipes that connect concurrent
Go routines (like threads). You can send values into a channel from one routine
and receive that value from the channel in another routine with the channel
operator `<-`.

**By default, sends and receives block until the other side is ready. This 
allows goroutines to synchronize without explicit locks or condition 
variables.** - Part of why Go is cool!

```go
package main

import "fmt"

func sum(s []int, c chan int) {
	sum := 0
	for _, v := range s {
		sum += v
	}
	c <- sum // send sum to c
}

func main() {
	s := []int{7, 2, 8, -9, 4, 0}

	c := make(chan int)
	go sum(s[:len(s)/2], c) // One routine sum up first half
	go sum(s[len(s)/2:], c) // Second routine sum up second half
	x, y := <-c, <-c // receive from c

	fmt.Println(x, y, x+y)
}
```

### Operators
#### Arithmetic Operators
|Operator|Description|
|--------|-----------|
|+|Adds two operands|
|-|Subtracts second operand from first operand|
|\*|Multiplies operands together|
|/|Divides first operand by second operand|
|%|Modulus operator - gives remainder of division|
|++|Increments value by 1|
|--|Decrements value by 1|

#### Relational Operators

|Operator|
|--------|
|==|
|<=|
|>=|
|<|
|>|
|!=|
|--|

#### Logical Operators

|Operator|Description|
|--------|-----------|
|&&|AND|
|\|\||OR|
|!|NOT|


#### Others

Find documentation on all operators here:
[https://www.tutorialspoint.com/go/go_operators.htm](https://www.tutorialspoint.com/go/go_operators.htm)

### Decision Making
![](https://www.tutorialspoint.com/go/images/decision_making.jpg)

#### If Statement
```go
package main

import "fmt"

func main() {
  /* local variable definition */
  var a int = 10

    /* check the boolean condition using if statement */
    if( a < 20 ) {
        /* if condition is true then print the following */
        fmt.Printf("a is less than 20\n" )
    }
    fmt.Printf("value of a is : %d\n", a)
}
```
#### If...Else Statement
```go
package main

import "fmt"

func main() {
	/* local variable definition */
	var a int = 100;

	/* check the boolean condition */
	if( a < 20 ) {
		/* if condition is true then print the following */
		fmt.Printf("a is less than 20\n" );
	} else {
		/* if condition is false then print the following */
		fmt.Printf("a is not less than 20\n" );
	}
	fmt.Printf("value of a is : %d\n", a);
}
```
#### Nested If Statement
```go
package main

import "fmt"

func main() {
	/* local variable definition */
	var a int = 100
		var b int = 200

		/* check the boolean condition */
		if( a == 100 ) {
			/* if condition is true then check the following */
			if( b == 200 )  {
				/* if condition is true then print the following */
				fmt.Printf("Value of a is 100 and b is 200\n" );
			}
		}
	fmt.Printf("Exact value of a is : %d\n", a );
	fmt.Printf("Exact value of b is : %d\n", b );
}
```
#### Switch Statement
```go
package main

import "fmt"

func main() {
	/* local variable definition */
	var grade string = "B"
		var marks int = 90

		switch marks {
			case 90: grade = "A"
			case 80: grade = "B"
			case 50,60,70 : grade = "C"
			default: grade = "D"  
		}
	switch {
		case grade == "A" :
			fmt.Printf("Excellent!\n" )     
		case grade == "B", grade == "C" :
				fmt.Printf("Well done\n" )      
		case grade == "D" :
					fmt.Printf("You passed\n" )      
		case grade == "F":
						fmt.Printf("Better try again\n" )
		default:
							fmt.Printf("Invalid grade\n" );
	}
	fmt.Printf("Your grade is  %s\n", grade );      
}
```
#### Select Statement


A select statement is like a switch statement but specifically for channels.


```go
select {
	case communication clause  :
		statement(s);      
	case communication clause  :
		statement(s); 
		/* you can have any number of case statements */
	default : /* Optional */
		statement(s);
}
```
