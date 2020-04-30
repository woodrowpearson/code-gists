# Sharing Defaults \(Bash Reference Manual\)

 Next: [Operation Controls](operation-controls-bash-reference-manual.md#Operation-Controls), Previous: [Specifying the System Type](specifying-the-system-type-bash-reference-manual.md#Specifying-the-System-Type), Up: [Installing Bash](installing-bash-bash-reference-manual.md#Installing-Bash)   \[[Contents]()\]\[[Index](indexes-bash-reference-manual.md#Indexes)\]

If you want to set default values for `configure` scripts to share, you can create a site shell script called `config.site` that gives default values for variables like `CC`, `cache_file`, and `prefix`. `configure` looks for PREFIX/share/config.site if it exists, then PREFIX/etc/config.site if it exists. Or, you can set the `CONFIG_SITE` environment variable to the location of the site script. A warning: the Bash `configure` looks for a site script, but not all `configure` scripts do.

