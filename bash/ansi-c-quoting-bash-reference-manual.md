# ANSI-C Quoting \(Bash Reference Manual\)

## 3.1.2.4 ANSI-C Quoting

Words of the form `$'string'` are treated specially. The word expands to string, with backslash-escaped characters replaced as specified by the ANSI C standard. Backslash escape sequences, if present, are decoded as follows:`\a`

alert \(bell\)`\b`

backspace`\e\E`

an escape character \(not ANSI C\)`\f`

form feed`\n`

newline`\r`

carriage return`\t`

horizontal tab`\v`

vertical tab`\\`

backslash`\'`

single quote`\"`

double quote`\?`

question mark`\nnn`

the eight-bit character whose value is the octal value nnn \(one to three octal digits\)`\xHH`

the eight-bit character whose value is the hexadecimal value HH \(one or two hex digits\)`\uHHHH`

the Unicode \(ISO/IEC 10646\) character whose value is the hexadecimal value HHHH \(one to four hex digits\)`\UHHHHHHHH`

the Unicode \(ISO/IEC 10646\) character whose value is the hexadecimal value HHHHHHHH \(one to eight hex digits\)`\cx`

a control-x character

The expanded result is single-quoted, as if the dollar sign had not been present.

