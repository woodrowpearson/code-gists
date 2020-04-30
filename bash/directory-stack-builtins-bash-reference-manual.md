# Directory Stack Builtins \(Bash Reference Manual\)

```text
pushd [-n] [+N | -N | dir]
```

Save the current directory on the top of the directory stack and then `cd` to dir. With no arguments, `pushd` exchanges the top two directories and makes the new top the current directory.

