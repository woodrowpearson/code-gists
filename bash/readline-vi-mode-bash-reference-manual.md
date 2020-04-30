# Readline vi Mode \(Bash Reference Manual\)

## 8.5 Readline vi Mode

While the Readline library does not have a full set of `vi` editing functions, it does contain enough to allow simple editing of the line. The Readline `vi` mode behaves as specified in the POSIX standard.

In order to switch interactively between `emacs` and `vi` editing modes, use the ‘set -o emacs’ and ‘set -o vi’ commands \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\). The Readline default is `emacs` mode.

When you enter a line in `vi` mode, you are already placed in ‘insertion’ mode, as if you had typed an ‘i’. Pressing ESC switches you into ‘command’ mode, where you can edit the text of the line with the standard `vi` movement keys, move to previous history lines with ‘k’ and subsequent lines with ‘j’, and so forth.

