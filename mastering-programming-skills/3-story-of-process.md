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

## File Descriptor / Handle

- It is a token (number) provided by OS when access to a file is requested and is used to access the file.
  - It is always positive
  - It is reserved as long as the file is open
  - It is reassigned when available
- `fd = open('./movies.txt', 'r')` - Here fd is a python file descriptor wrapper created to read _./movies.txt_ file.
  - `fd.fileno()` - Gives the token number or file descriptor given by OS to python for read on _./movies.txt_
    - `os.read(fd.fileno(), bytes_to_read)` - for direct read using fd from OS
    - similarly `os.write(fd.fileno(), b'byte string')`
  - Python's garbage collector automatically closes a file when its `fd` object has no references pointing to it.

> /proc/pid/fd - contains info on every file (descriptor) opened by a process

- There are three file descriptors which are always opened for each process:
  - `0` - _stdin_ - file tied to keyboard
    - used to read from keyboard
    - standard input stream
  - `1` - _stdout_ - file tied to screen
    - used to write to screen
    - standard output stream
  - `2` - _stderr_ - file tied to screen
    - used to write to screen
    - standard error stream
  - These files are not present on the hard disk and are kind of virtual files
  - They can be redirected to and from any other file on disk
    - example: `python3 run.py 0<./file1.txt 1>./file2.txt` - take stdin from file1.txt, print stdout to file2.txt
- Good practice: prompt user before input
