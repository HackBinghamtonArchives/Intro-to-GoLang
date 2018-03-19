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
Here we see some different ways to initialize variables of different types
```go
var  i, j, k int;
var  c, ch byte;
var  f, salary float32;
d =  42;

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
