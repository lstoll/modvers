# modvers

Tester for Go module loading/version handling, for a propsed twirp modularization.

A straight go get will fetch the v1.0.0 module over the v8.0.0 non-module code:

```
$ go get github.com/lstoll/modvers
go: downloading github.com/lstoll/modvers v1.0.0
go: added github.com/lstoll/modvers v1.0.0
```

go get for v9 works as expected, and includes the v1 release as well:

```
$ go get github.com/lstoll/modvers/v9
go: downloading github.com/lstoll/modvers/v9 v9.0.0
go: added github.com/lstoll/modvers v1.0.0
go: added github.com/lstoll/modvers/v9 v9.0.0
```

Explicitly getting the v8.0.0 tag gets the non-module/incompatible version:

```
$ go get github.com/lstoll/modvers@v8.0.0
go: added github.com/lstoll/modvers v8.0.0+incompatible
```

Getting the v9 module after this leaves it on the incompatible tag, which is still compilable code:

```
$ go get github.com/lstoll/modvers/v9
go: added github.com/lstoll/modvers/v9 v9.0.0
$ cat go.mod
module github.com/lstoll/modvers-test

go 1.27.2

require (
        github.com/lstoll/modvers v8.0.0+incompatible // indirect
        github.com/lstoll/modvers/v9 v9.0.0 // indirect
)
```
