# Bourne Shell Builtins \(Bash Reference Manual\)

The following shell builtin commands are inherited from the Bourne Shell. These commands are implemented as specified by the POSIX standard.`: (a colon)`

Do nothing beyond expanding arguments and performing redirections. The return status is zero.`. (a period)`

Read and execute commands from the filename argument in the current shell context. If filename does not contain a slash, the `PATH` variable is used to find filename. When Bash is not in POSIX mode, the current directory is searched if filename is not found in `$PATH`. If any arguments are supplied, they become the positional parameters when filename is executed. Otherwise the positional parameters are unchanged. If the -T option is enabled, `source` inherits any trap on `DEBUG`; if it is not, any `DEBUG` trap string is saved and restored around the call to `source`, and `source` unsets the `DEBUG` trap while it executes. If -T is not set, and the sourced file changes the `DEBUG` trap, the new value is retained when `source` completes. The return status is the exit status of the last command executed, or zero if no commands are executed. If filename is not found, or cannot be read, the return status is non-zero. This builtin is equivalent to `source`.`break`

Exit from a `for`, `while`, `until`, or `select` loop. If n is supplied, the nth enclosing loop is exited. n must be greater than or equal to 1. The return status is zero unless n is not greater than or equal to 1.`cd`

```text
cd [-L|[-P [-e]] [-@] [directory]
```

Change the current working directory to directory. If directory is not supplied, the value of the `HOME` shell variable is used. Any additional arguments following directory are ignored. If the shell variable `CDPATH` exists, it is used as a search path: each directory name in `CDPATH` is searched for directory, with alternative directory names in `CDPATH` separated by a colon \(‘:’\). If directory begins with a slash, `CDPATH` is not used.

The -P option means to not follow symbolic links: symbolic links are resolved while `cd` is traversing directory and before processing an instance of ‘..’ in directory.

By default, or when the -L option is supplied, symbolic links in directory are resolved after `cd` processes an instance of ‘..’ in directory.

If ‘..’ appears in directory, it is processed by removing the immediately preceding pathname component, back to a slash or the beginning of directory.

If the -e option is supplied with -P and the current working directory cannot be successfully determined after a successful directory change, `cd` will return an unsuccessful status.

On systems that support it, the -@ option presents the extended attributes associated with a file as a directory.

If directory is ‘-’, it is converted to `$OLDPWD` before the directory change is attempted.

If a non-empty directory name from `CDPATH` is used, or if ‘-’ is the first argument, and the directory change is successful, the absolute pathname of the new working directory is written to the standard output.

The return status is zero if the directory is successfully changed, non-zero otherwise.`continue`

Resume the next iteration of an enclosing `for`, `while`, `until`, or `select` loop. If n is supplied, the execution of the nth enclosing loop is resumed. n must be greater than or equal to 1. The return status is zero unless n is not greater than or equal to 1.`eval`

The arguments are concatenated together into a single command, which is then read and executed, and its exit status returned as the exit status of `eval`. If there are no arguments or only empty arguments, the return status is zero.`exec`

```text
exec [-cl] [-a name] [command [arguments]]
```

If command is supplied, it replaces the shell without creating a new process. If the -l option is supplied, the shell places a dash at the beginning of the zeroth argument passed to command. This is what the `login` program does. The -c option causes command to be executed with an empty environment. If -a is supplied, the shell passes name as the zeroth argument to command. If command cannot be executed for some reason, a non-interactive shell exits, unless the `execfail` shell option is enabled. In that case, it returns failure. An interactive shell returns failure if the file cannot be executed. A subshell exits unconditionally if `exec` fails. If no command is specified, redirections may be used to affect the current shell environment. If there are no redirection errors, the return status is zero; otherwise the return status is non-zero.`exit`

Exit the shell, returning a status of n to the shell’s parent. If n is omitted, the exit status is that of the last command executed. Any trap on `EXIT` is executed before the shell terminates.`export`

```text
export [-fn] [-p] [name[=value]]
```

Mark each name to be passed to child processes in the environment. If the -f option is supplied, the names refer to shell functions; otherwise the names refer to shell variables. The -n option means to no longer mark each name for export. If no names are supplied, or if the -p option is given, a list of names of all exported variables is displayed. The -p option displays output in a form that may be reused as input. If a variable name is followed by =value, the value of the variable is set to value.

The return status is zero unless an invalid option is supplied, one of the names is not a valid shell variable name, or -f is supplied with a name that is not a shell function.`getopts`

```text
getopts optstring name [args]
```

`getopts` is used by shell scripts to parse positional parameters. optstring contains the option characters to be recognized; if a character is followed by a colon, the option is expected to have an argument, which should be separated from it by whitespace. The colon \(‘:’\) and question mark \(‘?’\) may not be used as option characters. Each time it is invoked, `getopts` places the next option in the shell variable name, initializing name if it does not exist, and the index of the next argument to be processed into the variable `OPTIND`. `OPTIND` is initialized to 1 each time the shell or a shell script is invoked. When an option requires an argument, `getopts` places that argument into the variable `OPTARG`. The shell does not reset `OPTIND` automatically; it must be manually reset between multiple calls to `getopts` within the same shell invocation if a new set of parameters is to be used.

When the end of options is encountered, `getopts` exits with a return value greater than zero. `OPTIND` is set to the index of the first non-option argument, and name is set to ‘?’.

`getopts` normally parses the positional parameters, but if more arguments are given in args, `getopts` parses those instead.

`getopts` can report errors in two ways. If the first character of optstring is a colon, silent error reporting is used. In normal operation, diagnostic messages are printed when invalid options or missing option arguments are encountered. If the variable `OPTERR` is set to 0, no error messages will be displayed, even if the first character of `optstring` is not a colon.

If an invalid option is seen, `getopts` places ‘?’ into name and, if not silent, prints an error message and unsets `OPTARG`. If `getopts` is silent, the option character found is placed in `OPTARG` and no diagnostic message is printed.

If a required argument is not found, and `getopts` is not silent, a question mark \(‘?’\) is placed in name, `OPTARG` is unset, and a diagnostic message is printed. If `getopts` is silent, then a colon \(‘:’\) is placed in name and `OPTARG` is set to the option character found.`hash`

```text
hash [-r] [-p filename] [-dt] [name]
```

Each time `hash` is invoked, it remembers the full pathnames of the commands specified as name arguments, so they need not be searched for on subsequent invocations. The commands are found by searching through the directories listed in `$PATH`. Any previously-remembered pathname is discarded. The -p option inhibits the path search, and filename is used as the location of name. The -r option causes the shell to forget all remembered locations. The -d option causes the shell to forget the remembered location of each name. If the -t option is supplied, the full pathname to which each name corresponds is printed. If multiple name arguments are supplied with -t, the name is printed before the hashed full pathname. The -l option causes output to be displayed in a format that may be reused as input. If no arguments are given, or if only -l is supplied, information about remembered commands is printed. The return status is zero unless a name is not found or an invalid option is supplied.`pwd`

Print the absolute pathname of the current working directory. If the -P option is supplied, the pathname printed will not contain symbolic links. If the -L option is supplied, the pathname printed may contain symbolic links. The return status is zero unless an error is encountered while determining the name of the current directory or an invalid option is supplied.`readonly`

```text
readonly [-aAf] [-p] [name[=value]] …
```

Mark each name as readonly. The values of these names may not be changed by subsequent assignment. If the -f option is supplied, each name refers to a shell function. The -a option means each name refers to an indexed array variable; the -A option means each name refers to an associative array variable. If both options are supplied, -A takes precedence. If no name arguments are given, or if the -p option is supplied, a list of all readonly names is printed. The other options may be used to restrict the output to a subset of the set of readonly names. The -p option causes output to be displayed in a format that may be reused as input. If a variable name is followed by =value, the value of the variable is set to value. The return status is zero unless an invalid option is supplied, one of the name arguments is not a valid shell variable or function name, or the -f option is supplied with a name that is not a shell function.`return`

Cause a shell function to stop executing and return the value n to its caller. If n is not supplied, the return value is the exit status of the last command executed in the function. If `return` is executed by a trap handler, the last command used to determine the status is the last command executed before the trap handler. If `return` is executed during a `DEBUG` trap, the last command used to determine the status is the last command executed by the trap handler before `return` was invoked. `return` may also be used to terminate execution of a script being executed with the `.` \(`source`\) builtin, returning either n or the exit status of the last command executed within the script as the exit status of the script. If n is supplied, the return value is its least significant 8 bits. Any command associated with the `RETURN` trap is executed before execution resumes after the function or script. The return status is non-zero if `return` is supplied a non-numeric argument or is used outside a function and not during the execution of a script by `.` or `source`.`shift`

Shift the positional parameters to the left by n. The positional parameters from n+1 … `$#` are renamed to `$1` … `$#`-n. Parameters represented by the numbers `$#` to `$#`-n+1 are unset. n must be a non-negative number less than or equal to `$#`. If n is zero or greater than `$#`, the positional parameters are not changed. If n is not supplied, it is assumed to be 1. The return status is zero unless n is greater than `$#` or less than zero, non-zero otherwise.`test[`

Evaluate a conditional expression expr and return a status of 0 \(true\) or 1 \(false\). Each operator and operand must be a separate argument. Expressions are composed of the primaries described below in [Bash Conditional Expressions](bash-conditional-expressions-bash-reference-manual.md#Bash-Conditional-Expressions). `test` does not accept any options, nor does it accept and ignore an argument of -- as signifying the end of options.

When the `[` form is used, the last argument to the command must be a `]`.

Expressions may be combined using the following operators, listed in decreasing order of precedence. The evaluation depends on the number of arguments; see below. Operator precedence is used when there are five or more arguments.`! expr`

True if expr is false.`( expr )`

Returns the value of expr. This may be used to override the normal precedence of operators.`expr1 -a expr2`

True if both expr1 and expr2 are true.`expr1 -o expr2`

True if either expr1 or expr2 is true.

The `test` and `[` builtins evaluate conditional expressions using a set of rules based on the number of arguments.0 arguments

The expression is false.1 argument

The expression is true if, and only if, the argument is not null.2 arguments

If the first argument is ‘!’, the expression is true if and only if the second argument is null. If the first argument is one of the unary conditional operators \(see [Bash Conditional Expressions](bash-conditional-expressions-bash-reference-manual.md#Bash-Conditional-Expressions)\), the expression is true if the unary test is true. If the first argument is not a valid unary operator, the expression is false.3 arguments

The following conditions are applied in the order listed.

1.  If the second argument is one of the binary conditional operators \(see [Bash Conditional Expressions](bash-conditional-expressions-bash-reference-manual.md#Bash-Conditional-Expressions)\), the result of the expression is the result of the binary test using the first and third arguments as operands. The ‘-a’ and ‘-o’ operators are considered binary operators when there are three arguments.
2.  If the first argument is ‘!’, the value is the negation of the two-argument test using the second and third arguments.
3.  If the first argument is exactly ‘\(’ and the third argument is exactly ‘\)’, the result is the one-argument test of the second argument.
4.  Otherwise, the expression is false.

4 arguments

If the first argument is ‘!’, the result is the negation of the three-argument expression composed of the remaining arguments. Otherwise, the expression is parsed and evaluated according to precedence using the rules listed above.5 or more arguments

The expression is parsed and evaluated according to precedence using the rules listed above.

When used with `test` or ‘\[’, the ‘&lt;’ and ‘&gt;’ operators sort lexicographically using ASCII ordering.`times`

Print out the user and system times used by the shell and its children. The return status is zero.`trap`

```text
trap [-lp] [arg] [sigspec …]
```

The commands in arg are to be read and executed when the shell receives signal sigspec. If arg is absent \(and there is a single sigspec\) or equal to ‘-’, each specified signal’s disposition is reset to the value it had when the shell was started. If arg is the null string, then the signal specified by each sigspec is ignored by the shell and commands it invokes. If arg is not present and -p has been supplied, the shell displays the trap commands associated with each sigspec. If no arguments are supplied, or only -p is given, `trap` prints the list of commands associated with each signal number in a form that may be reused as shell input. The -l option causes the shell to print a list of signal names and their corresponding numbers. Each sigspec is either a signal name or a signal number. Signal names are case insensitive and the `SIG` prefix is optional.

If a sigspec is `0` or `EXIT`, arg is executed when the shell exits. If a sigspec is `DEBUG`, the command arg is executed before every simple command, `for` command, `case` command, `select` command, every arithmetic `for` command, and before the first command executes in a shell function. Refer to the description of the `extdebug` option to the `shopt` builtin \(see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\) for details of its effect on the `DEBUG` trap. If a sigspec is `RETURN`, the command arg is executed each time a shell function or a script executed with the `.` or `source` builtins finishes executing.

If a sigspec is `ERR`, the command arg is executed whenever a pipeline \(which may consist of a single simple command\), a list, or a compound command returns a non-zero exit status, subject to the following conditions. The `ERR` trap is not executed if the failed command is part of the command list immediately following an `until` or `while` keyword, part of the test following the `if` or `elif` reserved words, part of a command executed in a `&&` or `||` list except the command following the final `&&` or `||`, any command in a pipeline but the last, or if the command’s return status is being inverted using `!`. These are the same conditions obeyed by the `errexit` \(-e\) option.

Signals ignored upon entry to the shell cannot be trapped or reset. Trapped signals that are not being ignored are reset to their original values in a subshell or subshell environment when one is created.

The return status is zero unless a sigspec does not specify a valid signal.`umask`

Set the shell process’s file creation mask to mode. If mode begins with a digit, it is interpreted as an octal number; if not, it is interpreted as a symbolic mode mask similar to that accepted by the `chmod` command. If mode is omitted, the current value of the mask is printed. If the -S option is supplied without a mode argument, the mask is printed in a symbolic format. If the -p option is supplied, and mode is omitted, the output is in a form that may be reused as input. The return status is zero if the mode is successfully changed or if no mode argument is supplied, and non-zero otherwise.

Note that when the mode is interpreted as an octal number, each number of the umask is subtracted from `7`. Thus, a umask of `022` results in permissions of `755`.`unset`

Remove each variable or function name. If the -v option is given, each name refers to a shell variable and that variable is removed. If the -f option is given, the names refer to shell functions, and the function definition is removed. If the -n option is supplied, and name is a variable with the nameref attribute, name will be unset rather than the variable it references. -n has no effect if the -f option is supplied. If no options are supplied, each name refers to a variable; if there is no variable by that name, any function with that name is unset. Readonly variables and functions may not be unset. The return status is zero unless a name is readonly.

