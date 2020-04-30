# Coprocesses \(Bash Reference Manual\)

## 3.2.5 Coprocesses

A `coprocess` is a shell command preceded by the `coproc` reserved word. A coprocess is executed asynchronously in a subshell, as if the command had been terminated with the ‘&’ control operator, with a two-way pipe established between the executing shell and the coprocess.

The format for a coprocess is:

```text
coproc [NAME] command [redirections]
```

This creates a coprocess named NAME. If NAME is not supplied, the default name is COPROC. NAME must not be supplied if command is a simple command \(see [Simple Commands](simple-commands-bash-reference-manual.md#Simple-Commands)\); otherwise, it is interpreted as the first word of the simple command.

When the coprocess is executed, the shell creates an array variable \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\) named `NAME` in the context of the executing shell. The standard output of command is connected via a pipe to a file descriptor in the executing shell, and that file descriptor is assigned to `NAME`\[0\]. The standard input of command is connected via a pipe to a file descriptor in the executing shell, and that file descriptor is assigned to `NAME`\[1\]. This pipe is established before any redirections specified by the command \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\). The file descriptors can be utilized as arguments to shell commands and redirections using standard word expansions. Other than those created to execute command and process substitutions, the file descriptors are not available in subshells.

The process ID of the shell spawned to execute the coprocess is available as the value of the variable `NAME`\_PID. The `wait` builtin command may be used to wait for the coprocess to terminate.

Since the coprocess is created as an asynchronous command, the `coproc` command always returns success. The return status of a coprocess is the exit status of command.

