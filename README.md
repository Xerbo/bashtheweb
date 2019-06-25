# bashtheweb
A highly configurable webserver written in bash

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