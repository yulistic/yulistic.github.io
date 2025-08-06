+++
author = "yulistic"
date = "2017-08-10T14:03:23+09:00"
description = "tcp server/client test for linux"
draft = false
tags = ["tcp","netcat", "nc", "network"]
title = "TCP server/client test in linux"
topics = ["linux"]
type = "post"

+++

`netcat` in Ubuntu, `nc` or `ncat` in Fedora, can be used to test a simple tcp(udp) server/client connection.

### Example

In a server side, use following command to listen an incoming connection assuming that the port `3300` is used.

```shell
netcat -l -p 3300
```

A client from another machine can make a connection to the server as below assuming that the ip address of server is `192.168.0.13`.
```shell
netcat 192.168.0.13 3300
```
