# Example Go Install

This package aims to demonstrate how libraries / commands should be organized in a go package.

## Notes

1. The name of your repository will be the command that users type into the command line. Since my repository is named `example-go-install`, when you install it, that's the command you'll call on the command line.
2. If you're testing this out and installing your application multiple times to debug it, make sure you change your `$GOPROXY` environment variable to be `direct`, that will avoid any caching of your projects versions.

   ```sh
   export GOPROXY=direct
   ```

## Structure

```
mylib
  mylib.go
main.go
```

|||
|---|---|
|`mylib/`|One of many possible libraries that your application has packaged with it.|
|`main.go`|The main entry point for executing the program.|

## `main.go`

The `main.go` file should have it's package set to `package main` and it should have a `main()` function. This is what will be called when your program is executed.

If your `main.go` file needs to make use of any of the libraries in your package, you should import them with the fully qualified URL to the github repository including the sub-directory for the library.

`main.go`
```go
package main

import (
    // Import the library we need
    "github.com/nathan-fiscaletti/example-go-install/mylib"
)

func main() {
    mylib.PrintName("nathan")
}
```

## Installing your package

You should tell users to install your binary using `go install`.

When they run `go install`, it will automatically compile your main package for that platform and place it in the `$GOPATH/bin` directory.

```sh
$ go install github.com/nathan-fiscaletti/example-go-install@latest
```

Provided the user installing the program has `$GOPATH/bin` in their `$PATH` environment variable, they can now call `example-go-install` from anywhere.