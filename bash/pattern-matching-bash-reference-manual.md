# Pattern Matching \(Bash Reference Manual\)

Matches any one of the enclosed characters. A pair of characters separated by a hyphen denotes a range expression; any character that falls between those two characters, inclusive, using the current locale’s collating sequence and character set, is matched. If the first character following the ‘\[’ is a ‘!’ or a ‘^’ then any character not enclosed is matched. A ‘-’ may be matched by including it as the first or last character in the set. A ‘\]’ may be matched by including it as the first character in the set. The sorting order of characters in range expressions is determined by the current locale and the values of the `LC_COLLATE` and `LC_ALL` shell variables, if set.

For example, in the default C locale, ‘\[a-dx-z\]’ is equivalent to ‘\[abcdxyz\]’. Many locales sort characters in dictionary order, and in these locales ‘\[a-dx-z\]’ is typically not equivalent to ‘\[abcdxyz\]’; it might be equivalent to ‘\[aBbCcDdxXyYz\]’, for example. To obtain the traditional interpretation of ranges in bracket expressions, you can force the use of the C locale by setting the `LC_COLLATE` or `LC_ALL` environment variable to the value ‘C’, or enable the `globasciiranges` shell option.

Within ‘\[’ and ‘\]’, character classes can be specified using the syntax `[:`class`:]`, where class is one of the following classes defined in the POSIX standard:

```text
alnum   alpha   ascii   blank   cntrl   digit   graph   lower
print   punct   space   upper   word    xdigit
```

A character class matches any character belonging to that class. The `word` character class matches letters, digits, and the character ‘\_’.

Within ‘\[’ and ‘\]’, an equivalence class can be specified using the syntax `[=`c`=]`, which matches all characters with the same collation weight \(as defined by the current locale\) as the character c.

Within ‘\[’ and ‘\]’, the syntax `[.`symbol`.]` matches the collating symbol symbol.

