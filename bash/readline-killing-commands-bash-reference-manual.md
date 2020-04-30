# Readline Killing Commands \(Bash Reference Manual\)

## 8.2.3 Readline Killing Commands

_Killing_ text means to delete the text from the line, but to save it away for later use, usually by _yanking_ \(re-inserting\) it back into the line. \(‘Cut’ and ‘paste’ are more recent jargon for ‘kill’ and ‘yank’.\)

If the description for a command says that it ‘kills’ text, then you can be sure that you can get the text back in a different \(or the same\) place later.

When you use a kill command, the text is saved in a _kill-ring_. Any number of consecutive kills save all of the killed text together, so that when you yank it back, you get it all. The kill ring is not line specific; the text that you killed on a previously typed line is available to be yanked back later, when you are typing another line.

Here is the list of commands for killing text.C-k

Kill the text from the current cursor position to the end of the line.M-d

Kill from the cursor to the end of the current word, or, if between words, to the end of the next word. Word boundaries are the same as those used by M-f.M-DEL

Kill from the cursor the start of the current word, or, if between words, to the start of the previous word. Word boundaries are the same as those used by M-b.C-w

Kill from the cursor to the previous whitespace. This is different than M-DEL because the word boundaries differ.

Here is how to _yank_ the text back into the line. Yanking means to copy the most-recently-killed text from the kill buffer.C-y

Yank the most recently killed text back into the buffer at the cursor.M-y

Rotate the kill-ring, and yank the new top. You can only do this if the prior command is C-y or M-y.

