# Major Differences From The Bourne Shell \(Bash Reference Manual\)

## Appendix B Major Differences From The Bourne Shell

Bash implements essentially the same grammar, parameter and variable expansion, redirection, and quoting as the Bourne Shell. Bash uses the POSIX standard as the specification of how these features are to be implemented. There are some differences between the traditional Bourne shell and Bash; this section quickly details the differences of significance. A number of these differences are explained in greater depth in previous sections. This section uses the version of `sh` included in SVR4.2 \(the last version of the historical Bourne shell\) as the baseline reference.

*  Bash is POSIX-conformant, even where the POSIX specification differs from traditional `sh` behavior \(see [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode)\).
*  Bash has multi-character invocation options \(see [Invoking Bash](invoking-bash-bash-reference-manual.md#Invoking-Bash)\).
*  Bash has command-line editing \(see [Command Line Editing](command-line-editing-bash-reference-manual.md#Command-Line-Editing)\) and the `bind` builtin.
*  Bash provides a programmable word completion mechanism \(see [Programmable Completion](programmable-completion-bash-reference-manual.md#Programmable-Completion)\), and builtin commands `complete`, `compgen`, and `compopt`, to manipulate it.
*  Bash has command history \(see [Bash History Facilities](bash-history-facilities-bash-reference-manual.md#Bash-History-Facilities)\) and the `history` and `fc` builtins to manipulate it. The Bash history list maintains timestamp information and uses the value of the `HISTTIMEFORMAT` variable to display it.
*  Bash implements `csh`-like history expansion \(see [History Interaction](history-interaction-bash-reference-manual.md#History-Interaction)\).
*  Bash has one-dimensional array variables \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\), and the appropriate variable expansions and assignment syntax to use them. Several of the Bash builtins take options to act on arrays. Bash provides a number of built-in array variables.
*  The `$'…'` quoting syntax, which expands ANSI-C backslash-escaped characters in the text between the single quotes, is supported \(see [ANSI-C Quoting](ansi-c-quoting-bash-reference-manual.md#ANSI_002dC-Quoting)\).
*  Bash supports the `$"…"` quoting syntax to do locale-specific translation of the characters between the double quotes. The -D, --dump-strings, and --dump-po-strings invocation options list the translatable strings found in a script \(see [Locale Translation](locale-translation-bash-reference-manual.md#Locale-Translation)\).
*  Bash implements the `!` keyword to negate the return value of a pipeline \(see [Pipelines](pipelines-bash-reference-manual.md#Pipelines)\). Very useful when an `if` statement needs to act only if a test fails. The Bash ‘-o pipefail’ option to `set` will cause a pipeline to return a failure status if any command fails.
*  Bash has the `time` reserved word and command timing \(see [Pipelines](pipelines-bash-reference-manual.md#Pipelines)\). The display of the timing statistics may be controlled with the `TIMEFORMAT` variable.
*  Bash implements the `for (( expr1 ; expr2 ; expr3 ))` arithmetic for command, similar to the C language \(see [Looping Constructs](looping-constructs-bash-reference-manual.md#Looping-Constructs)\).
*  Bash includes the `select` compound command, which allows the generation of simple menus \(see [Conditional Constructs](conditional-constructs-bash-reference-manual.md#Conditional-Constructs)\).
*  Bash includes the `[[` compound command, which makes conditional testing part of the shell grammar \(see [Conditional Constructs](conditional-constructs-bash-reference-manual.md#Conditional-Constructs)\), including optional regular expression matching.
*  Bash provides optional case-insensitive matching for the `case` and `[[` constructs.
*  Bash includes brace expansion \(see [Brace Expansion](brace-expansion-bash-reference-manual.md#Brace-Expansion)\) and tilde expansion \(see [Tilde Expansion](tilde-expansion-bash-reference-manual.md#Tilde-Expansion)\).
*  Bash implements command aliases and the `alias` and `unalias` builtins \(see [Aliases](aliases-bash-reference-manual.md#Aliases)\).
*  Bash provides shell arithmetic, the `((` compound command \(see [Conditional Constructs](conditional-constructs-bash-reference-manual.md#Conditional-Constructs)\), and arithmetic expansion \(see [Shell Arithmetic](shell-arithmetic-bash-reference-manual.md#Shell-Arithmetic)\).
*  Variables present in the shell’s initial environment are automatically exported to child processes. The Bourne shell does not normally do this unless the variables are explicitly marked using the `export` command.
*  Bash supports the ‘+=’ assignment operator, which appends to the value of the variable named on the left hand side.
*  Bash includes the POSIX pattern removal ‘%’, ‘\#’, ‘%%’ and ‘\#\#’ expansions to remove leading or trailing substrings from variable values \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
*  The expansion `${#xx}`, which returns the length of `${xx}`, is supported \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
*  The expansion `${var:`offset`[:`length`]}`, which expands to the substring of `var`’s value of length length, beginning at offset, is present \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
*  The expansion `${var/[/]`pattern`[/`replacement`]}`, which matches pattern and replaces it with replacement in the value of `var`, is available \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
*  The expansion `${!prefix*}` expansion, which expands to the names of all shell variables whose names begin with prefix, is available \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
*  Bash has indirect variable expansion using `${!word}` \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\).
*  Bash can expand positional parameters beyond `$9` using `${num}`.
*  The POSIX `$()` form of command substitution is implemented \(see [Command Substitution](command-substitution-bash-reference-manual.md#Command-Substitution)\), and preferred to the Bourne shell’s ```````` \(which is also implemented for backwards compatibility\).
*  Bash has process substitution \(see [Process Substitution](process-substitution-bash-reference-manual.md#Process-Substitution)\).
*  Bash automatically assigns variables that provide information about the current user \(`UID`, `EUID`, and `GROUPS`\), the current host \(`HOSTTYPE`, `OSTYPE`, `MACHTYPE`, and `HOSTNAME`\), and the instance of Bash that is running \(`BASH`, `BASH_VERSION`, and `BASH_VERSINFO`\). See [Bash Variables](bash-variables-bash-reference-manual.md#Bash-Variables), for details.
*  The `IFS` variable is used to split only the results of expansion, not all words \(see [Word Splitting](word-splitting-bash-reference-manual.md#Word-Splitting)\). This closes a longstanding shell security hole.
*  The filename expansion bracket expression code uses ‘!’ and ‘^’ to negate the set of characters between the brackets. The Bourne shell uses only ‘!’.
*  Bash implements the full set of POSIX filename expansion operators, including character classes, equivalence classes, and collating symbols \(see [Filename Expansion](filename-expansion-bash-reference-manual.md#Filename-Expansion)\).
*  Bash implements extended pattern matching features when the `extglob` shell option is enabled \(see [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching)\).
*  It is possible to have a variable and a function with the same name; `sh` does not separate the two name spaces.
*  Bash functions are permitted to have local variables using the `local` builtin, and thus useful recursive functions may be written \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  Variable assignments preceding commands affect only that command, even builtins and functions \(see [Environment](environment-bash-reference-manual.md#Environment)\). In `sh`, all variable assignments preceding commands are global unless the command is executed from the file system.
*  Bash performs filename expansion on filenames specified as operands to input and output redirection operators \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\).
*  Bash contains the ‘&lt;&gt;’ redirection operator, allowing a file to be opened for both reading and writing, and the ‘&&gt;’ redirection operator, for directing standard output and standard error to the same file \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\).
*  Bash includes the ‘&lt;&lt;&lt;’ redirection operator, allowing a string to be used as the standard input to a command.
*  Bash implements the ‘\[n\]&lt;&word’ and ‘\[n\]&gt;&word’ redirection operators, which move one file descriptor to another.
*  Bash treats a number of filenames specially when they are used in redirection operators \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\).
*  Bash can open network connections to arbitrary machines and services with the redirection operators \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\).
*  The `noclobber` option is available to avoid overwriting existing files with output redirection \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\). The ‘&gt;\|’ redirection operator may be used to override `noclobber`.
*  The Bash `cd` and `pwd` builtins \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\) each take -L and -P options to switch between logical and physical modes.
*  Bash allows a function to override a builtin with the same name, and provides access to that builtin’s functionality within the function via the `builtin` and `command` builtins \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  The `command` builtin allows selective disabling of functions when command lookup is performed \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  Individual builtins may be enabled or disabled using the `enable` builtin \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  The Bash `exec` builtin takes additional options that allow users to control the contents of the environment passed to the executed command, and what the zeroth argument to the command is to be \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).
*  Shell functions may be exported to children via the environment using `export -f` \(see [Shell Functions](shell-functions-bash-reference-manual.md#Shell-Functions)\).
*  The Bash `export`, `readonly`, and `declare` builtins can take a -f option to act on shell functions, a -p option to display variables with various attributes set in a format that can be used as shell input, a -n option to remove various variable attributes, and ‘name=value’ arguments to set variable attributes and values simultaneously.
*  The Bash `hash` builtin allows a name to be associated with an arbitrary filename, even when that filename cannot be found by searching the `$PATH`, using ‘hash -p’ \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).
*  Bash includes a `help` builtin for quick reference to shell facilities \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  The `printf` builtin is available to display formatted output \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  The Bash `read` builtin \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\) will read a line ending in ‘\’ with the -r option, and will use the `REPLY` variable as a default if no non-option arguments are supplied. The Bash `read` builtin also accepts a prompt string with the -p option and will use Readline to obtain the line when given the -e option. The `read` builtin also has additional options to control input: the -s option will turn off echoing of input characters as they are read, the -t option will allow `read` to time out if input does not arrive within a specified number of seconds, the -n option will allow reading only a specified number of characters rather than a full line, and the -d option will read until a particular character rather than newline.
*  The `return` builtin may be used to abort execution of scripts executed with the `.` or `source` builtins \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).
*  Bash includes the `shopt` builtin, for finer control of shell optional capabilities \(see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\), and allows these options to be set and unset at shell invocation \(see [Invoking Bash](invoking-bash-bash-reference-manual.md#Invoking-Bash)\).
*  Bash has much more optional behavior controllable with the `set` builtin \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\).
*  The ‘-x’ \(xtrace\) option displays commands other than simple commands when performing an execution trace \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\).
*  The `test` builtin \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\) is slightly different, as it implements the POSIX algorithm, which specifies the behavior based on the number of arguments.
*  Bash includes the `caller` builtin, which displays the context of any active subroutine call \(a shell function or a script executed with the `.` or `source` builtins\). This supports the bash debugger.
*  The `trap` builtin \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\) allows a `DEBUG` pseudo-signal specification, similar to `EXIT`. Commands specified with a `DEBUG` trap are executed before every simple command, `for` command, `case` command, `select` command, every arithmetic `for` command, and before the first command executes in a shell function. The `DEBUG` trap is not inherited by shell functions unless the function has been given the `trace` attribute or the `functrace` option has been enabled using the `shopt` builtin. The `extdebug` shell option has additional effects on the `DEBUG` trap.

  The `trap` builtin \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\) allows an `ERR` pseudo-signal specification, similar to `EXIT` and `DEBUG`. Commands specified with an `ERR` trap are executed after a simple command fails, with a few exceptions. The `ERR` trap is not inherited by shell functions unless the `-o errtrace` option to the `set` builtin is enabled.

  The `trap` builtin \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\) allows a `RETURN` pseudo-signal specification, similar to `EXIT` and `DEBUG`. Commands specified with an `RETURN` trap are executed before execution resumes after a shell function or a shell script executed with `.` or `source` returns. The `RETURN` trap is not inherited by shell functions unless the function has been given the `trace` attribute or the `functrace` option has been enabled using the `shopt` builtin.

*  The Bash `type` builtin is more extensive and gives more information about the names it finds \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\).
*  The Bash `umask` builtin permits a -p option to cause the output to be displayed in the form of a `umask` command that may be reused as input \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).
*  Bash implements a `csh`-like directory stack, and provides the `pushd`, `popd`, and `dirs` builtins to manipulate it \(see [The Directory Stack](the-directory-stack-bash-reference-manual.md#The-Directory-Stack)\). Bash also makes the directory stack visible as the value of the `DIRSTACK` shell variable.
*  Bash interprets special backslash-escaped characters in the prompt strings when interactive \(see [Controlling the Prompt](controlling-the-prompt-bash-reference-manual.md#Controlling-the-Prompt)\).
*  The Bash restricted mode is more useful \(see [The Restricted Shell](the-restricted-shell-bash-reference-manual.md#The-Restricted-Shell)\); the SVR4.2 shell restricted mode is too limited.
*  The `disown` builtin can remove a job from the internal shell job table \(see [Job Control Builtins](job-control-builtins-bash-reference-manual.md#Job-Control-Builtins)\) or suppress the sending of `SIGHUP` to a job when the shell exits as the result of a `SIGHUP`.
*  Bash includes a number of features to support a separate debugger for shell scripts.
*  The SVR4.2 shell has two privilege-related builtins \(`mldmode` and `priv`\) not present in Bash.
*  Bash does not have the `stop` or `newgrp` builtins.
*  Bash does not use the `SHACCT` variable or perform shell accounting.
*  The SVR4.2 `sh` uses a `TIMEOUT` variable like Bash uses `TMOUT`.

More features unique to Bash may be found in [Bash Features](bash-features-bash-reference-manual.md#Bash-Features).

### B.1 Implementation Differences From The SVR4.2 Shell

Since Bash is a completely new implementation, it does not suffer from many of the limitations of the SVR4.2 shell. For instance:

*  Bash does not fork a subshell when redirecting into or out of a shell control structure such as an `if` or `while` statement.
*  Bash does not allow unbalanced quotes. The SVR4.2 shell will silently insert a needed closing quote at `EOF` under certain circumstances. This can be the cause of some hard-to-find errors.
*  The SVR4.2 shell uses a baroque memory management scheme based on trapping `SIGSEGV`. If the shell is started from a process with `SIGSEGV` blocked \(e.g., by using the `system()` C library function call\), it misbehaves badly.
*  In a questionable attempt at security, the SVR4.2 shell, when invoked without the -p option, will alter its real and effective UID and GID if they are less than some magic threshold value, commonly 100. This can lead to unexpected results.
*  The SVR4.2 shell does not allow users to trap `SIGSEGV`, `SIGALRM`, or `SIGCHLD`.
*  The SVR4.2 shell does not allow the `IFS`, `MAILCHECK`, `PATH`, `PS1`, or `PS2` variables to be unset.
*  The SVR4.2 shell treats ‘^’ as the undocumented equivalent of ‘\|’.
*  Bash allows multiple option arguments when it is invoked \(`-x -v`\); the SVR4.2 shell allows only one option argument \(`-xv`\). In fact, some versions of the shell dump core if the second argument begins with a ‘-’.
*  The SVR4.2 shell exits a script if any builtin fails; Bash exits a script only if one of the POSIX special builtins fails, and only for certain failures, as enumerated in the POSIX standard.
*  The SVR4.2 shell behaves differently when invoked as `jsh` \(it turns on job control\).

