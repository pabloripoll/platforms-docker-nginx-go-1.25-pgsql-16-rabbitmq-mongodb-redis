# GO 1.25

## Running the app

Once the container is built, it has already installed [Air - Live reload for Go apps](https://github.com/air-verse/air) due to issues on refreshing the app.

because with it, the Go app Supervisor service must be reload on every change.

Not recommended because will run once when the service is started, and NGIX wont show new changes despite further `$ go run main.go`
```bash
[program:go]
command=go run main.go # Will run once
stdout_logfile=/dev/stdout
stdout_logfile_maxbytes=0
stderr_logfile=/dev/stderr
stderr_logfile_maxbytes=0
autorestart=true
startretries=0
```

Recommended
```bash
[program:go]
command=air -c .air.toml
stdout_logfile=/dev/stdout
stdout_logfile_maxbytes=0
stderr_logfile=/dev/stderr
stderr_logfile_maxbytes=0
autorestart=true
startretries=3
```