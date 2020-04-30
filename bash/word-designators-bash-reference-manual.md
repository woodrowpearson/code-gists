# Word Designators \(Bash Reference Manual\)

## 9.3.2 Word Designators

Word designators are used to select desired words from the event. A ‘:’ separates the event specification from the word designator. It may be omitted if the word designator begins with a ‘^’, ‘$’, ‘\*’, ‘-’, or ‘%’. Words are numbered from the beginning of the line, with the first word being denoted by 0 \(zero\). Words are inserted into the current line separated by single spaces.

For example,`!!`

designates the preceding command. When you type this, the preceding command is repeated in toto.`!!:$`

designates the last argument of the preceding command. This may be shortened to `!$`.`!fi:2`

designates the second argument of the most recent command starting with the letters `fi`.

Here are the word designators:`0 (zero)`

The `0`th word. For many applications, this is the command word.`n`

The nth word.`^`

The first argument; that is, word 1.`$`

The last argument.`%`

The word matched by the most recent ‘?string?’ search.`x-y`

A range of words; ‘-y’ abbreviates ‘0-y’.`*`

All of the words, except the `0`th. This is a synonym for ‘1-$’. It is not an error to use ‘\*’ if there is just one word in the event; the empty string is returned in that case.`x*`

Abbreviates ‘x-$’`x-`

Abbreviates ‘x-$’ like ‘x\*’, but omits the last word.

If a word designator is supplied without an event specification, the previous command is used as the event.

