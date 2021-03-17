# BASH

- BASH or Bourne Again SHell is a command language interpreter.
- It is a program and its executable can be located via `which bash`.

## Script vs Programme

These differences are historical and may not be valid across the board in current times.

- A script is a one way street and control flows in linear fashion.
- Script does not contain functions.
- Scripts are used to accomplish simple tasks.

## directory shortcuts

There are three directory shortcuts available:

1. `.` - denotes current directory
1. `..` - denotes parent of current directory
1. `~` - denotes user home directory

## Variables

- Initialisation: `var=val`
- Accessing stored val: `$var`
- Output capturing from command sequence: `output=$(command)` or output=\`command\`, eg `output=$(ps -e | grep kde)`

## Misc

- `$?` returns the status of last command executed
  - 0 - unsuccessful
  - 1 - successful
- A script to check if a file named _a.txt_ is present in the current directory.

```sh
ls -l | grep a.txt
if [ $? = 0 ]; then
  echo "File exists"
else
  echo "File missing"
fi
```
