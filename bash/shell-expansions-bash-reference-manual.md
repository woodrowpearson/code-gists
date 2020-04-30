# Shell Expansions \(Bash Reference Manual\)

## 3.5 Shell Expansions

Expansion is performed on the command line after it has been split into `token`s. There are seven kinds of expansion performed:

*  brace expansion
*  tilde expansion
*  parameter and variable expansion
*  command substitution
*  arithmetic expansion
*  word splitting
*  filename expansion

The order of expansions is: brace expansion; tilde expansion, parameter and variable expansion, arithmetic expansion, and command substitution \(done in a left-to-right fashion\); word splitting; and filename expansion.

On systems that can support it, there is an additional expansion available: process substitution. This is performed at the same time as tilde, parameter, variable, and arithmetic expansion and command substitution.

After these expansions are performed, quote characters present in the original word are removed unless they have been quoted themselves \(quote removal\).

Only brace expansion, word splitting, and filename expansion can increase the number of words of the expansion; other expansions expand a single word to a single word. The only exceptions to this are the expansions of `"$@"` and `$*` \(see [Special Parameters](special-parameters-bash-reference-manual.md#Special-Parameters)\), and `"${name[@]}"` and `${name[*]}` \(see [Arrays](arrays-bash-reference-manual.md#Arrays)\).

After all expansions, `quote removal` \(see [Quote Removal](quote-removal-bash-reference-manual.md#Quote-Removal)\) is performed.

