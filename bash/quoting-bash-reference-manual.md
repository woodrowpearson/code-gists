# Quoting \(Bash Reference Manual\)

## 3.1.2 Quoting

Quoting is used to remove the special meaning of certain characters or words to the shell. Quoting can be used to disable special treatment for special characters, to prevent reserved words from being recognized as such, and to prevent parameter expansion.

Each of the shell metacharacters \(see [Definitions](definitions-bash-reference-manual.md#Definitions)\) has special meaning to the shell and must be quoted if it is to represent itself. When the command history expansion facilities are being used \(see [History Interaction](history-interaction-bash-reference-manual.md#History-Interaction)\), the history expansion character, usually ‘!’, must be quoted to prevent history expansion. See [Bash History Facilities](bash-history-facilities-bash-reference-manual.md#Bash-History-Facilities), for more details concerning history expansion.

There are three quoting mechanisms: the escape character, single quotes, and double quotes.

