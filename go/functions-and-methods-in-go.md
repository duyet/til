# Functions and Methods in Go?

The term "method" came up with object-oriented programming. In an OOP language (like C++ for example) you can define a "class" which encapsulates data and functions which belong together. Those functions inside a class are called "methods" and you need an instance of that class to call such a method.

```go
type MyInteger int
func (a MyInteger) MyMethod(b int) int {
  return a + b
}
// Usage:
// var x MyInteger = 1
// x.MyMethod(2)
```

Ref: [https://stackoverflow.com/a/8263702](https://stackoverflow.com/a/8263702) 

\------

[There](https://golang.org/doc/faq#methods_on_values_or_pointers) are two ways of defining them. If you want to modify the receiver use a pointer like:

```go
func (s *MyStruct) pointerMethod() { } // method on pointer
```

If you dont need to modify the receiver you can define the receiver as a value like:

```go
func (s MyStruct)  valueMethod()   { } // method on value
```

Ref: [https://stackoverflow.com/a/34350336](https://stackoverflow.com/a/34350336) 
