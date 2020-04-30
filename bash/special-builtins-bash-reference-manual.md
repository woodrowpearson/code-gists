# Special Builtins \(Bash Reference Manual\)

## 4.4 Special Builtins

For historical reasons, the POSIX standard has classified several builtin commands as _special_. When Bash is executing in POSIX mode, the special builtins differ from other builtin commands in three respects:

1.  Special builtins are found before shell functions during command lookup.
2.  If a special builtin returns an error status, a non-interactive shell exits.
3.  Assignment statements preceding the command stay in effect in the shell environment after the command completes.

When Bash is not executing in POSIX mode, these builtins behave no differently than the rest of the Bash builtin commands. The Bash POSIX mode is described in [Bash POSIX Mode](bash-posix-mode-bash-reference-manual.md#Bash-POSIX-Mode).

These are the POSIX special builtins:

```text
break : . continue eval exec exit export readonly return set
shift trap unset
```

