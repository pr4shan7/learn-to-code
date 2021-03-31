# Signals
 - A signal is used by a process to communicate to another.
 - It is like a nudge.
 - They are standard i.e, each signal has a specific meaning known to both the sender and receiver.

 ### Signal Masking

 - A process can decide if it responds to a signal or not.
 - It can also decide how exactly it can respond to the signal
 - This is called Signal Masking
 - SIGKILL is the only signal that can not be masked.

 >Fact: Kill command uses SIGKILL. 

 ## Some signals:
 
- SIGINT: interupt
    - used when we press Ctrl + C
- SIGQUIT: request a process to quit
- SIGILL: invalid instruction
- SIGTRAP: used in bash, if script generates error
- SIGFPE: floating point eroor
- SIGALRM: Asking the OS to alarm after a fixed time
- SIGSTOP, SIGCONT: pause and play a process
- SIGCHLD: sent to parent when child dies
- SIGWINCH: when window is resized
- SIGUSR: open ended for custom use


### Experimenting with Signals

```py
import signal
import os
import time


def sig_handler(a,b):
    print("Child died")

signal.signal(signal.SIGCHLD,sig_handler)

pid = os.fork()
if pid > 0:
    time.sleep(1000)
else:
    time.sleep(5)
    exit(0)
```
- We can change the signal in this code to experiment with different types of signals.
- `sig_handler` is the function that executes when the specified signal is received.