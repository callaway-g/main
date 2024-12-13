# PortForwarding

## local port forward

``` shell
    # port forwarding
    ssh -N -L <localport>:<remoteXXX.XXX.XXX.XXX>:<remote_port> <踏み台user>@<踏み台XXX.XXX.XXX.XXX.>
```

## dynamic port forward

``` shell
    # dynamic port forwarding
    ssh -fND 127.0.0.1:8080 -i <鍵のパス> <踏み台user>@<踏み台XXX.XXX.XXX.XXX.>
```
