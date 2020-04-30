# Command Line Editing \(Bash Reference Manual\)

## 8 Command Line Editing

This chapter describes the basic features of the GNU command line editing interface. Command line editing is provided by the Readline library, which is used by several different programs, including Bash. Command line editing is enabled by default when using an interactive shell, unless the --noediting option is supplied at shell invocation. Line editing is also used when using the -e option to the `read` builtin command \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\). By default, the line editing commands are similar to those of Emacs. A vi-style line editing interface is also available. Line editing can be enabled at any time using the -o emacs or -o vi options to the `set` builtin command \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\), or disabled using the +o emacs or +o vi options to `set`.

