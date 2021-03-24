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
  - 0 - successful
  - 1 - unsuccessful
- A script to check if a file named _a.txt_ is present in the current directory.

```sh
ls -l | grep a.txt
if [ $? = 0 ]; then
  echo "File exists"
else
  echo "File missing"
fi
```

> Todo: Write a script to find if a process with the given pid is running.

- `$@` gives a list of all the arguments passed to the script / command
- `$$` gives the pid of the immidiate process using it
- `rm *` - a new bash process first parses * and then sends the list generated to rm

## Operators

- `|` - pipe operator - used to route output from a command as input to another command
  - example: `ps -e | grep kde`
- `< >` - angle brackets
  - `>` - route standard output to a file and overwrite it, example: `echo "hello" > hello.txt`
  - `>>` - similar but appends instead of overwriting
  - `<` - redirects standard input from file
  - `<<` - used to give input without creating a file

    ```sh
    # END can be any string, used for signalling end of text input
    grep $1 << END
    username=username
    password=password
    END
    ```

  - `<<<` - simpler version of above, but cannot add new lines
    - `grep first <<< "this is a line"`

## Custom command overwrite / implementation

- We can overwrite pre-existing commands or implement our new custom commands.

```sh
# in .bashrc so that custom commands persist across bash instances

# custom rm (moves file to trash)
rm() { # safe rm
  mv $@ ~/.local/share/Trash/files/
}

# rm binary absolute location from "which rm"
del() { # rm
  /usr/bin/rm $@
}
```

---

Note: `""` and `''` are different

- bash doesn't parse anything in single quotes, while it still parses some special symbols in double quotes
- e.g. `echo "$var"` prints `val` of var, while `echo '$var'` simply prints `$var`
