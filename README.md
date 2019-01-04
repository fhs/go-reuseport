# go-reuseport

[![travisbadge](https://travis-ci.org/libp2p/go-reuseport.svg)](https://travis-ci.org/libp2p/go-reuseport)

This package enables listening and dialing from _the same_ TCP or UDP port.
This means that the following sockopts may be set:

```
SO_REUSEADDR
SO_REUSEPORT
```

- godoc: https://godoc.org/github.com/libp2p/go-reuseport

This is a simple package to help with address reuse. This is particularly
important when attempting to do TCP NAT holepunching, which requires a process
to both Listen and Dial on the same TCP port. This package provides some
utilities around enabling this behaviour on various OS.

## Examples


```Go
// listen on the same port. oh yeah.
l1, _ := reuse.Listen("tcp", "127.0.0.1:1234")
l2, _ := reuse.Listen("tcp", "127.0.0.1:1234")
```

```Go
// dial from the same port. oh yeah.
l1, _ := reuse.Listen("tcp", "127.0.0.1:1234")
l2, _ := reuse.Listen("tcp", "127.0.0.1:1235")
c, _ := reuse.Dial("tcp", "127.0.0.1:1234", "127.0.0.1:1235")
```

**Note: cant dial self because tcp/ip stacks use 4-tuples to identify connections, and doing so would clash.**

## Tested

Tested on `darwin`, `linux`, and `windows`.
