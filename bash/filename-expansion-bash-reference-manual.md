# Filename Expansion \(Bash Reference Manual\)

## 3.5.8 Filename Expansion

After word splitting, unless the -f option has been set \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\), Bash scans each word for the characters ‘\*’, ‘?’, and ‘\[’. If one of these characters appears, then the word is regarded as a pattern, and replaced with an alphabetically sorted list of filenames matching the pattern \(see [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching)\). If no matching filenames are found, and the shell option `nullglob` is disabled, the word is left unchanged. If the `nullglob` option is set, and no matches are found, the word is removed. If the `failglob` shell option is set, and no matches are found, an error message is printed and the command is not executed. If the shell option `nocaseglob` is enabled, the match is performed without regard to the case of alphabetic characters.

When a pattern is used for filename expansion, the character ‘.’ at the start of a filename or immediately following a slash must be matched explicitly, unless the shell option `dotglob` is set. The filenames ‘.’ and ‘..’ must always be matched explicitly, even if `dotglob` is set. In other cases, the ‘.’ character is not treated specially.

When matching a filename, the slash character must always be matched explicitly by a slash in the pattern, but in other matching contexts it can be matched by a special pattern character as described below \(see [Pattern Matching](pattern-matching-bash-reference-manual.md#Pattern-Matching)\).

See the description of `shopt` in [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin), for a description of the `nocaseglob`, `nullglob`, `failglob`, and `dotglob` options.

The `GLOBIGNORE` shell variable may be used to restrict the set of file names matching a pattern. If `GLOBIGNORE` is set, each matching file name that also matches one of the patterns in `GLOBIGNORE` is removed from the list of matches. If the `nocaseglob` option is set, the matching against the patterns in `GLOBIGNORE` is performed without regard to case. The filenames . and .. are always ignored when `GLOBIGNORE` is set and not null. However, setting `GLOBIGNORE` to a non-null value has the effect of enabling the `dotglob` shell option, so all other filenames beginning with a ‘.’ will match. To get the old behavior of ignoring filenames beginning with a ‘.’, make ‘.\*’ one of the patterns in `GLOBIGNORE`. The `dotglob` option is disabled when `GLOBIGNORE` is unset.

