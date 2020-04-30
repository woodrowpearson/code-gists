# Bash Conditional Expressions \(Bash Reference Manual\)

## 6.4 Bash Conditional Expressions

Conditional expressions are used by the `[[` compound command and the `test` and `[` builtin commands. The `test` and `[` commands determine their behavior based on the number of arguments; see the descriptions of those commands for any other command-specific actions.

Expressions may be unary or binary, and are formed from the following primaries. Unary expressions are often used to examine the status of a file. There are string operators and numeric comparison operators as well. Bash handles several filenames specially when they are used in expressions. If the operating system on which Bash is running provides these special files, Bash will use them; otherwise it will emulate them internally with this behavior: If the file argument to one of the primaries is of the form /dev/fd/N, then file descriptor N is checked. If the file argument to one of the primaries is one of /dev/stdin, /dev/stdout, or /dev/stderr, file descriptor 0, 1, or 2, respectively, is checked.

When used with `[[`, the ‘&lt;’ and ‘&gt;’ operators sort lexicographically using the current locale. The `test` command uses ASCII ordering.

Unless otherwise specified, primaries that operate on files follow symbolic links and operate on the target of the link, rather than the link itself.`-a file`

True if file exists.`-b file`

True if file exists and is a block special file.`-c file`

True if file exists and is a character special file.`-d file`

True if file exists and is a directory.`-e file`

True if file exists.`-f file`

True if file exists and is a regular file.`-g file`

True if file exists and its set-group-id bit is set.`-h file`

True if file exists and is a symbolic link.`-k file`

True if file exists and its "sticky" bit is set.`-p file`

True if file exists and is a named pipe \(FIFO\).`-r file`

True if file exists and is readable.`-s file`

True if file exists and has a size greater than zero.`-t fd`

True if file descriptor fd is open and refers to a terminal.`-u file`

True if file exists and its set-user-id bit is set.`-w file`

True if file exists and is writable.`-x file`

True if file exists and is executable.`-G file`

True if file exists and is owned by the effective group id.`-L file`

True if file exists and is a symbolic link.`-N file`

True if file exists and has been modified since it was last read.`-O file`

True if file exists and is owned by the effective user id.`-S file`

True if file exists and is a socket.`file1 -ef file2`

True if file1 and file2 refer to the same device and inode numbers.`file1 -nt file2`

True if file1 is newer \(according to modification date\) than file2, or if file1 exists and file2 does not.`file1 -ot file2`

True if file1 is older than file2, or if file2 exists and file1 does not.`-o optname`

True if the shell option optname is enabled. The list of options appears in the description of the -o option to the `set` builtin \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\).`-v varname`

True if the shell variable varname is set \(has been assigned a value\).`-R varname`

True if the shell variable varname is set and is a name reference.`-z string`

True if the length of string is zero.`-n stringstring`

True if the length of string is non-zero.`string1 == string2string1 = string2`

True if the strings are equal. When used with the `[[` command, this performs pattern matching as described above \(see [Conditional Constructs](conditional-constructs-bash-reference-manual.md#Conditional-Constructs)\).

‘=’ should be used with the `test` command for POSIX conformance.`string1 != string2`

True if the strings are not equal.`string1 < string2`

True if string1 sorts before string2 lexicographically.`string1 > string2`

True if string1 sorts after string2 lexicographically.`arg1 OP arg2`

`OP` is one of ‘-eq’, ‘-ne’, ‘-lt’, ‘-le’, ‘-gt’, or ‘-ge’. These arithmetic binary operators return true if arg1 is equal to, not equal to, less than, less than or equal to, greater than, or greater than or equal to arg2, respectively. Arg1 and arg2 may be positive or negative integers. When used with the `[[` command, Arg1 and Arg2 are evaluated as arithmetic expressions \(see [Shell Arithmetic](shell-arithmetic-bash-reference-manual.md#Shell-Arithmetic)\).

