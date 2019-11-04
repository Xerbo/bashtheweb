# bashtheweb
A highly configurable webserver written in bash

Should you use it for anything apart from a joke? no, you really shouldn't.

# Prerequisites
 - bash (duh)
 - GNU coreutils
 - socat

# Usage
It can be started with:
```
chmod +x bashtheweb
./bashtheweb
```
And will serve the current directory at 0.0.0.0:8080

If you are intrested in more speed you can use shc to compile bashtheweb to a binary.
```
shc -f bashtheweb -o bashtheweb.bin
```
and use `./bashtheweb.bin` instead of `./bashtheweb`.

However you can also use it as a handler with socat/netcat
```
socat TCP4-LISTEN:8080,fork EXEC:"./bashtheweb -z"
netcat -l 8080 -e "./bashtheweb -z" (NOTE: UNTESTED)
```

However bashtheweb normally calls itself recursively to make easier to use, below is a diagram which shows what happens:
```
bashtheweb -r /var/www
 └ socat
    └ bashtheweb -z -r /var/www
```

# Benchmarks

If you are faint of heart, don't look at this part.

These measurements were taken with bombardier (probably some very old version)

```
Statistics        Avg      Stdev        Max
  Reqs/sec       145.29      86.65     449.99
  Latency      811.98ms   476.33ms      4.35s
  HTTP codes:
    1xx - 0, 2xx - 1578, 3xx - 0, 4xx - 0, 5xx - 0
    others - 0
  Throughput:    32.35KB/s
```

nginx (as a reference)

```
Statistics        Avg      Stdev        Max
  Reqs/sec     72225.30    5429.33   90190.49
  Latency        1.73ms     0.85ms    28.95ms
  HTTP codes:
    1xx - 0, 2xx - 722548, 3xx - 0, 4xx - 0, 5xx - 0
    others - 0
  Throughput:    21.77MB/s
```