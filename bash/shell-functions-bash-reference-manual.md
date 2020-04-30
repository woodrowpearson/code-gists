# Shell Functions \(Bash Reference Manual\)

## 3.3 Shell Functions

Shell functions are a way to group commands for later execution using a single name for the group. They are executed just like a "regular" command. When the name of a shell function is used as a simple command name, the list of commands associated with that function name is executed. Shell functions are executed in the current shell context; no new process is created to interpret them.

Functions are declared using this syntax:

```text
name () compound-command [ redirections ]
```

or

```text
function name [()] compound-command [ redirections ]
```

This defines a shell function named name. The reserved word `function` is optional. If the `function` reserved word is supplied, the parentheses are optional. The body of the function is the compound command compound-command \(see [Compound Commands](compound-commands-bash-reference-manual.md#Compound-Commands)\). That command is usually a list enclosed between { and }, but may be any compound command listed above, with one exception: If the `function` reserved word is used, but the parentheses are not supplied, the braces are required. compound-command is executed whenever name is specified as the name of a command. When the shell is in POSIX mode \(see [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode)\), name may not be the same as one of the special builtins \(see [Special Builtins](special-builtins-bash-reference-manual.md#Special-Builtins)\). Any redirections \(see [Redirections](redirections-bash-reference-manual.md#Redirections)\) associated with the shell function are performed when the function is executed.

A function definition may be deleted using the -f option to the `unset` builtin \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).

The exit status of a function definition is zero unless a syntax error occurs or a readonly function with the same name already exists. When executed, the exit status of a function is the exit status of the last command executed in the body.

Note that for historical reasons, in the most common usage the curly braces that surround the body of the function must be separated from the body by `blank`s or newlines. This is because the braces are reserved words and are only recognized as such when they are separated from the command list by whitespace or another shell metacharacter. Also, when using the braces, the list must be terminated by a semicolon, a ‘&’, or a newline.

When a function is executed, the arguments to the function become the positional parameters during its execution \(see [Positional Parameters](positional-parameters-bash-reference-manual.md#Positional-Parameters)\). The special parameter ‘\#’ that expands to the number of positional parameters is updated to reflect the change. Special parameter `0` is unchanged. The first element of the `FUNCNAME` variable is set to the name of the function while the function is executing.

All other aspects of the shell execution environment are identical between a function and its caller with these exceptions: the `DEBUG` and `RETURN` traps are not inherited unless the function has been given the `trace` attribute using the `declare` builtin or the `-o functrace` option has been enabled with the `set` builtin, \(in which case all functions inherit the `DEBUG` and `RETURN` traps\), and the `ERR` trap is not inherited unless the `-o errtrace` shell option has been enabled. See [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins), for the description of the `trap` builtin.

The `FUNCNEST` variable, if set to a numeric value greater than 0, defines a maximum function nesting level. Function invocations that exceed the limit cause the entire command to abort.

If the builtin command `return` is executed in a function, the function completes and execution resumes with the next command after the function call. Any command associated with the `RETURN` trap is executed before execution resumes. When a function completes, the values of the positional parameters and the special parameter ‘\#’ are restored to the values they had prior to the function’s execution. If a numeric argument is given to `return`, that is the function’s return status; otherwise the function’s return status is the exit status of the last command executed before the `return`.

Variables local to the function may be declared with the `local` builtin. These variables are visible only to the function and the commands it invokes. This is particularly important when a shell function calls other functions.

Local variables "shadow" variables with the same name declared at previous scopes. For instance, a local variable declared in a function hides a global variable of the same name: references and assignments refer to the local variable, leaving the global variable unmodified. When the function returns, the global variable is once again visible.

The shell uses dynamic scoping to control a variable’s visibility within functions. With dynamic scoping, visible variables and their values are a result of the sequence of function calls that caused execution to reach the current function. The value of a variable that a function sees depends on its value within its caller, if any, whether that caller is the "global" scope or another shell function. This is also the value that a local variable declaration "shadows", and the value that is restored when the function returns.

For example, if a variable var is declared as local in function func1, and func1 calls another function func2, references to var made from within func2 will resolve to the local variable var from func1, shadowing any global variable named var.

The following script demonstrates this behavior. When executed, the script displays

```text
In func2, var = func1 local
```

```text
func1()
{
    local var='func1 local'
    func2
}

func2()
{
    echo "In func2, var = $var"
}

var=global
func1
```

The `unset` builtin also acts using the same dynamic scope: if a variable is local to the current scope, `unset` will unset it; otherwise the unset will refer to the variable found in any calling scope as described above. If a variable at the current local scope is unset, it will remain so until it is reset in that scope or until the function returns. Once the function returns, any instance of the variable at a previous scope will become visible. If the unset acts on a variable at a previous scope, any instance of a variable with that name that had been shadowed will become visible.

Function names and definitions may be listed with the -f option to the `declare` \(`typeset`\) builtin command \(see [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins)\). The -F option to `declare` or `typeset` will list the function names only \(and optionally the source file and line number, if the `extdebug` shell option is enabled\). Functions may be exported so that subshells automatically have them defined with the -f option to the `export` builtin \(see [Bourne Shell Builtins](bourne-shell-builtins-bash-reference-manual.md#Bourne-Shell-Builtins)\).

Functions may be recursive. The `FUNCNEST` variable may be used to limit the depth of the function call stack and restrict the number of function invocations. By default, no limit is placed on the number of recursive calls.

