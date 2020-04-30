# Commands For Moving \(Bash Reference Manual\)

`beginning-of-line (C-a)`

Move to the start of the current line.`end-of-line (C-e)`

Move to the end of the line.`forward-char (C-f)`

Move forward a character.`backward-char (C-b)`

Move back a character.`forward-word (M-f)`

Move forward to the end of the next word. Words are composed of letters and digits.`backward-word (M-b)`

Move back to the start of the current or previous word. Words are composed of letters and digits.`shell-forward-word ()`

Move forward to the end of the next word. Words are delimited by non-quoted shell metacharacters.`shell-backward-word ()`

Move back to the start of the current or previous word. Words are delimited by non-quoted shell metacharacters.`previous-screen-line ()`

Attempt to move point to the same physical screen column on the previous physical screen line. This will not have the desired effect if the current Readline line does not take up more than one physical line or if point is not greater than the length of the prompt plus the screen width.`next-screen-line ()`

Attempt to move point to the same physical screen column on the next physical screen line. This will not have the desired effect if the current Readline line does not take up more than one physical line or if the length of the current Readline line is not greater than the length of the prompt plus the screen width.`clear-screen (C-l)`

Clear the screen and redraw the current line, leaving the current line at the top of the screen.`redraw-current-line ()`

Refresh the current line. By default, this is unbound.

