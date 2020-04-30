# Is this Shell Interactive? \(Bash Reference Manual\)

## 6.3.2 Is this Shell Interactive?

To determine within a startup script whether or not Bash is running interactively, test the value of the ‘-’ special parameter. It contains `i` when the shell is interactive. For example:

```text
case "$-" in
*i*)	echo This shell is interactive ;;
*)	echo This shell is not interactive ;;
esac
```

Alternatively, startup scripts may examine the variable `PS1`; it is unset in non-interactive shells, and set in interactive shells. Thus:

```text
if [ -z "$PS1" ]; then
        echo This shell is not interactive
else
        echo This shell is interactive
fi
```

