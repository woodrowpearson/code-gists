# The Restricted Shell \(Bash Reference Manual\)

## 6.10 The Restricted Shell

If Bash is started with the name `rbash`, or the --restricted or -r option is supplied at invocation, the shell becomes restricted. A restricted shell is used to set up an environment more controlled than the standard shell. A restricted shell behaves identically to `bash` with the exception that the following are disallowed or not performed:

*  Changing directories with the `cd` builtin.
*  Setting or unsetting the values of the `SHELL`, `PATH`, `ENV`, or `BASH_ENV` variables.
*  Specifying command names containing slashes.
*  Specifying a filename containing a slash as an argument to the `.` builtin command.
*  Specifying a filename containing a slash as an argument to the -p option to the `hash` builtin command.
*  Importing function definitions from the shell environment at startup.
*  Parsing the value of `SHELLOPTS` from the shell environment at startup.
*  Redirecting output using the ‘&gt;’, ‘&gt;\|’, ‘&lt;&gt;’, ‘&gt;&’, ‘&&gt;’, and ‘&gt;&gt;’ redirection operators.
*  Using the `exec` builtin to replace the shell with another command.
*  Adding or deleting builtin commands with the -f and -d options to the `enable` builtin.
*  Using the `enable` builtin command to enable disabled shell builtins.
*  Specifying the -p option to the `command` builtin.
*  Turning off restricted mode with ‘set +r’ or ‘set +o restricted’.

These restrictions are enforced after any startup files are read.

When a command that is found to be a shell script is executed \(see [Shell Scripts](shell-scripts-bash-reference-manual.md#Shell-Scripts)\), `rbash` turns off any restrictions in the shell spawned to execute the script.

The restricted shell mode is only one component of a useful restricted environment. It should be accompanied by setting `PATH` to a value that allows execution of only a few verified commands \(commands that allow shell escapes are particularly vulnerable\), leaving the user in a non-writable directory other than his home directory after login, not allowing the restricted shell to execute shell scripts, and cleaning the environment of variables that cause some commands to modify their behavior \(e.g., `VISUAL` or `PAGER`\).

Modern systems provide more secure ways to implement a restricted environment, such as `jails`, `zones`, or `containers`.

