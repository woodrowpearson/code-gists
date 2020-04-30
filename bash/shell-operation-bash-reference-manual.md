# Shell Operation \(Bash Reference Manual\)

## 3.1.1 Shell Operation

The following is a brief description of the shell’s operation when it reads and executes a command. Basically, the shell does the following:

1.  Reads its input from a file \(see [Shell Scripts](shell-scripts-bash-reference-manual.md#Shell-Scripts)\), from a string supplied as an argument to the -c invocation option \(see [Invoking Bash](invoking-bash-bash-reference-manual.md#Invoking-Bash)\), or from the user’s terminal.
2.  Breaks the input into words and operators, obeying the quoting rules described in [Quoting](quoting-bash-reference-manual.md#Quoting). These tokens are separated by `metacharacters`. Alias expansion is performed by this step \(see [Aliases](aliases-bash-reference-manual.md#Aliases)\).
3.  Parses the tokens into simple and compound commands \(see [Shell Commands](shell-commands-bash-reference-manual.md#Shell-Commands)\).
4.  Performs the various shell expansions \(see [Shell Expansions](shell-expansions-bash-reference-manual.md#Shell-Expansions)\), breaking the expanded tokens into lists of filenames \(see [Filename Expansion](filename-expansion-bash-reference-manual.md#Filename-Expansion)\) and commands and arguments.
5.  Performs any necessary redirections \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\) and removes the redirection operators and their operands from the argument list.
6.  Executes the command \(see [Executing Commands](executing-commands-bash-reference-manual.md#Executing-Commands)\).
7.  Optionally waits for the command to complete and collects its exit status \(see [Exit Status](exit-status-bash-reference-manual.md#Exit-Status)\).

