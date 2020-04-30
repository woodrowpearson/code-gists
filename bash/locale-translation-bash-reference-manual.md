# Locale Translation \(Bash Reference Manual\)

## 3.1.2.5 Locale-Specific Translation

A double-quoted string preceded by a dollar sign \(‘$’\) will cause the string to be translated according to the current locale. If the current locale is `C` or `POSIX`, the dollar sign is ignored. If the string is translated and replaced, the replacement is double-quoted.

Some systems use the message catalog selected by the `LC_MESSAGES` shell variable. Others create the name of the message catalog from the value of the `TEXTDOMAIN` shell variable, possibly adding a suffix of ‘.mo’. If you use the `TEXTDOMAIN` variable, you may need to set the `TEXTDOMAINDIR` variable to the location of the message catalog files. Still others use both variables in this fashion: `TEXTDOMAINDIR`/`LC_MESSAGES`/LC\_MESSAGES/`TEXTDOMAIN`.mo.

