# Invoking Bash \(Bash Reference Manual\)

## 6.1 Invoking Bash

```text
bash [long-opt] [-ir] [-abefhkmnptuvxdBCDHP] [-o option]
    [-O shopt_option] [argument …]
bash [long-opt] [-abefhkmnptuvxdBCDHP] [-o option]
    [-O shopt_option] -c string [argument …]
bash [long-opt] -s [-abefhkmnptuvxdBCDHP] [-o option]
    [-O shopt_option] [argument …]
```

All of the single-character options used with the `set` builtin \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\) can be used as options when the shell is invoked. In addition, there are several multi-character options that you can use. These options must appear on the command line before the single-character options to be recognized.`--debugger`

Arrange for the debugger profile to be executed before the shell starts. Turns on extended debugging mode \(see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin) for a description of the `extdebug` option to the `shopt` builtin\).`--dump-po-strings`

A list of all double-quoted strings preceded by ‘$’ is printed on the standard output in the GNU `gettext` PO \(portable object\) file format. Equivalent to -D except for the output format.`--dump-strings`

Equivalent to -D.`--help`

Display a usage message on standard output and exit successfully.`--init-file filename--rcfile filename`

Execute commands from filename \(instead of ~/.bashrc\) in an interactive shell.`--login`

Equivalent to -l.`--noediting`

Do not use the GNU Readline library \(see [Command Line Editing](command-line-editing-bash-reference-manual.md#Command-Line-Editing)\) to read command lines when the shell is interactive.`--noprofile`

Don’t load the system-wide startup file /etc/profile or any of the personal initialization files ~/.bash\_profile, ~/.bash\_login, or ~/.profile when Bash is invoked as a login shell.`--norc`

Don’t read the ~/.bashrc initialization file in an interactive shell. This is on by default if the shell is invoked as `sh`.`--posix`

Change the behavior of Bash where the default operation differs from the POSIX standard to match the standard. This is intended to make Bash behave as a strict superset of that standard. See [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode), for a description of the Bash POSIX mode.`--restricted`

Make the shell a restricted shell \(see [The Restricted Shell](the-restricted-shell-bash-reference-manual.md#The-Restricted-Shell)\).`--verbose`

Equivalent to -v. Print shell input lines as they’re read.`--version`

Show version information for this instance of Bash on the standard output and exit successfully.

There are several single-character options that may be supplied at invocation which are not available with the `set` builtin.`-c`

Read and execute commands from the first non-option argument command\_string, then exit. If there are arguments after the command\_string, the first argument is assigned to `$0` and any remaining arguments are assigned to the positional parameters. The assignment to `$0` sets the name of the shell, which is used in warning and error messages.`-i`

Force the shell to run interactively. Interactive shells are described in [Interactive Shells](interactive-shells-bash-reference-manual.md#Interactive-Shells).`-l`

Make this shell act as if it had been directly invoked by login. When the shell is interactive, this is equivalent to starting a login shell with ‘exec -l bash’. When the shell is not interactive, the login shell startup files will be executed. ‘exec bash -l’ or ‘exec bash --login’ will replace the current shell with a Bash login shell. See [Bash Startup Files](bash-startup-files-bash-reference-manual.md#Bash-Startup-Files), for a description of the special behavior of a login shell.`-r`

Make the shell a restricted shell \(see [The Restricted Shell](the-restricted-shell-bash-reference-manual.md#The-Restricted-Shell)\).`-s`

If this option is present, or if no arguments remain after option processing, then commands are read from the standard input. This option allows the positional parameters to be set when invoking an interactive shell or when reading input through a pipe.`-D`

A list of all double-quoted strings preceded by ‘$’ is printed on the standard output. These are the strings that are subject to language translation when the current locale is not `C` or `POSIX` \(see [Locale Translation](locale-translation-bash-reference-manual.md#Locale-Translation)\). This implies the -n option; no commands will be executed.`[-+]O [shopt_option]`

shopt\_option is one of the shell options accepted by the `shopt` builtin \(see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\). If shopt\_option is present, -O sets the value of that option; +O unsets it. If shopt\_option is not supplied, the names and values of the shell options accepted by `shopt` are printed on the standard output. If the invocation option is +O, the output is displayed in a format that may be reused as input.`--`

A `--` signals the end of options and disables further option processing. Any arguments after the `--` are treated as filenames and arguments.

A _login_ shell is one whose first character of argument zero is ‘-’, or one invoked with the --login option.

An _interactive_ shell is one started without non-option arguments, unless -s is specified, without specifying the -c option, and whose input and output are both connected to terminals \(as determined by `isatty(3)`\), or one started with the -i option. See [Interactive Shells](interactive-shells-bash-reference-manual.md#Interactive-Shells), for more information.

If arguments remain after option processing, and neither the -c nor the -s option has been supplied, the first argument is assumed to be the name of a file containing shell commands \(see [Shell Scripts](shell-scripts-bash-reference-manual.md#Shell-Scripts)\). When Bash is invoked in this fashion, `$0` is set to the name of the file, and the positional parameters are set to the remaining arguments. Bash reads and executes commands from this file, then exits. Bash’s exit status is the exit status of the last command executed in the script. If no commands are executed, the exit status is 0.

