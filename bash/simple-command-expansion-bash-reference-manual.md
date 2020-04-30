# Simple Command Expansion \(Bash Reference Manual\)

## 3.7.1 Simple Command Expansion

When a simple command is executed, the shell performs the following expansions, assignments, and redirections, from left to right.

1.  The words that the parser has marked as variable assignments \(those preceding the command name\) and redirections are saved for later processing.
2.  The words that are not variable assignments or redirections are expanded \(see [Shell Expansions](shell-expansions-bash-reference-manual.md#Shell-Expansions)\). If any words remain after expansion, the first word is taken to be the name of the command and the remaining words are the arguments.
3.  Redirections are performed as described above \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\).
4.  The text after the ‘=’ in each variable assignment undergoes tilde expansion, parameter expansion, command substitution, arithmetic expansion, and quote removal before being assigned to the variable.

If no command name results, the variable assignments affect the current shell environment. Otherwise, the variables are added to the environment of the executed command and do not affect the current shell environment. If any of the assignments attempts to assign a value to a readonly variable, an error occurs, and the command exits with a non-zero status.

If no command name results, redirections are performed, but do not affect the current shell environment. A redirection error causes the command to exit with a non-zero status.

If there is a command name left after expansion, execution proceeds as described below. Otherwise, the command exits. If one of the expansions contained a command substitution, the exit status of the command is the exit status of the last command substitution performed. If there were no command substitutions, the command exits with a status of zero.

