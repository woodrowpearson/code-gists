# The Set Builtin \(Bash Reference Manual\)

If no options or arguments are supplied, `set` displays the names and values of all shell variables and functions, sorted according to the current locale, in a format that may be reused as input for setting or resetting the currently-set variables. Read-only variables cannot be reset. In POSIX mode, only shell variables are listed.

When options are supplied, they set or unset shell attributes. Options, if specified, have the following meanings:`-a`

Each variable or function that is created or modified is given the export attribute and marked for export to the environment of subsequent commands.`-b`

Cause the status of terminated background jobs to be reported immediately, rather than before printing the next primary prompt.`-e`

Exit immediately if a pipeline \(see [Pipelines](pipelines-bash-reference-manual.md#Pipelines)\), which may consist of a single simple command \(see [Simple Commands](simple-commands-bash-reference-manual.md#Simple-Commands)\), a list \(see [Lists](lists-bash-reference-manual.md#Lists)\), or a compound command \(see [Compound Commands](compound-commands-bash-reference-manual.md#Compound-Commands)\) returns a non-zero status. The shell does not exit if the command that fails is part of the command list immediately following a `while` or `until` keyword, part of the test in an `if` statement, part of any command executed in a `&&` or `||` list except the command following the final `&&` or `||`, any command in a pipeline but the last, or if the command’s return status is being inverted with `!`. If a compound command other than a subshell returns a non-zero status because a command failed while -e was being ignored, the shell does not exit. A trap on `ERR`, if set, is executed before the shell exits.

This option applies to the shell environment and each subshell environment separately \(see [Command Execution Environment](command-execution-environment-bash-reference-manual.md#Command-Execution-Environment)\), and may cause subshells to exit before executing all the commands in the subshell.

If a compound command or shell function executes in a context where -e is being ignored, none of the commands executed within the compound command or function body will be affected by the -e setting, even if -e is set and a command returns a failure status. If a compound command or shell function sets -e while executing in a context where -e is ignored, that setting will not have any effect until the compound command or the command containing the function call completes.`-f`

Disable filename expansion \(globbing\).`-h`

Locate and remember \(hash\) commands as they are looked up for execution. This option is enabled by default.`-k`

All arguments in the form of assignment statements are placed in the environment for a command, not just those that precede the command name.`-m`

Job control is enabled \(see [Job Control](job-control-bash-reference-manual.md#Job-Control)\). All processes run in a separate process group. When a background job completes, the shell prints a line containing its exit status.`-n`

Read commands but do not execute them. This may be used to check a script for syntax errors. This option is ignored by interactive shells.`-o option-name`

Set the option corresponding to option-name:`allexport`

Same as `-a`.`braceexpand`

Same as `-B`.`emacs`

Use an `emacs`-style line editing interface \(see [Command Line Editing](command-line-editing-bash-reference-manual.md#Command-Line-Editing)\). This also affects the editing interface used for `read -e`.`errexit`

Same as `-e`.`errtrace`

Same as `-E`.`functrace`

Same as `-T`.`hashall`

Same as `-h`.`histexpand`

Same as `-H`.`history`

Enable command history, as described in [Bash History Facilities](bash-history-facilities-bash-reference-manual.md#Bash-History-Facilities). This option is on by default in interactive shells.`ignoreeof`

An interactive shell will not exit upon reading EOF.`keyword`

Same as `-k`.`monitor`

Same as `-m`.`noclobber`

Same as `-C`.`noexec`

Same as `-n`.`noglob`

Same as `-f`.`nolog`

Currently ignored.`notify`

Same as `-b`.`nounset`

Same as `-u`.`onecmd`

Same as `-t`.`physical`

Same as `-P`.`pipefail`

If set, the return value of a pipeline is the value of the last \(rightmost\) command to exit with a non-zero status, or zero if all commands in the pipeline exit successfully. This option is disabled by default.`posix`

Change the behavior of Bash where the default operation differs from the POSIX standard to match the standard \(see [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode)\). This is intended to make Bash behave as a strict superset of that standard.`privileged`

Same as `-p`.`verbose`

Same as `-v`.`vi`

Use a `vi`-style line editing interface. This also affects the editing interface used for `read -e`.`xtrace`

Same as `-x`.`-p`

Turn on privileged mode. In this mode, the `$BASH_ENV` and `$ENV` files are not processed, shell functions are not inherited from the environment, and the `SHELLOPTS`, `BASHOPTS`, `CDPATH` and `GLOBIGNORE` variables, if they appear in the environment, are ignored. If the shell is started with the effective user \(group\) id not equal to the real user \(group\) id, and the -p option is not supplied, these actions are taken and the effective user id is set to the real user id. If the -p option is supplied at startup, the effective user id is not reset. Turning this option off causes the effective user and group ids to be set to the real user and group ids.`-t`

Exit after reading and executing one command.`-u`

Treat unset variables and parameters other than the special parameters ‘@’ or ‘\*’ as an error when performing parameter expansion. An error message will be written to the standard error, and a non-interactive shell will exit.`-v`

Print shell input lines as they are read.`-x`

Print a trace of simple commands, `for` commands, `case` commands, `select` commands, and arithmetic `for` commands and their arguments or associated word lists after they are expanded and before they are executed. The value of the `PS4` variable is expanded and the resultant value is printed before the command and its expanded arguments.`-B`

The shell will perform brace expansion \(see [Brace Expansion](brace-expansion-bash-reference-manual.md#Brace-Expansion)\). This option is on by default.`-C`

Prevent output redirection using ‘&gt;’, ‘&gt;&’, and ‘&lt;&gt;’ from overwriting existing files.`-E`

If set, any trap on `ERR` is inherited by shell functions, command substitutions, and commands executed in a subshell environment. The `ERR` trap is normally not inherited in such cases.`-H`

Enable ‘!’ style history substitution \(see [History Interaction](history-interaction-bash-reference-manual.md#History-Interaction)\). This option is on by default for interactive shells.`-P`

If set, do not resolve symbolic links when performing commands such as `cd` which change the current directory. The physical directory is used instead. By default, Bash follows the logical chain of directories when performing commands which change the current directory.

For example, if /usr/sys is a symbolic link to /usr/local/sys then:

```text
$ cd /usr/sys; echo $PWD
/usr/sys
$ cd ..; pwd
/usr
```

If `set -P` is on, then:

```text
$ cd /usr/sys; echo $PWD
/usr/local/sys
$ cd ..; pwd
/usr/local
```

`-T`

If set, any trap on `DEBUG` and `RETURN` are inherited by shell functions, command substitutions, and commands executed in a subshell environment. The `DEBUG` and `RETURN` traps are normally not inherited in such cases.`--`

If no arguments follow this option, then the positional parameters are unset. Otherwise, the positional parameters are set to the arguments, even if some of them begin with a ‘-’.`-`

Signal the end of options, cause all remaining arguments to be assigned to the positional parameters. The -x and -v options are turned off. If there are no arguments, the positional parameters remain unchanged.

Using ‘+’ rather than ‘-’ causes these options to be turned off. The options can also be used upon invocation of the shell. The current set of options may be found in `$-`.

The remaining N arguments are positional parameters and are assigned, in order, to `$1`, `$2`, … `$N`. The special parameter `#` is set to N.

The return status is always zero unless an invalid option is supplied.

