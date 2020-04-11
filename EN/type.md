# typeKeyword summary

### type Usage:

* Define structure
* Define the interface
* Type alias
* Type definition
* Type switch

The difference between type definition and type alias:
The difference is that the type definition completely defines a new type,
The type alias is simply an alias for the existing type. (The compiler is replaced with a basic type.)


### Type Common Demo

###### Defining Structures
```
type Demo struct {}

```

###### Define the interface
```
type Demoer interface {}

```

###### Type alias
```
type Demo string

```

###### Type definition
```
type handle func (str string)

```

###### Type Switch
```
func Demo (params ... interface (}) {
   for i, x: = range params {
      switch x. (type) {
      case bool:
         fmt.Printf ("type #% d is bool", i)
      default:
         fmt.Printf ("type is unknow")
      }
   }
}

```

### Type Considerations

###### Type comparison
Remarks:
Refer to Go documentation for type description:
* Named types (simple types), there are type names such as int, int64, float, string, bool. There are also custom named types.
* Unnamed type (complex type), no type name array slice, map, func () {}, interface {}. But ** chan type is == comparable **.
   * Slice memory is not continuous, and the underlying objects are open.
   * The map memory is not continuous, and the underlying objects are stored independently.
   * chan memory is continuous, single object, can be directly compared;
* When comparing two named types, the type names must be the same; when comparing named types with unnamed types, ** the underlying types are the same **.
* The comparison is based on two principles: 1. the underlying basic type of memory; 2. whether the type itself determines the type or the unstable type;

* Null interface value comparison

```
package main

import (
"fmt"
"reflect"
)

type T1 [] string
type T2 [] string

func main () {
foo0: = [] string {}
foo1: = T1 {}
foo2: = T2 {}
fmt.Println (reflect.TypeOf (foo0))
fmt.Println (reflect.TypeOf (foo1))
fmt.Println (reflect.TypeOf (foo2))

// Output:
// [] string
// main.T1
// main.T2

// Compile pass, and vice versa
// foo1 = foo0
// foo0 = foo1

// Compile failed
// Error prompt: cannot use foo2 (type T2) as type T1 in assignment
foo2 = foo0
   foo1 = foo2 // cannot



   // Compiled by: chan
   ch1: = make (chan int)
   ch2: = make (chan int)
   fmt.Println (ch1 == ch2)
    
   // Compile failed: slice
   s1: = [] int {1,2}
   s2: = [] int {2,1}
   fmt.Println (s1 == s2)

   // Compile failed: map
   m1: = make (map [int] int)
   m2: = make (map [int] int)
   fmt.Println (m1 == m2)
}

```


###### Type Comparability

Judgment principle:
Whether the underlying data structure type is stable and consistent

| Type | Description |
|: --- |: ------------------ |
map | downtime error, not comparable |
| Slice ([] T) | Downtime error, not comparable
Channel | Comparable, must be generated by the same make, that is, the same channel will be true, otherwise false |
Array ([capacity] T) | Comparable, compile time knows if two arrays are consistent |
Structure | Comparable, you can compare structure values ​​one by one |
| Functions | Comparable