# Bindable Readline Commands \(Bash Reference Manual\)

## 8.4 Bindable Readline Commands

This section describes Readline commands that may be bound to key sequences. You can list your key bindings by executing `bind -P` or, for a more terse format, suitable for an inputrc file, `bind -p`. \(See [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins).\) Command names without an accompanying key sequence are unbound by default.

In the following descriptions, _point_ refers to the current cursor position, and _mark_ refers to a cursor position saved by the `set-mark` command. The text between the point and mark is referred to as the _region_.

