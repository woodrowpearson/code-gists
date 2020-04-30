# Shell Scripts \(Bash Reference Manual\)

## 3.8 Shell Scripts

A shell script is a text file containing shell commands. When such a file is used as the first non-option argument when invoking Bash, and neither the -c nor -s option is supplied \(see [Invoking Bash](invoking-bash-bash-reference-manual.md#Invoking-Bash)\), Bash reads and executes commands from the file, then exits. This mode of operation creates a non-interactive shell. The shell first searches for the file in the current directory, and looks in the directories in `$PATH` if not found there.

When Bash runs a shell script, it sets the special parameter `0` to the name of the file, rather than the name of the shell, and the positional parameters are set to the remaining arguments, if any are given. If no additional arguments are supplied, the positional parameters are unset.

A shell script may be made executable by using the `chmod` command to turn on the execute bit. When Bash finds such a file while searching the `$PATH` for a command, it spawns a subshell to execute it. In other words, executing

is equivalent to executing

if `filename` is an executable shell script. This subshell reinitializes itself, so that the effect is as if a new shell had been invoked to interpret the script, with the exception that the locations of commands remembered by the parent \(see the description of `hash` in [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\) are retained by the child.

Most versions of Unix make this a part of the operating system’s command execution mechanism. If the first line of a script begins with the two characters ‘\#!’, the remainder of the line specifies an interpreter for the program. Thus, you can specify Bash, `awk`, Perl, or some other interpreter and write the rest of the script file in that language.

The arguments to the interpreter consist of a single optional argument following the interpreter name on the first line of the script file, followed by the name of the script file, followed by the rest of the arguments. Bash will perform this action on operating systems that do not handle it themselves. Note that some older versions of Unix limit the interpreter name and argument to a maximum of 32 characters.

Bash scripts often begin with `#! /bin/bash` \(assuming that Bash has been installed in /bin\), since this ensures that Bash will be used to interpret the script, even if it is executed under another shell.

