# Shell Parameter Expansion \(Bash Reference Manual\)

## 3.5.3 Shell Parameter Expansion

The ‘$’ character introduces parameter expansion, command substitution, or arithmetic expansion. The parameter name or symbol to be expanded may be enclosed in braces, which are optional but serve to protect the variable to be expanded from characters immediately following it which could be interpreted as part of the name.

When braces are used, the matching ending brace is the first ‘}’ not escaped by a backslash or within a quoted string, and not within an embedded arithmetic expansion, command substitution, or parameter expansion.

The basic form of parameter expansion is ${parameter}. The value of parameter is substituted. The parameter is a shell parameter as described above \(see [Shell Parameters](shell-parameters-bash-reference-manual.md#Shell-Parameters)\) or an array reference \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\). The braces are required when parameter is a positional parameter with more than one digit, or when parameter is followed by a character that is not to be interpreted as part of its name.

If the first character of parameter is an exclamation point \(!\), and parameter is not a nameref, it introduces a level of indirection. Bash uses the value formed by expanding the rest of parameter as the new parameter; this is then expanded and that value is used in the rest of the expansion, rather than the expansion of the original parameter. This is known as `indirect expansion`. The value is subject to tilde expansion, parameter expansion, command substitution, and arithmetic expansion. If parameter is a nameref, this expands to the name of the variable referenced by parameter instead of performing the complete indirect expansion. The exceptions to this are the expansions of ${!prefix\*} and ${!name\[@\]} described below. The exclamation point must immediately follow the left brace in order to introduce indirection.

In each of the cases below, word is subject to tilde expansion, parameter expansion, command substitution, and arithmetic expansion.

When not performing substring expansion, using the form described below \(e.g., ‘:-’\), Bash tests for a parameter that is unset or null. Omitting the colon results in a test only for a parameter that is unset. Put another way, if the colon is included, the operator tests for both parameter’s existence and that its value is not null; if the colon is omitted, the operator tests only for existence.`${parameter:-word}`

If parameter is unset or null, the expansion of word is substituted. Otherwise, the value of parameter is substituted.`${parameter:=word}`

If parameter is unset or null, the expansion of word is assigned to parameter. The value of parameter is then substituted. Positional parameters and special parameters may not be assigned to in this way.`${parameter:?word}`

If parameter is null or unset, the expansion of word \(or a message to that effect if word is not present\) is written to the standard error and the shell, if it is not interactive, exits. Otherwise, the value of parameter is substituted.`${parameter:+word}`

If parameter is null or unset, nothing is substituted, otherwise the expansion of word is substituted.`${parameter:offset}${parameter:offset:length}`

This is referred to as Substring Expansion. It expands to up to length characters of the value of parameter starting at the character specified by offset. If parameter is ‘@’, an indexed array subscripted by ‘@’ or ‘\*’, or an associative array name, the results differ as described below. If length is omitted, it expands to the substring of the value of parameter starting at the character specified by offset and extending to the end of the value. length and offset are arithmetic expressions \(see [Shell Arithmetic](shell-arithmetic-bash-reference-manual.md#Shell-Arithmetic)\).

If offset evaluates to a number less than zero, the value is used as an offset in characters from the end of the value of parameter. If length evaluates to a number less than zero, it is interpreted as an offset in characters from the end of the value of parameter rather than a number of characters, and the expansion is the characters between offset and that result. Note that a negative offset must be separated from the colon by at least one space to avoid being confused with the ‘:-’ expansion.

Here are some examples illustrating substring expansion on parameters and subscripted arrays:

```text
$ string=01234567890abcdefgh
$ echo ${string:7}
7890abcdefgh
$ echo ${string:7:0}

$ echo ${string:7:2}
78
$ echo ${string:7:-2}
7890abcdef
$ echo ${string: -7}
bcdefgh
$ echo ${string: -7:0}

$ echo ${string: -7:2}
bc
$ echo ${string: -7:-2}
bcdef
$ set -- 01234567890abcdefgh
$ echo ${1:7}
7890abcdefgh
$ echo ${1:7:0}

$ echo ${1:7:2}
78
$ echo ${1:7:-2}
7890abcdef
$ echo ${1: -7}
bcdefgh
$ echo ${1: -7:0}

$ echo ${1: -7:2}
bc
$ echo ${1: -7:-2}
bcdef
$ array[0]=01234567890abcdefgh
$ echo ${array[0]:7}
7890abcdefgh
$ echo ${array[0]:7:0}

$ echo ${array[0]:7:2}
78
$ echo ${array[0]:7:-2}
7890abcdef
$ echo ${array[0]: -7}
bcdefgh
$ echo ${array[0]: -7:0}

$ echo ${array[0]: -7:2}
bc
$ echo ${array[0]: -7:-2}
bcdef
```

If parameter is ‘@’, the result is length positional parameters beginning at offset. A negative offset is taken relative to one greater than the greatest positional parameter, so an offset of -1 evaluates to the last positional parameter. It is an expansion error if length evaluates to a number less than zero.

The following examples illustrate substring expansion using positional parameters:

```text
$ set -- 1 2 3 4 5 6 7 8 9 0 a b c d e f g h
$ echo ${@:7}
7 8 9 0 a b c d e f g h
$ echo ${@:7:0}

$ echo ${@:7:2}
7 8
$ echo ${@:7:-2}
bash: -2: substring expression < 0
$ echo ${@: -7:2}
b c
$ echo ${@:0}
./bash 1 2 3 4 5 6 7 8 9 0 a b c d e f g h
$ echo ${@:0:2}
./bash 1
$ echo ${@: -7:0}

```

If parameter is an indexed array name subscripted by ‘@’ or ‘\*’, the result is the length members of the array beginning with `${parameter[offset]}`. A negative offset is taken relative to one greater than the maximum index of the specified array. It is an expansion error if length evaluates to a number less than zero.

These examples show how you can use substring expansion with indexed arrays:

```text
$ array=(0 1 2 3 4 5 6 7 8 9 0 a b c d e f g h)
$ echo ${array[@]:7}
7 8 9 0 a b c d e f g h
$ echo ${array[@]:7:2}
7 8
$ echo ${array[@]: -7:2}
b c
$ echo ${array[@]: -7:-2}
bash: -2: substring expression < 0
$ echo ${array[@]:0}
0 1 2 3 4 5 6 7 8 9 0 a b c d e f g h
$ echo ${array[@]:0:2}
0 1
$ echo ${array[@]: -7:0}

```

Substring expansion applied to an associative array produces undefined results.

Substring indexing is zero-based unless the positional parameters are used, in which case the indexing starts at 1 by default. If offset is 0, and the positional parameters are used, `$@` is prefixed to the list.`${!prefix*}${!prefix@}`

Expands to the names of variables whose names begin with prefix, separated by the first character of the `IFS` special variable. When ‘@’ is used and the expansion appears within double quotes, each variable name expands to a separate word.`${!name[@]}${!name[*]}`

If name is an array variable, expands to the list of array indices \(keys\) assigned in name. If name is not an array, expands to 0 if name is set and null otherwise. When ‘@’ is used and the expansion appears within double quotes, each key expands to a separate word.`${#parameter}`

The length in characters of the expanded value of parameter is substituted. If parameter is ‘\*’ or ‘@’, the value substituted is the number of positional parameters. If parameter is an array name subscripted by ‘\*’ or ‘@’, the value substituted is the number of elements in the array. If parameter is an indexed array name subscripted by a negative number, that number is interpreted as relative to one greater than the maximum index of parameter, so negative indices count back from the end of the array, and an index of -1 references the last element.`${parameter#word}${parameter##word}`

The word is expanded to produce a pattern and matched according to the rules described below \(see [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching)\). If the pattern matches the beginning of the expanded value of parameter, then the result of the expansion is the expanded value of parameter with the shortest matching pattern \(the ‘\#’ case\) or the longest matching pattern \(the ‘\#\#’ case\) deleted. If parameter is ‘@’ or ‘\*’, the pattern removal operation is applied to each positional parameter in turn, and the expansion is the resultant list. If parameter is an array variable subscripted with ‘@’ or ‘\*’, the pattern removal operation is applied to each member of the array in turn, and the expansion is the resultant list.`${parameter%word}${parameter%%word}`

The word is expanded to produce a pattern and matched according to the rules described below \(see [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching)\). If the pattern matches a trailing portion of the expanded value of parameter, then the result of the expansion is the value of parameter with the shortest matching pattern \(the ‘%’ case\) or the longest matching pattern \(the ‘%%’ case\) deleted. If parameter is ‘@’ or ‘\*’, the pattern removal operation is applied to each positional parameter in turn, and the expansion is the resultant list. If parameter is an array variable subscripted with ‘@’ or ‘\*’, the pattern removal operation is applied to each member of the array in turn, and the expansion is the resultant list.`${parameter/pattern/string}`

The pattern is expanded to produce a pattern just as in filename expansion. Parameter is expanded and the longest match of pattern against its value is replaced with string. The match is performed according to the rules described below \(see [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching)\). If pattern begins with ‘/’, all matches of pattern are replaced with string. Normally only the first match is replaced. If pattern begins with ‘\#’, it must match at the beginning of the expanded value of parameter. If pattern begins with ‘%’, it must match at the end of the expanded value of parameter. If string is null, matches of pattern are deleted and the `/` following pattern may be omitted. If the `nocasematch` shell option \(see the description of `shopt` in [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\) is enabled, the match is performed without regard to the case of alphabetic characters. If parameter is ‘@’ or ‘\*’, the substitution operation is applied to each positional parameter in turn, and the expansion is the resultant list. If parameter is an array variable subscripted with ‘@’ or ‘\*’, the substitution operation is applied to each member of the array in turn, and the expansion is the resultant list.`${parameter^pattern}${parameter^^pattern}${parameter,pattern}${parameter,,pattern}`

This expansion modifies the case of alphabetic characters in parameter. The pattern is expanded to produce a pattern just as in filename expansion. Each character in the expanded value of parameter is tested against pattern, and, if it matches the pattern, its case is converted. The pattern should not attempt to match more than one character. The ‘^’ operator converts lowercase letters matching pattern to uppercase; the ‘,’ operator converts matching uppercase letters to lowercase. The ‘^^’ and ‘,,’ expansions convert each matched character in the expanded value; the ‘^’ and ‘,’ expansions match and convert only the first character in the expanded value. If pattern is omitted, it is treated like a ‘?’, which matches every character. If parameter is ‘@’ or ‘\*’, the case modification operation is applied to each positional parameter in turn, and the expansion is the resultant list. If parameter is an array variable subscripted with ‘@’ or ‘\*’, the case modification operation is applied to each member of the array in turn, and the expansion is the resultant list.`${parameter@operator}`

The expansion is either a transformation of the value of parameter or information about parameter itself, depending on the value of operator. Each operator is a single letter:`Q`

The expansion is a string that is the value of parameter quoted in a format that can be reused as input.`E`

The expansion is a string that is the value of parameter with backslash escape sequences expanded as with the `$'…'` quoting mechanism.`P`

The expansion is a string that is the result of expanding the value of parameter as if it were a prompt string \(see [Controlling the Prompt](controlling-the-prompt-bash-reference-manual.md#Controlling-the-Prompt)\).`A`

The expansion is a string in the form of an assignment statement or `declare` command that, if evaluated, will recreate parameter with its attributes and value.`a`

The expansion is a string consisting of flag values representing parameter’s attributes.

If parameter is ‘@’ or ‘\*’, the operation is applied to each positional parameter in turn, and the expansion is the resultant list. If parameter is an array variable subscripted with ‘@’ or ‘\*’, the operation is applied to each member of the array in turn, and the expansion is the resultant list.

The result of the expansion is subject to word splitting and pathname expansion as described below.

