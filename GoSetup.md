| [Description](README.md) | [Use Cases](UseCases.md)| [Results](Results.md) | Setup | [Run](Run.md) | [Evaluation](Evaluation.md)

# Go Installation Steps

**Disclaimer:** This likely works on operating systems that are not Linux since the profiler is written in Go which is cross platform, but we did not test these instructions with anything besides Linux.

## Install Go

It's safe to assume that if you want to profile a Go application, you probably already have Go and the environment set up; but if not, here are the instructions.

Grab the newest version of Go from the [golang website](https://golang.org/dl/)

Follow the Go website's [instructions to install Go](https://golang.org/doc/install).

Make sure your GOPATH environment variable is set. In Linux in the ~/.bashrc this can be done with the line ```export GOPATH=~/go/```.

## Install Uber's Go Torch

Uber created an application called Go Torch which profiles and creates flame graphs of a Go application.

```go get github.com/uber/go-torch``` will install the application as a Go application

## Add the Flame Graph tool to Go Torch

```
cd $GOPATH/src/github.com/uber/go-torch
git clone --depth=1 https://github.com/brendangregg/FlameGraph.git
```

## Add the Go Profiler to your Application

You have to make a couple modifications to the source to be profiled. These modifications can be made in the main file of your program.

These modifications add Go's pprof profiler to your application which profiles your application according to http requests it receives.

**Add to your imports**

```
import _ "net/http/pprof"
```

**Add somewhere in your main file:**

```
go func() {
	log.Println(http.ListenAndServe("localhost:6060", nil))
}()
```

The port number here can be different from 6060, just remember it for later when you go to launch go-torch

## Sources

[Go-Torch Repository](https://github.com/uber/go-torch)
[Go pprof documenation](https://golang.org/pkg/net/http/pprof/)
