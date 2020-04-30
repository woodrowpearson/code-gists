# Simple Commands \(Bash Reference Manual\)

## 3.2.1 Simple Commands

A simple command is the kind of command encountered most often. It’s just a sequence of words separated by `blank`s, terminated by one of the shell’s control operators \(see [Definitions](definitions-bash-reference-manual.md#Definitions)\). The first word generally specifies a command to be executed, with the rest of the words being that command’s arguments.

The return status \(see [Exit Status](exit-status-bash-reference-manual.md#Exit-Status)\) of a simple command is its exit status as provided by the POSIX 1003.1 `waitpid` function, or 128+n if the command was terminated by signal n.

