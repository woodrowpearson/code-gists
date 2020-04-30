# Escape Character \(Bash Reference Manual\)

 Next: [Single Quotes](single-quotes-bash-reference-manual.md#Single-Quotes), Up: [Quoting](quoting-bash-reference-manual.md#Quoting)   \[[Contents]()\]\[[Index](indexes-bash-reference-manual.md#Indexes)\]

A non-quoted backslash ‘\’ is the Bash escape character. It preserves the literal value of the next character that follows, with the exception of `newline`. If a `\newline` pair appears, and the backslash itself is not quoted, the `\newline` is treated as a line continuation \(that is, it is removed from the input stream and effectively ignored\).

