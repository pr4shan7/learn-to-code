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

## Teletype Terminal (tty)
> Todo: Read about tty in detail
  - In olden days, the server and terminals were physically distant.
  - Due to this, speed of tranfer was less.
  - A lot of features in Linux are to reduce limitations of that time.
  - Earlier, keyboard took some time to show what we typed.
  - ECHO is used to check what was typed before sending to the  server.
  -stdin, stdout, stderr are tty terminal.
   > Read more about: tcgetattr tcsetattr termios
  
  ### Interesting features of tty
  - `ls -l` shows some text in specific colors.
  - `ls -l > out.txt`: No color is seen in the out.txt file
  - This coloring is a behaviour of tty
  - tty is a protocol, there is certain set of command,they help to print and read according to our need.
  - tty devices and commands help to build cool things
## Daemons
- Daemon runs in the background, takes no terminal, is not connected to screen or keyborad.
- If we list all process, we see that some are connected to terminal and some are not.
- By default, all are given access to 0 1 2 but some process chose not to connect to these.
> If we open two zsh, both have different ttys, means both are given different part of the screen to type.

- We can interact with daemon using kill only
- The ANSI color code helps to play with the tty and color using tty commands.


## Fork in Detail

- Everthing in Linux gets created by Fork
- Forking is basically cloning. Fork will make a copy of the existing process and new pid is assigned to it.

### Process in Memory
  - A process is made up of three logical segments: code, data and Stack
  - Code and data both are stored in RAM in separate segments called code segment and data segment respectively.
  - Eg. `print("Hello")` Here print is the code and the string "Hello" is the data
  - Arguments and return value go on the stack .
  - Hackers use to manipulate arguments by accessing the stack. This is called stack overflow.
  - All the three have attributes for security reasons. code: x, data: w , stack: w.Stack historically has x permission as well
  > dis.dis() can be used to disassociate all the instructions of a statement.
  
py
import os
import time
print("i am alone")


time.sleep(1)

print("I am going to clone myself")
pid = os.fork()

if pid == 0:
    print("I am the child")
else:
    print("I just gave birth to a child")
time.sleep(25) 

### Observations from the above code

- Forking helps to do run process' in parallel
- After calling fork, if block is executed in the child process.The else block is executed in the parent process.

> Important : The child process is the exact copy of the parent and it starts to run from the exact line where the parent was at.

- The copy is a shallow copy. 

### Killing a Child Process

- If we kill the child process directly, it will still be present in the Process table of Linux.

- Linux does not wipe out the child process completly until the parent specifies it by `os.wait()` 
- The child process that are present in the process table even after dying are called Zombie or Defunked process.
- If there are too many zombie processes, the system will crash.