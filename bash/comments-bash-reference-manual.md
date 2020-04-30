# Comments \(Bash Reference Manual\)

## 3.1.3 Comments

In a non-interactive shell, or an interactive shell in which the `interactive_comments` option to the `shopt` builtin is enabled \(see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\), a word beginning with ‘\#’ causes that word and all remaining characters on that line to be ignored. An interactive shell without the `interactive_comments` option enabled does not allow comments. The `interactive_comments` option is on by default in interactive shells. See [Interactive Shells](interactive-shells-bash-reference-manual.md#Interactive-Shells), for a description of what makes a shell interactive.

