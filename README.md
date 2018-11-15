# Overview
`jgonize` is a tool to help definition of struct for Golang that store json.

When there is a definition of a structure like the following code,
```
type User struct {
	FirstName string
	LastName  string
	Age       int
}
```

Using `jgonize`,
it is rewritten as follows,
tags are added.

```
type User struct {
	FirstName string `json:"first_name"`
	LastName  string `json:"last_name"`
	Age       int `json:"age"`
}
```

# Install

```
$ go get github.com/shumon84/jgonize
$ go install github.com/shumon84/jgonize
$ jgonize -v
```

# Usage

```
jgonize [-v | -h] [type ...]
```

### Parameters
Specify the following parameters.

`type` - Specify the type name that you want to adding json tag.

### Options

The following options are available.

#### -v, --version
Displays version information and exit.

#### -h, --help
Displays usage information and exit.

# Example

```
$ cat example.go
package example

type User struct {
	FirstName string
	LastName  string
	Age       int
}
$ jgonize User
$ cat example.go
package example

type User struct {
	FirstName string `json:"first_name"`
	LastName  string `json:"last_name"`
	Age       int    `json:"age"`
}
```

It is useful to use `go generate`.

```
$ cat example.go
package example

//go:generate jgonize User
type User struct {
	FirstName string
	LastName  string
	Age       int
}
$ go generate
$ cat example.go
package example

//go:generate jgonize User
type User struct {
	FirstName string `json:"first_name"`
	LastName  string `json:"last_name"`
	Age       int    `json:"age"`
}
```