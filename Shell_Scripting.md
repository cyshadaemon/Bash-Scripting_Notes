# Shell Scripting
## What is a script?
A program written in an interpreted language, typically associated with a shell or a compiled program.

- Plain-text files, created with a text editor
- In Linux, many scripts are written as shell scripts associated with bash or another shell
- use shell scripts to automate tedious, repetitive tasks or to perform new and complex tasks
- perform many of the Linux start up functions

> Note: In the real world, many System Administrators create a bin directory within their ~ to keep their scripts. 

## To Begin a Shell Script
A shell script will begin with a line that identifies the shell used to run it.

- **`#!/bin/bash`**
    
    This will always be the first liine of a script. It indicates that it is a bash shell.
    - the **#!** is a special code that tells Linux that this is a script
    - `/bin/bash` tells which program to run to interpret the script
    - the hash, `#` is a comment character also
        - the script utility will ignore this line throughout the script, even though the kernel does not ignore it.
    - **`/bin/sh`**
        - is a **symbolic link** that points to /bin/bash (on most systems)
            - can be set up to point to a different shell also
        - when you specify the script as using /bin/sh, this will guarantee that any Linux system will have a shell program to run that script

## Make Script Executable

After writing script, the permissions must be modified to become **executable**
- this is done using the `chmod` command
    - To check current permissions, run command:
        `ls -la`
    - To make executable, run command:
        - `chmod 755 <filename.sh>`
        - or, `chmod +x <filename.sh>`
- To run script, run command:
    - `./<filename.sh>`
        - the (`.`) tells the command line to run [`filename.sh`](http://filename.sh) located in the current working directory (`.`) as a program or script. This is the same as typing the full path for example - `/home/rose/filename.sh`
        - This is because the location of the script is not defined in the $PATH variable.

> Note: Simple bash scripts can run in other shells, but more complex scripts may be bash specific. Will not run outside of bash

## Where to store scripts?

It is best to have a central location to run your scripts from. This is for other system administrator to have access to if needed. 

FHS is a specification that exists to clarify the purpose of each of the typical directories that are found on most (or all) of the Linux distributions. https://wiki.linuxfoundation.org/lsb/fhs

This recommends that System Administrators use the `usr/local/bin` directory be used for locally installed programs. 
> Note: This directory is already in the $PATH environment variable.

### Steps: Move Scripts to this Location
**To Move**
```bash
sudo mv script.sh /usr/local/bin/script 
```
<span style="color:red;">WARNING: The mv command has the ability to overwrite existing files without asking. Please review command usage and avoid moving files to the directory with the same file name. </span>


**Modify Ownership**

```bash
sudo chown root:root /usr/local/bin/script
```
This is an important step. If you still own the script, user can possibly modify the script. Change to root so that sudo permissions are needed to run it.

**Add to PATH, if needed**
```bash
export PATH=/usr/local/bin:$PATH
```
This creates a new variable called `PATH` and sets it equal to `/usr/local/bin:$PATH`. This means that the new path will be appended to the already existing paths in the variable.