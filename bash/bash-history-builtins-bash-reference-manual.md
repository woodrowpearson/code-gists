# Bash History Builtins \(Bash Reference Manual\)

```text
fc [-e ename] [-lnr] [first] [last]
fc -s [pat=rep] [command]
```

The first form selects a range of commands from first to last from the history list and displays or edits and re-executes them. Both first and last may be specified as a string \(to locate the most recent command beginning with that string\) or as a number \(an index into the history list, where a negative number is used as an offset from the current command number\). If last is not specified, it is set to first. If first is not specified, it is set to the previous command for editing and -16 for listing. If the -l flag is given, the commands are listed on standard output. The -n flag suppresses the command numbers when listing. The -r flag reverses the order of the listing. Otherwise, the editor given by ename is invoked on a file containing those commands. If ename is not given, the value of the following variable expansion is used: `${FCEDIT:-${EDITOR:-vi}}`. This says to use the value of the `FCEDIT` variable if set, or the value of the `EDITOR` variable if that is set, or `vi` if neither is set. When editing is complete, the edited commands are echoed and executed.

In the second form, command is re-executed after each instance of pat in the selected command is replaced by rep. command is intepreted the same as first above.

A useful alias to use with the `fc` command is `r='fc -s'`, so that typing ‘r cc’ runs the last command beginning with `cc` and typing ‘r’ re-executes the last command \(see [Aliases](aliases-bash-reference-manual.md#Aliases)\).

```text
history [n]
history -c
history -d offset
history -d start-end
history [-anrw] [filename]
history -ps arg
```

With no options, display the history list with line numbers. Lines prefixed with a ‘\*’ have been modified. An argument of n lists only the last n lines. If the shell variable `HISTTIMEFORMAT` is set and not null, it is used as a format string for strftime to display the time stamp associated with each displayed history entry. No intervening blank is printed between the formatted time stamp and the history line.

Options, if supplied, have the following meanings:`-c`

Clear the history list. This may be combined with the other options to replace the history list completely.`-d offset`

Delete the history entry at position offset. If offset is positive, it should be specified as it appears when the history is displayed. If offset is negative, it is interpreted as relative to one greater than the last history position, so negative indices count back from the end of the history, and an index of ‘-1’ refers to the current `history -d` command.`-d start-end`

Delete the history entries between positions start and end, inclusive. Positive and negative values for start and end are interpreted as described above.`-a`

Append the new history lines to the history file. These are history lines entered since the beginning of the current Bash session, but not already appended to the history file.`-n`

Append the history lines not already read from the history file to the current history list. These are lines appended to the history file since the beginning of the current Bash session.`-r`

Read the history file and append its contents to the history list.`-w`

Write out the current history list to the history file.`-p`

Perform history substitution on the args and display the result on the standard output, without storing the results in the history list.`-s`

The args are added to the end of the history list as a single entry.

When any of the -w, -r, -a, or -n options is used, if filename is given, then it is used as the history file. If not, then the value of the `HISTFILE` variable is used.

