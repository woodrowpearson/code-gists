# Readline Bare Essentials \(Bash Reference Manual\)

## 8.2.1 Readline Bare Essentials

In order to enter characters into the line, simply type them. The typed character appears where the cursor was, and then the cursor moves one space to the right. If you mistype a character, you can use your erase character to back up and delete the mistyped character.

Sometimes you may mistype a character, and not notice the error until you have typed several other characters. In that case, you can type C-b to move the cursor to the left, and then correct your mistake. Afterwards, you can move the cursor to the right with C-f.

When you add text in the middle of a line, you will notice that characters to the right of the cursor are ‘pushed over’ to make room for the text that you have inserted. Likewise, when you delete text behind the cursor, characters to the right of the cursor are ‘pulled back’ to fill in the blank space created by the removal of the text. A list of the bare essentials for editing the text of an input line follows.C-b

Move back one character.C-f

Move forward one character.DEL or Backspace

Delete the character to the left of the cursor.C-d

Delete the character underneath the cursor.Printing characters

Insert the character into the line at the cursor.C-\_ or C-x C-u

Undo the last editing command. You can undo all the way back to an empty line.

\(Depending on your configuration, the Backspace key be set to delete the character to the left of the cursor and the DEL key set to delete the character underneath the cursor, like C-d, rather than the character to the left of the cursor.\)

