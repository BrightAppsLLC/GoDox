### Install (based on Arch Linux)
- `sudo pacman -S go go-tools`
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
