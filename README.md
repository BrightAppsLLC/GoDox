## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Install
- `sudo pacman -S go go-tools` for Arch Linux
- `mkdir GoTest`
- `cd GoTest`
- ```export GOPATH=`pwd` ```
- `mkdir src`
- `cd src`
- `mkdir HelloWorld`
- `nano HelloWorld/HelloWorld.go`
    ```go
    package main

    import "fmt"

    func main() {
        fmt.Printf("Hellow World !!\n")
    }
    ```
- `go run HelloWorld/HelloWorld.go` => outputs "Hellow World !!"
- `go install HelloWorld` Install the package into the `$GOPATH/bin` also creates the folder if not existent
- `ls $GOPATH/bin/HelloWorld` => outputs "Hellow World !!"

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) System Packages & Play
- `https://golang.org/pkg`
- `go doc fmt` shows dox on a package
- `go doc fmr Printf` shows dox on a package function
- `https://play.golang.org`

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Types
- Int
    - `int8`, `int16`, `int32`, `int64`
    - `uint8`, `uint16`, `uint32`, `uint64`
    - machine depended types `int`, `uint`, `uintptr`
    - aliases
        - `byte` -> `uint8` used to get ASCII chars
        - `rune` -> `uint32` user to get UNICODE chars
    - no automatic conversion, use `int` for most cases

- Float
    - `float32`, `float64` use `float64` as general purpose
    - `complex64`, `complex128`

- String
    - array of `byte` or `rune`, all arrays in Go are zero based
    - a `""` string can contain special chars like `\n` or `\t`
    - a``` `` ``` string can contain new lines, meaning span multiple lines
    - `"Go"[1]` returns `111` the ASCII code of letter `o`

- Boolean
    - `true`, `false`


## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Variables
- `var greeting string = "Hello World !!"`
- `var age = 35` the type will be infered as int
- `var pi = 3.14` as `float64`
- `var c = 3 + 5i` as `complex128`
- `age := 35` is same as `var age = 35` but can be used inside `func` level not `package` level
- inference uses `int`, `float64`, `complex128`
- `var a, b = 3, 5` and `a, b := 3, 5` are the same thing, it delcares two vars and assigns them values
- `var a, b int8 = 3, 5` delcares two vars of type `int8` and assigns them values

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Functions
```go
func add(a, b int) int {
    return a + b
}
```

```go
func swap1(a, b int) (int, int) {
    return b, a
}

func swap2(a, b int) (x int, y int) {
    x, y = b, a
    return
}

func main() {
    var a, b = 3, 4   // => 3, 4
    a, b = swap1(a, b) // => 4, 3
    a, b = swap2(a, b) // => 3, 4
}
```

```go
func sum(params ...int) int { // variable list of params, this thing has to be at the end of parameters of a function
    var sum = 0
    for _,  v := range params {
        sum += v
    }

    return sum
}

func main() {
    var sumOfAll = sum(1, 2, 3, 4, 5) // => 15
}
```

```go
func main() {
    sum := sum(a, b) int { // Closure
        return a + b
    }

    var s = sum(1, 2)
}
```

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) For / If / Switch
```go
for i:=0; i < 8; i++ {
    ...
}

i := 0
for i < 8 {
    ...
    i++
}

if a == b {
    ...
} else if a > b {
    ...
} else {
    ...
}

var scores = [4]float64{ 1.0, 2.0, 3.0, 4.0}
for score := range scores {
    switch {
        case score > 0:
            ...
        case score < 0:
            ...
        default:
            ...
    }

    // or

    switch score {
        case 1.0, 2.0:
            ...
        case 3.0, 4.0:
            ...
        default:
            ...
    }
}
```

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Array and Slice
- Array - size must be known
```go
var scores = [4]float64{ 1.0, 2.0, 3.0, 4.0 }

var avg = 0.0
for i := range scores {
    avg += scores[i]
}

avg = avg / float64(len(avg))
```

- Slice - aka a reference to an underlying array  
```go
var values = make([]int, 10, 100) // initial length of 10 and capacity 100, if the capacity is depassed it will recalculate

var sum = 0
for i := range values {
    sum += values[i]
}
```
- `var newSlice = append(values, 20)` - append to slice
- `var subSlice = values[2:5]` - slice of a slice
- `var subSliceTillTheEnd = values[2:]`
```go
var simpleDeclaredSlice = []int{1, 3, 4, 5, 6, 7}
simpleDeclaredSlice = append(simpleDeclaredSlice, 8, 9, 10)

var a = []int{ 1, 2, 3 }
var b = []int{ 4, 5, 6 }
var c = append(a, b...)
var d = append(c[3:]...)
var e = append(d[:5]...)
```

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Maps / Dictionary
```go
var digits = map[string]int {
    "zero": 0,
    "one" : 1,
    "two" : 2, // the last comma is needed
}

digits["five"] = 5 // add
delete(digits, "five") // delete


var digit int
var ok bool
if digit, ok = digits["ten"]; ok { // check if a key is in dictionary
    ...
}
// or 
if _, ok = digits["ten"]; ok { // use this to check for key but value not used
    ...
}
```

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Struct
```go

type Rect struct {
    width, height float64
}

func area(rect Rect) float64 {
    return rect.width * rect.height
}

func (r Rect) areaButAsMethod() float64 {
    return r.width * r.height
}


func main() {
    var r1 Rect
    r1.width = 1.0
    r2.width = 1.0

    r2 := new(Rect)
    r2.width = 1.0
    r2.width = 1.0

    a1 = area(r1)
    a2 = area(*r1)
    a3 = r1.areaButAsMethod()
}

```

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Pointers
Same as in C

## ![](https://storage.googleapis.com/material-icons/external-assets/v4/icons/svg/ic_label_outline_black_18px.svg) Interfaces
```go
type Describer interface {
    describe()
}

type Circle struct {
    radius float64
}

type Rect struct {
    width float64
    height float64
}

func (r Circle) describe() {
    fmt.Print("I'm a CIRCLE")
}

func (r Rect) describe() {
    fmt.Print("I'm a RECT")
}

var a = []Describer{ Circle{}, Rect{} }
for _, shape := range a {
    shape.describe()
}
```