# Processes

## PID

- PID or Process ID is the unique id given to each process
- PID is incremental for new processes and is mostly not reassigned.

> Todo: Why difference in pids for successive command executions not 1?

## Forks

- Forks are system calls which spawn child processes out of parent processes.
- Every process has a parent, except _init_ process which is not born out of fork.
- _init_ (pid = 0) starts _systmed_ (pid = 1) which starts the system

> /proc/pid_of_process/... is a virtual directory which contains information on processes

## Environment

- Environment is a set of variables inherited by a process started by shell.
- Normally the only way to execute a process is through a shell, which provides environment to each process.
  - Environment is by, for and usually used by bash - processes also sometimes use this info.
- `printenv` - prints all the environment variables associated with a shell process
  - `os.getenv(key)` - to get an environment variable in a python process
- `export` - to set environment variables
  - example: `export FLASK_APP=app.py`, here FLASK_APP is the environment variable
- Environment is a channel for providing info to a process or storing info about the environment in which it was launched.
- A bash process shares a copy of its environment variables with its children, while it doesn't share its local variables.
