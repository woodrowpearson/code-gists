# Modifiers \(Bash Reference Manual\)

After the optional word designator, you can add a sequence of one or more of the following modifiers, each preceded by a ‘:’.`h`

Remove a trailing pathname component, leaving only the head.`t`

Remove all leading pathname components, leaving the tail.`r`

Remove a trailing suffix of the form ‘.suffix’, leaving the basename.`e`

Remove all but the trailing suffix.`p`

Print the new command but do not execute it.`q`

Quote the substituted words, escaping further substitutions.`x`

Quote the substituted words as with ‘q’, but break into words at spaces, tabs, and newlines.`s/old/new/`

Substitute new for the first occurrence of old in the event line. Any delimiter may be used in place of ‘/’. The delimiter may be quoted in old and new with a single backslash. If ‘&’ appears in new, it is replaced by old. A single backslash will quote the ‘&’. The final delimiter is optional if it is the last character on the input line.`&`

Repeat the previous substitution.`ga`

Cause changes to be applied over the entire event line. Used in conjunction with ‘s’, as in `gs/old/new/`, or with ‘&’.`G`

Apply the following ‘s’ modifier once to each word in the event.

