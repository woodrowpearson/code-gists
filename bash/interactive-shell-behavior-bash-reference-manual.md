# Interactive Shell Behavior \(Bash Reference Manual\)

## 6.3.3 Interactive Shell Behavior

When the shell is running interactively, it changes its behavior in several ways.

1.  Startup files are read and executed as described in [Bash Startup Files](bash-startup-files-bash-reference-manual.md#Bash-Startup-Files).
2.  Job Control \(see [Job Control](job-control-bash-reference-manual.md#Job-Control)\) is enabled by default. When job control is in effect, Bash ignores the keyboard-generated job control signals `SIGTTIN`, `SIGTTOU`, and `SIGTSTP`.
3.  Bash expands and displays `PS1` before reading the first line of a command, and expands and displays `PS2` before reading the second and subsequent lines of a multi-line command. Bash expands and displays `PS0` after it reads a command but before executing it. See [Controlling the Prompt](controlling-the-prompt-bash-reference-manual.md#Controlling-the-Prompt), for a complete list of prompt string escape sequences.
4.  Bash executes the value of the `PROMPT_COMMAND` variable as a command before printing the primary prompt, `$PS1` \(see [Bash Variables](bash-variables-bash-reference-manual.md#Bash-Variables)\).
5.  Readline \(see [Command Line Editing](command-line-editing-bash-reference-manual.md#Command-Line-Editing)\) is used to read commands from the user’s terminal.
6.  Bash inspects the value of the `ignoreeof` option to `set -o` instead of exiting immediately when it receives an `EOF` on its standard input when reading a command \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\).
7.  Command history \(see [Bash History Facilities](bash-history-facilities-bash-reference-manual.md#Bash-History-Facilities)\) and history expansion \(see [History Interaction](history-interaction-bash-reference-manual.md#History-Interaction)\) are enabled by default. Bash will save the command history to the file named by `$HISTFILE` when a shell with history enabled exits.
8.  Alias expansion \(see [Aliases](aliases-bash-reference-manual.md#Aliases)\) is performed by default.
9.  In the absence of any traps, Bash ignores `SIGTERM` \(see [Signals](signals-bash-reference-manual.md#Signals)\).
10.  In the absence of any traps, `SIGINT` is caught and handled \(see [Signals](signals-bash-reference-manual.md#Signals)\). `SIGINT` will interrupt some shell builtins.
11.  An interactive login shell sends a `SIGHUP` to all jobs on exit if the `huponexit` shell option has been enabled \(see [Signals](signals-bash-reference-manual.md#Signals)\).
12.  The -n invocation option is ignored, and ‘set -n’ has no effect \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\).
13.  Bash will check for mail periodically, depending on the values of the `MAIL`, `MAILPATH`, and `MAILCHECK` shell variables \(see [Bash Variables](bash-variables-bash-reference-manual.md#Bash-Variables)\).
14.  Expansion errors due to references to unbound shell variables after ‘set -u’ has been enabled will not cause the shell to exit \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\).
15.  The shell will not exit on expansion errors caused by var being unset or null in `${var:?word}` expansions \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
16.  Redirection errors encountered by shell builtins will not cause the shell to exit.
17.  When running in POSIX mode, a special builtin returning an error status will not cause the shell to exit \(see [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode)\).
18.  A failed `exec` will not cause the shell to exit \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).
19.  Parser syntax errors will not cause the shell to exit.
20.  Simple spelling correction for directory arguments to the `cd` builtin is enabled by default \(see the description of the `cdspell` option to the `shopt` builtin in [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\).
21.  The shell will check the value of the `TMOUT` variable and exit if a command is not read within the specified number of seconds after printing `$PS1` \(see [Bash Variables](bash-variables-bash-reference-manual.md#Bash-Variables)\).

