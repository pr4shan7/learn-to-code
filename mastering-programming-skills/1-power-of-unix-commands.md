# Commands

## 1. ps
Lists the processes running on the computer

#### Useful commandline options:
    -a : list processes of all users as well as the current user
    -c : show the process name without the full path
    -f : show full details about the processes
    -r : sort by CPU usage
    -m : sort by memory usage

#### Tips:
    - use 'ps -e' by default 

#### Hands-on:
    - try listing all processes that belong to the root.
    - try listing all processes that your current bash terminal has started.
    - locate the ps command file.
    - find the forefathers of the ps command you just ran.

## 2. which
Shows the location of the command's executable file

#### Useful commandline options:
    -a : list all instances of the command executable

#### Tips:
    return status of this command can be used to check if a command or
    a tool is installed on the computer or not

#### Hands-on:
    - list out all instances of 'vi' commands are installed on your
      computer
    - find if the git tool is installed on your computer

## 3. grep
Searches file(s) or stdin for given pattern(s)
 
#### Useful commandline options:
    - r : recursively search in files in subdirectories

#### Tips:
    none

#### Hands-on:
    - find all files what have the a word of your choice
    - find count of a given word in a file; a line in the file can have many instances of the given word
      e.g. find how many times the word 'mango' is written in grepfile.txt.
      *** start of grepfile.txt ***
      This manago is better than that mango.
      That mango is not fresh.
      *** end of grepfile.txt ***


## 4. top/htop
Show (sorted) all (or some) the processes running on the computer
 
#### Useful commandline options:
    none

#### Tips:
    Install htop and preferably use it

#### Hands-on:
    - find all processes ending with letter 'd'


## 5. cat
Show the content of file(s)
 
#### Useful commandline options:
    none

#### Tips:
    none

#### Hands-on:
    none


## 6. wc
Count the number of words, characters or lines in the file. If no file is given, it tries reading from the input (called stdin)
 
#### Useful commandline options:
    - c : count the number of characters
    - w : count the number of words
    - l : count the number of lines

#### Tips:
    none

#### Hands-on:
    - make a text file and write something in it in such a way that wc -w returns a non-zero number but wc -l return 0

## 7. watch
Execute a command repeatedly to observe changes

#### Useful commandline options:
    -n value: execute every value seconds

#### Tips:
    - use watch instead of manually executing a command repeatedly

#### Hands-on:
    - find out if the pid of the command executed throug watch is changing

## 8. man
The Google that works without the internet. Shows all the information of the command, along with the options/switches.

#### Useful commandline options:
    -f : displays one-line manual page descriptions

#### Tips:
    - use man instead of google whenever possible

#### Hands-on:
    - skim through man pages for useful and relevant content, don't worry about the complicated stuff
    - try going through the man pages of commands you find interesting

## 9. awk
Chops columns separated by space (default)

#### Useful commandline options:
    -F "string": splits at specified string

#### Tips:
    -

#### Hands-on:
    - get a list of pids of processes currently running

## 10. tail
Shows the end lines of the file.

#### Useful commandline options:
    -n value: shows the last value lines
    -f file: read from file

#### Tips:
    - use tail when you are interested in most recent entries in a large file

#### Hands-on:
    - read last 10 entries from a large file and repeatedly check if there is any update
