# Learning Note
## start and stop the process
### start
```
./cserv start
```
It will fork create a new child process and exit the original process.
Write the child process's `pid` to the config file `cserv.pid`.
### stop
```
./cserv stop
```
It will read the `pid` in config file `cserv.pid`.
Then according to the `pid` send the signal to process for `kill`.
Finally, delete the config file.