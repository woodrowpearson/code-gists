# Bash Builtins \(Bash Reference Manual\)

This section describes builtin commands which are unique to or have been extended in Bash. Some of these commands are specified in the POSIX standard.`alias`

```text
alias [-p] [name[=value] …]
```

Without arguments or with the -p option, `alias` prints the list of aliases on the standard output in a form that allows them to be reused as input. If arguments are supplied, an alias is defined for each name whose value is given. If no value is given, the name and value of the alias is printed. Aliases are described in [Aliases](aliases-bash-reference-manual.md#Aliases).`bind`

```text
bind [-m keymap] [-lpsvPSVX]
bind [-m keymap] [-q function] [-u function] [-r keyseq]
bind [-m keymap] -f filename
bind [-m keymap] -x keyseq:shell-command
bind [-m keymap] keyseq:function-name
bind [-m keymap] keyseq:readline-command
```

Display current Readline \(see [Command Line Editing](command-line-editing-bash-reference-manual.md#Command-Line-Editing)\) key and function bindings, bind a key sequence to a Readline function or macro, or set a Readline variable. Each non-option argument is a command as it would appear in a Readline initialization file \(see [Readline Init File](readline-init-file-bash-reference-manual.md#Readline-Init-File)\), but each binding or command must be passed as a separate argument; e.g., ‘"\C-x\C-r":re-read-init-file’.

Options, if supplied, have the following meanings:`-m keymap`

Use keymap as the keymap to be affected by the subsequent bindings. Acceptable keymap names are `emacs`, `emacs-standard`, `emacs-meta`, `emacs-ctlx`, `vi`, `vi-move`, `vi-command`, and `vi-insert`. `vi` is equivalent to `vi-command` \(`vi-move` is also a synonym\); `emacs` is equivalent to `emacs-standard`.`-l`

List the names of all Readline functions.`-p`

Display Readline function names and bindings in such a way that they can be used as input or in a Readline initialization file.`-P`

List current Readline function names and bindings.`-v`

Display Readline variable names and values in such a way that they can be used as input or in a Readline initialization file.`-V`

List current Readline variable names and values.`-s`

Display Readline key sequences bound to macros and the strings they output in such a way that they can be used as input or in a Readline initialization file.`-S`

Display Readline key sequences bound to macros and the strings they output.`-f filename`

Read key bindings from filename.`-q function`

Query about which keys invoke the named function.`-u function`

Unbind all keys bound to the named function.`-r keyseq`

Remove any current binding for keyseq.`-x keyseq:shell-command`

Cause shell-command to be executed whenever keyseq is entered. When shell-command is executed, the shell sets the `READLINE_LINE` variable to the contents of the Readline line buffer and the `READLINE_POINT` variable to the current location of the insertion point. If the executed command changes the value of `READLINE_LINE` or `READLINE_POINT`, those new values will be reflected in the editing state.`-X`

List all key sequences bound to shell commands and the associated commands in a format that can be reused as input.

The return status is zero unless an invalid option is supplied or an error occurs.`builtin`

```text
builtin [shell-builtin [args]]
```

Run a shell builtin, passing it args, and return its exit status. This is useful when defining a shell function with the same name as a shell builtin, retaining the functionality of the builtin within the function. The return status is non-zero if shell-builtin is not a shell builtin command.`caller`

Returns the context of any active subroutine call \(a shell function or a script executed with the `.` or `source` builtins\).

Without expr, `caller` displays the line number and source filename of the current subroutine call. If a non-negative integer is supplied as expr, `caller` displays the line number, subroutine name, and source file corresponding to that position in the current execution call stack. This extra information may be used, for example, to print a stack trace. The current frame is frame 0.

The return value is 0 unless the shell is not executing a subroutine call or expr does not correspond to a valid position in the call stack.`command`

```text
command [-pVv] command [arguments …]
```

Runs command with arguments ignoring any shell function named command. Only shell builtin commands or commands found by searching the `PATH` are executed. If there is a shell function named `ls`, running ‘command ls’ within the function will execute the external command `ls` instead of calling the function recursively. The -p option means to use a default value for `PATH` that is guaranteed to find all of the standard utilities. The return status in this case is 127 if command cannot be found or an error occurred, and the exit status of command otherwise.

If either the -V or -v option is supplied, a description of command is printed. The -v option causes a single word indicating the command or file name used to invoke command to be displayed; the -V option produces a more verbose description. In this case, the return status is zero if command is found, and non-zero if not.`declare`

```text
declare [-aAfFgilnrtux] [-p] [name[=value] …]
```

Declare variables and give them attributes. If no names are given, then display the values of variables instead.

The -p option will display the attributes and values of each name. When -p is used with name arguments, additional options, other than -f and -F, are ignored.

When -p is supplied without name arguments, `declare` will display the attributes and values of all variables having the attributes specified by the additional options. If no other options are supplied with -p, `declare` will display the attributes and values of all shell variables. The -f option will restrict the display to shell functions.

The -F option inhibits the display of function definitions; only the function name and attributes are printed. If the `extdebug` shell option is enabled using `shopt` \(see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\), the source file name and line number where each name is defined are displayed as well. -F implies -f.

The -g option forces variables to be created or modified at the global scope, even when `declare` is executed in a shell function. It is ignored in all other cases.

The following options can be used to restrict output to variables with the specified attributes or to give variables attributes:`-a`

Each name is an indexed array variable \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\).`-A`

Each name is an associative array variable \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\).`-f`

Use function names only.`-i`

The variable is to be treated as an integer; arithmetic evaluation \(see [Shell Arithmetic](shell-arithmetic-bash-reference-manual.md#Shell-Arithmetic)\) is performed when the variable is assigned a value.`-l`

When the variable is assigned a value, all upper-case characters are converted to lower-case. The upper-case attribute is disabled.`-n`

Give each name the nameref attribute, making it a name reference to another variable. That other variable is defined by the value of name. All references, assignments, and attribute modifications to name, except for those using or changing the -n attribute itself, are performed on the variable referenced by name’s value. The nameref attribute cannot be applied to array variables.`-r`

Make names readonly. These names cannot then be assigned values by subsequent assignment statements or unset.`-t`

Give each name the `trace` attribute. Traced functions inherit the `DEBUG` and `RETURN` traps from the calling shell. The trace attribute has no special meaning for variables.`-u`

When the variable is assigned a value, all lower-case characters are converted to upper-case. The lower-case attribute is disabled.`-x`

Mark each name for export to subsequent commands via the environment.

Using ‘+’ instead of ‘-’ turns off the attribute instead, with the exceptions that ‘+a’ and ‘+A’ may not be used to destroy array variables and ‘+r’ will not remove the readonly attribute. When used in a function, `declare` makes each name local, as with the `local` command, unless the -g option is used. If a variable name is followed by =value, the value of the variable is set to value.

When using -a or -A and the compound assignment syntax to create array variables, additional attributes do not take effect until subsequent assignments.

The return status is zero unless an invalid option is encountered, an attempt is made to define a function using ‘-f foo=bar’, an attempt is made to assign a value to a readonly variable, an attempt is made to assign a value to an array variable without using the compound assignment syntax \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\), one of the names is not a valid shell variable name, an attempt is made to turn off readonly status for a readonly variable, an attempt is made to turn off array status for an array variable, or an attempt is made to display a non-existent function with -f.`echo`

Output the args, separated by spaces, terminated with a newline. The return status is 0 unless a write error occurs. If -n is specified, the trailing newline is suppressed. If the -e option is given, interpretation of the following backslash-escaped characters is enabled. The -E option disables the interpretation of these escape characters, even on systems where they are interpreted by default. The `xpg_echo` shell option may be used to dynamically determine whether or not `echo` expands these escape characters by default. `echo` does not interpret -- to mean the end of options.

`echo` interprets the following escape sequences:`\a`

alert \(bell\)`\b`

backspace`\c`

suppress further output`\e\E`

escape`\f`

form feed`\n`

new line`\r`

carriage return`\t`

horizontal tab`\v`

vertical tab`\\`

backslash`\0nnn`

the eight-bit character whose value is the octal value nnn \(zero to three octal digits\)`\xHH`

the eight-bit character whose value is the hexadecimal value HH \(one or two hex digits\)`\uHHHH`

the Unicode \(ISO/IEC 10646\) character whose value is the hexadecimal value HHHH \(one to four hex digits\)`\UHHHHHHHH`

the Unicode \(ISO/IEC 10646\) character whose value is the hexadecimal value HHHHHHHH \(one to eight hex digits\)`enable`

```text
enable [-a] [-dnps] [-f filename] [name …]
```

Enable and disable builtin shell commands. Disabling a builtin allows a disk command which has the same name as a shell builtin to be executed without specifying a full pathname, even though the shell normally searches for builtins before disk commands. If -n is used, the names become disabled. Otherwise names are enabled. For example, to use the `test` binary found via `$PATH` instead of the shell builtin version, type ‘enable -n test’.

If the -p option is supplied, or no name arguments appear, a list of shell builtins is printed. With no other arguments, the list consists of all enabled shell builtins. The -a option means to list each builtin with an indication of whether or not it is enabled.

The -f option means to load the new builtin command name from shared object filename, on systems that support dynamic loading. The -d option will delete a builtin loaded with -f.

If there are no options, a list of the shell builtins is displayed. The -s option restricts `enable` to the POSIX special builtins. If -s is used with -f, the new builtin becomes a special builtin \(see [Special Builtins](special-builtins-bash-reference-manual.md#Special-Builtins)\).

The return status is zero unless a name is not a shell builtin or there is an error loading a new builtin from a shared object.`help`

Display helpful information about builtin commands. If pattern is specified, `help` gives detailed help on all commands matching pattern, otherwise a list of the builtins is printed.

Options, if supplied, have the following meanings:`-d`

Display a short description of each pattern`-m`

Display the description of each pattern in a manpage-like format`-s`

Display only a short usage synopsis for each pattern

The return status is zero unless no command matches pattern.`let`

```text
let expression [expression …]
```

The `let` builtin allows arithmetic to be performed on shell variables. Each expression is evaluated according to the rules given below in [Shell Arithmetic](shell-arithmetic-bash-reference-manual.md#Shell-Arithmetic). If the last expression evaluates to 0, `let` returns 1; otherwise 0 is returned.`local`

```text
local [option] name[=value] …
```

For each argument, a local variable named name is created, and assigned value. The option can be any of the options accepted by `declare`. `local` can only be used within a function; it makes the variable name have a visible scope restricted to that function and its children. If name is ‘-’, the set of shell options is made local to the function in which `local` is invoked: shell options changed using the `set` builtin inside the function are restored to their original values when the function returns. The return status is zero unless `local` is used outside a function, an invalid name is supplied, or name is a readonly variable.`logout`

Exit a login shell, returning a status of n to the shell’s parent.`mapfile`

```text
mapfile [-d delim] [-n count] [-O origin] [-s count]
    [-t] [-u fd] [-C callback] [-c quantum] [array]
```

Read lines from the standard input into the indexed array variable array, or from file descriptor fd if the -u option is supplied. The variable `MAPFILE` is the default array. Options, if supplied, have the following meanings:`-d`

The first character of delim is used to terminate each input line, rather than newline. If delim is the empty string, `mapfile` will terminate a line when it reads a NUL character.`-n`

Copy at most count lines. If count is 0, all lines are copied.`-O`

Begin assigning to array at index origin. The default index is 0.`-s`

Discard the first count lines read.`-t`

Remove a trailing delim \(default newline\) from each line read.`-u`

Read lines from file descriptor fd instead of the standard input.`-C`

Evaluate callback each time quantum lines are read. The -c option specifies quantum.`-c`

Specify the number of lines read between each call to callback.

If -C is specified without -c, the default quantum is 5000. When callback is evaluated, it is supplied the index of the next array element to be assigned and the line to be assigned to that element as additional arguments. callback is evaluated after the line is read but before the array element is assigned.

If not supplied with an explicit origin, `mapfile` will clear array before assigning to it.

`mapfile` returns successfully unless an invalid option or option argument is supplied, array is invalid or unassignable, or array is not an indexed array.`printf`

```text
printf [-v var] format [arguments]
```

Write the formatted arguments to the standard output under the control of the format. The -v option causes the output to be assigned to the variable var rather than being printed to the standard output.

The format is a character string which contains three types of objects: plain characters, which are simply copied to standard output, character escape sequences, which are converted and copied to the standard output, and format specifications, each of which causes printing of the next successive argument. In addition to the standard `printf(1)` formats, `printf` interprets the following extensions:`%b`

Causes `printf` to expand backslash escape sequences in the corresponding argument in the same way as `echo -e` \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).`%q`

Causes `printf` to output the corresponding argument in a format that can be reused as shell input.`%(datefmt)T`

Causes `printf` to output the date-time string resulting from using datefmt as a format string for `strftime`\(3\). The corresponding argument is an integer representing the number of seconds since the epoch. Two special argument values may be used: -1 represents the current time, and -2 represents the time the shell was invoked. If no argument is specified, conversion behaves as if -1 had been given. This is an exception to the usual `printf` behavior.

Arguments to non-string format specifiers are treated as C language constants, except that a leading plus or minus sign is allowed, and if the leading character is a single or double quote, the value is the ASCII value of the following character.

The format is reused as necessary to consume all of the arguments. If the format requires more arguments than are supplied, the extra format specifications behave as if a zero value or null string, as appropriate, had been supplied. The return value is zero on success, non-zero on failure.`read`

```text
read [-ers] [-a aname] [-d delim] [-i text] [-n nchars]
    [-N nchars] [-p prompt] [-t timeout] [-u fd] [name …]
```

One line is read from the standard input, or from the file descriptor fd supplied as an argument to the -u option, split into words as described above in [Word Splitting](word-splitting-bash-reference-manual.md#Word-Splitting), and the first word is assigned to the first name, the second word to the second name, and so on. If there are more words than names, the remaining words and their intervening delimiters are assigned to the last name. If there are fewer words read from the input stream than names, the remaining names are assigned empty values. The characters in the value of the `IFS` variable are used to split the line into words using the same rules the shell uses for expansion \(described above in [Word Splitting](word-splitting-bash-reference-manual.md#Word-Splitting)\). The backslash character ‘\’ may be used to remove any special meaning for the next character read and for line continuation. If no names are supplied, the line read is assigned to the variable `REPLY`. The exit status is zero, unless end-of-file is encountered, `read` times out \(in which case the status is greater than 128\), a variable assignment error \(such as assigning to a readonly variable\) occurs, or an invalid file descriptor is supplied as the argument to -u.

Options, if supplied, have the following meanings:`-a aname`

The words are assigned to sequential indices of the array variable aname, starting at 0. All elements are removed from aname before the assignment. Other name arguments are ignored.`-d delim`

The first character of delim is used to terminate the input line, rather than newline. If delim is the empty string, `read` will terminate a line when it reads a NUL character.`-e`

Readline \(see [Command Line Editing](command-line-editing-bash-reference-manual.md#Command-Line-Editing)\) is used to obtain the line. Readline uses the current \(or default, if line editing was not previously active\) editing settings, but uses Readline’s default filename completion.`-i text`

If Readline is being used to read the line, text is placed into the editing buffer before editing begins.`-n nchars`

`read` returns after reading nchars characters rather than waiting for a complete line of input, but honors a delimiter if fewer than nchars characters are read before the delimiter.`-N nchars`

`read` returns after reading exactly nchars characters rather than waiting for a complete line of input, unless EOF is encountered or `read` times out. Delimiter characters encountered in the input are not treated specially and do not cause `read` to return until nchars characters are read. The result is not split on the characters in `IFS`; the intent is that the variable is assigned exactly the characters read \(with the exception of backslash; see the -r option below\).`-p prompt`

Display prompt, without a trailing newline, before attempting to read any input. The prompt is displayed only if input is coming from a terminal.`-r`

If this option is given, backslash does not act as an escape character. The backslash is considered to be part of the line. In particular, a backslash-newline pair may not then be used as a line continuation.`-s`

Silent mode. If input is coming from a terminal, characters are not echoed.`-t timeout`

Cause `read` to time out and return failure if a complete line of input \(or a specified number of characters\) is not read within timeout seconds. timeout may be a decimal number with a fractional portion following the decimal point. This option is only effective if `read` is reading input from a terminal, pipe, or other special file; it has no effect when reading from regular files. If `read` times out, `read` saves any partial input read into the specified variable name. If timeout is 0, `read` returns immediately, without trying to read and data. The exit status is 0 if input is available on the specified file descriptor, non-zero otherwise. The exit status is greater than 128 if the timeout is exceeded.`-u fd`

Read input from file descriptor fd.`readarray`

```text
readarray [-d delim] [-n count] [-O origin] [-s count]
    [-t] [-u fd] [-C callback] [-c quantum] [array]
```

Read lines from the standard input into the indexed array variable array, or from file descriptor fd if the -u option is supplied.

A synonym for `mapfile`.`source`

A synonym for `.` \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).`type`

For each name, indicate how it would be interpreted if used as a command name.

If the -t option is used, `type` prints a single word which is one of ‘alias’, ‘function’, ‘builtin’, ‘file’ or ‘keyword’, if name is an alias, shell function, shell builtin, disk file, or shell reserved word, respectively. If the name is not found, then nothing is printed, and `type` returns a failure status.

If the -p option is used, `type` either returns the name of the disk file that would be executed, or nothing if -t would not return ‘file’.

The -P option forces a path search for each name, even if -t would not return ‘file’.

If a command is hashed, -p and -P print the hashed value, which is not necessarily the file that appears first in `$PATH`.

If the -a option is used, `type` returns all of the places that contain an executable named file. This includes aliases and functions, if and only if the -p option is not also used.

If the -f option is used, `type` does not attempt to find shell functions, as with the `command` builtin.

The return status is zero if all of the names are found, non-zero if any are not found.`typeset`

```text
typeset [-afFgrxilnrtux] [-p] [name[=value] …]
```

The `typeset` command is supplied for compatibility with the Korn shell. It is a synonym for the `declare` builtin command.`ulimit`

```text
ulimit [-HSabcdefiklmnpqrstuvxPT] [limit]
```

`ulimit` provides control over the resources available to processes started by the shell, on systems that allow such control. If an option is given, it is interpreted as follows:`-S`

Change and report the soft limit associated with a resource.`-H`

Change and report the hard limit associated with a resource.`-a`

All current limits are reported.`-b`

The maximum socket buffer size.`-c`

The maximum size of core files created.`-d`

The maximum size of a process’s data segment.`-e`

The maximum scheduling priority \("nice"\).`-f`

The maximum size of files written by the shell and its children.`-i`

The maximum number of pending signals.`-k`

The maximum number of kqueues that may be allocated.`-l`

The maximum size that may be locked into memory.`-m`

The maximum resident set size \(many systems do not honor this limit\).`-n`

The maximum number of open file descriptors \(most systems do not allow this value to be set\).`-p`

The pipe buffer size.`-q`

The maximum number of bytes in POSIX message queues.`-r`

The maximum real-time scheduling priority.`-s`

The maximum stack size.`-t`

The maximum amount of cpu time in seconds.`-u`

The maximum number of processes available to a single user.`-v`

The maximum amount of virtual memory available to the shell, and, on some systems, to its children.`-x`

The maximum number of file locks.`-P`

The maximum number of pseudoterminals.`-T`

The maximum number of threads.

If limit is given, and the -a option is not used, limit is the new value of the specified resource. The special limit values `hard`, `soft`, and `unlimited` stand for the current hard limit, the current soft limit, and no limit, respectively. A hard limit cannot be increased by a non-root user once it is set; a soft limit may be increased up to the value of the hard limit. Otherwise, the current value of the soft limit for the specified resource is printed, unless the -H option is supplied. When setting new limits, if neither -H nor -S is supplied, both the hard and soft limits are set. If no option is given, then -f is assumed. Values are in 1024-byte increments, except for -t, which is in seconds; -p, which is in units of 512-byte blocks; -P, -T, -b, -k, -n and -u, which are unscaled values; and, when in POSIX Mode \(see [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode)\), -c and -f, which are in 512-byte increments.

The return status is zero unless an invalid option or argument is supplied, or an error occurs while setting a new limit.`unalias`

Remove each name from the list of aliases. If -a is supplied, all aliases are removed. Aliases are described in [Aliases](aliases-bash-reference-manual.md#Aliases).

