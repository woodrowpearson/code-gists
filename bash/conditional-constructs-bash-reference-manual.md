# Conditional Constructs \(Bash Reference Manual\)

`if`

The syntax of the `if` command is:

```text
if test-commands; then
  consequent-commands;
[elif more-test-commands; then
  more-consequents;]
[else alternate-consequents;]
fi
```

The test-commands list is executed, and if its return status is zero, the consequent-commands list is executed. If test-commands returns a non-zero status, each `elif` list is executed in turn, and if its exit status is zero, the corresponding more-consequents is executed and the command completes. If ‘else alternate-consequents’ is present, and the final command in the final `if` or `elif` clause has a non-zero exit status, then alternate-consequents is executed. The return status is the exit status of the last command executed, or zero if no condition tested true.`case`

The syntax of the `case` command is:

```text
case word in
    [ [(] pattern [| pattern]…) command-list ;;]…
esac
```

`case` will selectively execute the command-list corresponding to the first pattern that matches word. The match is performed according to the rules described below in [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching). If the `nocasematch` shell option \(see the description of `shopt` in [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\) is enabled, the match is performed without regard to the case of alphabetic characters. The ‘\|’ is used to separate multiple patterns, and the ‘\)’ operator terminates a pattern list. A list of patterns and an associated command-list is known as a clause.

Each clause must be terminated with ‘;;’, ‘;&’, or ‘;;&’. The word undergoes tilde expansion, parameter expansion, command substitution, arithmetic expansion, and quote removal \(see [Shell Parameter Expansion](shell-parameter-expansion-bash-reference-manual.md#Shell-Parameter-Expansion)\) before matching is attempted. Each pattern undergoes tilde expansion, parameter expansion, command substitution, and arithmetic expansion.

There may be an arbitrary number of `case` clauses, each terminated by a ‘;;’, ‘;&’, or ‘;;&’. The first pattern that matches determines the command-list that is executed. It’s a common idiom to use ‘\*’ as the final pattern to define the default case, since that pattern will always match.

Here is an example using `case` in a script that could be used to describe one interesting feature of an animal:

```text
echo -n "Enter the name of an animal: "
read ANIMAL
echo -n "The $ANIMAL has "
case $ANIMAL in
  horse | dog | cat) echo -n "four";;
  man | kangaroo ) echo -n "two";;
  *) echo -n "an unknown number of";;
esac
echo " legs."
```

If the ‘;;’ operator is used, no subsequent matches are attempted after the first pattern match. Using ‘;&’ in place of ‘;;’ causes execution to continue with the command-list associated with the next clause, if any. Using ‘;;&’ in place of ‘;;’ causes the shell to test the patterns in the next clause, if any, and execute any associated command-list on a successful match, continuing the case statement execution as if the pattern list had not matched.

The return status is zero if no pattern is matched. Otherwise, the return status is the exit status of the command-list executed.`select`

The `select` construct allows the easy generation of menus. It has almost the same syntax as the `for` command:

```text
select name [in words …]; do commands; done
```

The list of words following `in` is expanded, generating a list of items. The set of expanded words is printed on the standard error output stream, each preceded by a number. If the ‘in words’ is omitted, the positional parameters are printed, as if ‘in "$@"’ had been specified. The `PS3` prompt is then displayed and a line is read from the standard input. If the line consists of a number corresponding to one of the displayed words, then the value of name is set to that word. If the line is empty, the words and prompt are displayed again. If `EOF` is read, the `select` command completes. Any other value read causes name to be set to null. The line read is saved in the variable `REPLY`.

The commands are executed after each selection until a `break` command is executed, at which point the `select` command completes.

Here is an example that allows the user to pick a filename from the current directory, and displays the name and index of the file selected.

```text
select fname in *;
do
	echo you picked $fname \($REPLY\)
	break;
done
```

`((…))`

The arithmetic expression is evaluated according to the rules described below \(see [Shell Arithmetic](shell-arithmetic-bash-reference-manual.md#Shell-Arithmetic)\). If the value of the expression is non-zero, the return status is 0; otherwise the return status is 1. This is exactly equivalent to

See [Bash Builtins](bash-builtins-bash-reference-manual.md#Bash-Builtins), for a full description of the `let` builtin.`[[…]]`

Return a status of 0 or 1 depending on the evaluation of the conditional expression expression. Expressions are composed of the primaries described below in [Bash Conditional Expressions](bash-conditional-expressions-bash-reference-manual.md#Bash-Conditional-Expressions). Word splitting and filename expansion are not performed on the words between the `[[` and `]]`; tilde expansion, parameter and variable expansion, arithmetic expansion, command substitution, process substitution, and quote removal are performed. Conditional operators such as ‘-f’ must be unquoted to be recognized as primaries.

When used with `[[`, the ‘&lt;’ and ‘&gt;’ operators sort lexicographically using the current locale.

When the ‘==’ and ‘!=’ operators are used, the string to the right of the operator is considered a pattern and matched according to the rules described below in [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching), as if the `extglob` shell option were enabled. The ‘=’ operator is identical to ‘==’. If the `nocasematch` shell option \(see the description of `shopt` in [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\) is enabled, the match is performed without regard to the case of alphabetic characters. The return value is 0 if the string matches \(‘==’\) or does not match \(‘!=’\) the pattern, and 1 otherwise. Any part of the pattern may be quoted to force the quoted portion to be matched as a string.

An additional binary operator, ‘=~’, is available, with the same precedence as ‘==’ and ‘!=’. When it is used, the string to the right of the operator is considered a POSIX extended regular expression and matched accordingly \(as in regex3\)\). The return value is 0 if the string matches the pattern, and 1 otherwise. If the regular expression is syntactically incorrect, the conditional expression’s return value is 2. If the `nocasematch` shell option \(see the description of `shopt` in [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\) is enabled, the match is performed without regard to the case of alphabetic characters. Any part of the pattern may be quoted to force the quoted portion to be matched as a string. Bracket expressions in regular expressions must be treated carefully, since normal quoting characters lose their meanings between brackets. If the pattern is stored in a shell variable, quoting the variable expansion forces the entire pattern to be matched as a string. Substrings matched by parenthesized subexpressions within the regular expression are saved in the array variable `BASH_REMATCH`. The element of `BASH_REMATCH` with index 0 is the portion of the string matching the entire regular expression. The element of `BASH_REMATCH` with index n is the portion of the string matching the nth parenthesized subexpression.

For example, the following will match a line \(stored in the shell variable line\) if there is a sequence of characters in the value consisting of any number, including zero, of space characters, zero or one instances of ‘a’, then a ‘b’:

```text
[[ $line =~ [[:space:]]*?(a)b ]]
```

That means values like ‘aab’ and ‘ aaaaaab’ will match, as will a line containing a ‘b’ anywhere in its value.

Storing the regular expression in a shell variable is often a useful way to avoid problems with quoting characters that are special to the shell. It is sometimes difficult to specify a regular expression literally without using quotes, or to keep track of the quoting used by regular expressions while paying attention to the shell’s quote removal. Using a shell variable to store the pattern decreases these problems. For example, the following is equivalent to the above:

```text
pattern='[[:space:]]*?(a)b'
[[ $line =~ $pattern ]]
```

If you want to match a character that’s special to the regular expression grammar, it has to be quoted to remove its special meaning. This means that in the pattern ‘xxx.txt’, the ‘.’ matches any character in the string \(its usual regular expression meaning\), but in the pattern ‘"xxx.txt"’ it can only match a literal ‘.’. Shell programmers should take special care with backslashes, since backslashes are used both by the shell and regular expressions to remove the special meaning from the following character. The following two sets of commands are _not_ equivalent:

```text
pattern='\.'

[[ . =~ $pattern ]]
[[ . =~ \. ]]

[[ . =~ "$pattern" ]]
[[ . =~ '\.' ]]
```

The first two matches will succeed, but the second two will not, because in the second two the backslash will be part of the pattern to be matched. In the first two examples, the backslash removes the special meaning from ‘.’, so the literal ‘.’ matches. If the string in the first examples were anything other than ‘.’, say ‘a’, the pattern would not match, because the quoted ‘.’ in the pattern loses its special meaning of matching any single character.

Expressions may be combined using the following operators, listed in decreasing order of precedence:`( expression )`

Returns the value of expression. This may be used to override the normal precedence of operators.`! expression`

True if expression is false.`expression1 && expression2`

True if both expression1 and expression2 are true.`expression1 || expression2`

True if either expression1 or expression2 is true.

The `&&` and `||` operators do not evaluate expression2 if the value of expression1 is sufficient to determine the return value of the entire conditional expression.

