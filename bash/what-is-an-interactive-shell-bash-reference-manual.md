# What is an Interactive Shell? \(Bash Reference Manual\)

 Next: [Is this Shell Interactive?](is-this-shell-interactive-bash-reference-manual.md#Is-this-Shell-Interactive_003f), Up: [Interactive Shells](interactive-shells-bash-reference-manual.md#Interactive-Shells)   \[[Contents]()\]\[[Index](indexes-bash-reference-manual.md#Indexes)\]

An interactive shell is one started without non-option arguments, unless -s is specified, without specifying the -c option, and whose input and error output are both connected to terminals \(as determined by `isatty(3)`\), or one started with the -i option.

An interactive shell generally reads from and writes to a user’s terminal.

The -s invocation option may be used to set the positional parameters when an interactive shell is started.

