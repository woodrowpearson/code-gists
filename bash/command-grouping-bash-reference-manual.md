# Command Grouping \(Bash Reference Manual\)

## 3.2.4.3 Grouping Commands

Bash provides two ways to group a list of commands to be executed as a unit. When commands are grouped, redirections may be applied to the entire command list. For example, the output of all the commands in the list may be redirected to a single stream.`()`

Placing a list of commands between parentheses causes a subshell environment to be created \(see [Command Execution Environment](command-execution-environment-bash-reference-manual.md#Command-Execution-Environment)\), and each of the commands in list to be executed in that subshell. Since the list is executed in a subshell, variable assignments do not remain in effect after the subshell completes.`{}`

Placing a list of commands between curly braces causes the list to be executed in the current shell context. No subshell is created. The semicolon \(or newline\) following list is required.

In addition to the creation of a subshell, there is a subtle difference between these two constructs due to historical reasons. The braces are `reserved words`, so they must be separated from the list by `blank`s or other shell metacharacters. The parentheses are `operators`, and are recognized as separate tokens by the shell even if they are not separated from the list by whitespace.

The exit status of both of these constructs is the exit status of list.

