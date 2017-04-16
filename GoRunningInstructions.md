# Generating Flame Graphs with Go Torch

This is an even simpler process than the C++ instructions.

## Running Go Torch

First have your application running, and if applicable, the part of the application you wish to have running.

Next type the following commands to profile with go-torch:

```
cd $GOPATH/src/github.com/uber/go-torch
go-torch -u http://127.0.0.1:6060/ --seconds 60
firefox torch.svg
```

That's it!


If your program is on a different box or port, change those accordingly. Same goes for how long you want to profile for.

## Sources

[Go-Torch Repository](https://github.com/uber/go-torch)