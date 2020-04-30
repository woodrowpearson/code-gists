# Commands For Text \(Bash Reference Manual\)

`end-of-file (usually C-d)`

The character indicating end-of-file as set, for example, by `stty`. If this character is read when there are no characters on the line, and point is at the beginning of the line, Readline interprets it as the end of input and returns EOF.`delete-char (C-d)`

Delete the character at point. If this function is bound to the same character as the tty EOF character, as C-d commonly is, see above for the effects.`backward-delete-char (Rubout)`

Delete the character behind the cursor. A numeric argument means to kill the characters instead of deleting them.`forward-backward-delete-char ()`

Delete the character under the cursor, unless the cursor is at the end of the line, in which case the character behind the cursor is deleted. By default, this is not bound to a key.`quoted-insert (C-q or C-v)`

Add the next character typed to the line verbatim. This is how to insert key sequences like C-q, for example.`self-insert (a, b, A, 1, !, …)`

Insert yourself.`bracketed-paste-begin ()`

This function is intended to be bound to the "bracketed paste" escape sequence sent by some terminals, and such a binding is assigned by default. It allows Readline to insert the pasted text as a single unit without treating each character as if it had been read from the keyboard. The characters are inserted as if each one was bound to `self-insert` instead of executing any editing commands.`transpose-chars (C-t)`

Drag the character before the cursor forward over the character at the cursor, moving the cursor forward as well. If the insertion point is at the end of the line, then this transposes the last two characters of the line. Negative arguments have no effect.`transpose-words (M-t)`

Drag the word before point past the word after point, moving point past that word as well. If the insertion point is at the end of the line, this transposes the last two words on the line.`upcase-word (M-u)`

Uppercase the current \(or following\) word. With a negative argument, uppercase the previous word, but do not move the cursor.`downcase-word (M-l)`

Lowercase the current \(or following\) word. With a negative argument, lowercase the previous word, but do not move the cursor.`capitalize-word (M-c)`

Capitalize the current \(or following\) word. With a negative argument, capitalize the previous word, but do not move the cursor.`overwrite-mode ()`

Toggle overwrite mode. With an explicit positive numeric argument, switches to overwrite mode. With an explicit non-positive numeric argument, switches to insert mode. This command affects only `emacs` mode; `vi` mode does overwrite differently. Each call to `readline()` starts in insert mode.

In overwrite mode, characters bound to `self-insert` replace the text at point rather than pushing the text to the right. Characters bound to `backward-delete-char` replace the character before point with a space.

By default, this command is unbound.

