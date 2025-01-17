# Bash POSIX Mode \(Bash Reference Manual\)

## 6.11 Bash POSIX Mode

Starting Bash with the --posix command-line option or executing ‘set -o posix’ while Bash is running will cause Bash to conform more closely to the POSIX standard by changing the behavior to match that specified by POSIX in areas where the Bash default differs.

When invoked as `sh`, Bash enters POSIX mode after reading the startup files.

The following list is what’s changed when ‘POSIX mode’ is in effect:

1.  Bash ensures that the `POSIXLY_CORRECT` variable is set.
2.  When a command in the hash table no longer exists, Bash will re-search `$PATH` to find the new location. This is also available with ‘shopt -s checkhash’.
3.  The message printed by the job control code and builtins when a job exits with a non-zero status is ‘Done\(status\)’.
4.  The message printed by the job control code and builtins when a job is stopped is ‘Stopped\(signame\)’, where signame is, for example, `SIGTSTP`.
5.  Alias expansion is always enabled, even in non-interactive shells.
6.  Reserved words appearing in a context where reserved words are recognized do not undergo alias expansion.
7.  The POSIX `PS1` and `PS2` expansions of ‘!’ to the history number and ‘!!’ to ‘!’ are enabled, and parameter expansion is performed on the values of `PS1` and `PS2` regardless of the setting of the `promptvars` option.
8.  The POSIX startup files are executed \(`$ENV`\) rather than the normal Bash files.
9.  Tilde expansion is only performed on assignments preceding a command name, rather than on all assignment statements on the line.
10.  The default history file is ~/.sh\_history \(this is the default value of `$HISTFILE`\).
11.  Redirection operators do not perform filename expansion on the word in the redirection unless the shell is interactive.
12.  Redirection operators do not perform word splitting on the word in the redirection.
13.  Function names must be valid shell `name`s. That is, they may not contain characters other than letters, digits, and underscores, and may not start with a digit. Declaring a function with an invalid name causes a fatal syntax error in non-interactive shells.
14.  Function names may not be the same as one of the POSIX special builtins.
15.  POSIX special builtins are found before shell functions during command lookup.
16.  When printing shell function definitions \(e.g., by `type`\), Bash does not print the `function` keyword.
17.  Literal tildes that appear as the first character in elements of the `PATH` variable are not expanded as described above under [Tilde Expansion](tilde-expansion-bash-reference-manual.md#Tilde-Expansion).
18.  The `time` reserved word may be used by itself as a command. When used in this way, it displays timing statistics for the shell and its completed children. The `TIMEFORMAT` variable controls the format of the timing information.
19.  When parsing and expanding a ${…} expansion that appears within double quotes, single quotes are no longer special and cannot be used to quote a closing brace or other special character, unless the operator is one of those defined to perform pattern removal. In this case, they do not have to appear as matched pairs.
20.  The parser does not recognize `time` as a reserved word if the next token begins with a ‘-’.
21.  The ‘!’ character does not introduce history expansion within a double-quoted string, even if the `histexpand` option is enabled.
22.  If a POSIX special builtin returns an error status, a non-interactive shell exits. The fatal errors are those listed in the POSIX standard, and include things like passing incorrect options, redirection errors, variable assignment errors for assignments preceding the command name, and so on.
23.  A non-interactive shell exits with an error status if a variable assignment error occurs when no command name follows the assignment statements. A variable assignment error occurs, for example, when trying to assign a value to a readonly variable.
24.  A non-interactive shell exits with an error status if a variable assignment error occurs in an assignment statement preceding a special builtin, but not with any other simple command.
25.  A non-interactive shell exits with an error status if the iteration variable in a `for` statement or the selection variable in a `select` statement is a readonly variable.
26.  Non-interactive shells exit if filename in `.` filename is not found.
27.  Non-interactive shells exit if a syntax error in an arithmetic expansion results in an invalid expression.
28.  Non-interactive shells exit if a parameter expansion error occurs.
29.  Non-interactive shells exit if there is a syntax error in a script read with the `.` or `source` builtins, or in a string processed by the `eval` builtin.
30.  Process substitution is not available.
31.  While variable indirection is available, it may not be applied to the ‘\#’ and ‘?’ special parameters.
32.  When expanding the ‘\*’ special parameter in a pattern context where the expansion is double-quoted does not treat the `$*` as if it were double-quoted.
33.  Assignment statements preceding POSIX special builtins persist in the shell environment after the builtin completes.
34.  Assignment statements preceding shell function calls persist in the shell environment after the function returns, as if a POSIX special builtin command had been executed.
35.  The `command` builtin does not prevent builtins that take assignment statements as arguments from expanding them as assignment statements; when not in POSIX mode, assignment builtins lose their assignment statement expansion properties when preceded by `command`.
36.  The `bg` builtin uses the required format to describe each job placed in the background, which does not include an indication of whether the job is the current or previous job.
37.  The output of ‘kill -l’ prints all the signal names on a single line, separated by spaces, without the ‘SIG’ prefix.
38.  The `kill` builtin does not accept signal names with a ‘SIG’ prefix.
39.  The `export` and `readonly` builtin commands display their output in the format required by POSIX.
40.  The `trap` builtin displays signal names without the leading `SIG`.
41.  The `trap` builtin doesn’t check the first argument for a possible signal specification and revert the signal handling to the original disposition if it is, unless that argument consists solely of digits and is a valid signal number. If users want to reset the handler for a given signal to the original disposition, they should use ‘-’ as the first argument.
42.  The `.` and `source` builtins do not search the current directory for the filename argument if it is not found by searching `PATH`.
43.  Enabling POSIX mode has the effect of setting the `inherit_errexit` option, so subshells spawned to execute command substitutions inherit the value of the -e option from the parent shell. When the `inherit_errexit` option is not enabled, Bash clears the -e option in such subshells.
44.  Enabling POSIX mode has the effect of setting the `shift_verbose` option, so numeric arguments to `shift` that exceed the number of positional parameters will result in an error message.
45.  When the `alias` builtin displays alias definitions, it does not display them with a leading ‘alias ’ unless the -p option is supplied.
46.  When the `set` builtin is invoked without options, it does not display shell function names and definitions.
47.  When the `set` builtin is invoked without options, it displays variable values without quotes, unless they contain shell metacharacters, even if the result contains nonprinting characters.
48.  When the `cd` builtin is invoked in logical mode, and the pathname constructed from `$PWD` and the directory name supplied as an argument does not refer to an existing directory, `cd` will fail instead of falling back to physical mode.
49.  When the `cd` builtin cannot change a directory because the length of the pathname constructed from `$PWD` and the directory name supplied as an argument exceeds PATH\_MAX when all symbolic links are expanded, `cd` will fail instead of attempting to use only the supplied directory name.
50.  The `pwd` builtin verifies that the value it prints is the same as the current directory, even if it is not asked to check the file system with the -P option.
51.  When listing the history, the `fc` builtin does not include an indication of whether or not a history entry has been modified.
52.  The default editor used by `fc` is `ed`.
53.  The `type` and `command` builtins will not report a non-executable file as having been found, though the shell will attempt to execute such a file if it is the only so-named file found in `$PATH`.
54.  The `vi` editing mode will invoke the `vi` editor directly when the ‘v’ command is run, instead of checking `$VISUAL` and `$EDITOR`.
55.  When the `xpg_echo` option is enabled, Bash does not attempt to interpret any arguments to `echo` as options. Each argument is displayed, after escape characters are converted.
56.  The `ulimit` builtin uses a block size of 512 bytes for the -c and -f options.
57.  The arrival of `SIGCHLD` when a trap is set on `SIGCHLD` does not interrupt the `wait` builtin and cause it to return immediately. The trap command is run once for each child that exits.
58.  The `read` builtin may be interrupted by a signal for which a trap has been set. If Bash receives a trapped signal while executing `read`, the trap handler executes and `read` returns an exit status greater than 128.
59.  Bash removes an exited background process’s status from the list of such statuses after the `wait` builtin is used to obtain it.

There is other POSIX behavior that Bash does not implement by default even when in POSIX mode. Specifically:

1.  The `fc` builtin checks `$EDITOR` as a program to edit history entries if `FCEDIT` is unset, rather than defaulting directly to `ed`. `fc` uses `ed` if `EDITOR` is unset.
2.  As noted above, Bash requires the `xpg_echo` option to be enabled for the `echo` builtin to be fully conformant.

Bash can be configured to be POSIX-conformant by default, by specifying the --enable-strict-posix-default to `configure` when building \(see [Optional Features](optional-features-bash-reference-manual.md#Optional-Features)\).

