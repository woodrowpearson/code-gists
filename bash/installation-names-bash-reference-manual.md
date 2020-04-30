# Installation Names \(Bash Reference Manual\)

## 10.4 Installation Names

By default, ‘make install’ will install into /usr/local/bin, /usr/local/man, etc. You can specify an installation prefix other than /usr/local by giving `configure` the option --prefix=PATH, or by specifying a value for the `DESTDIR` ‘make’ variable when running ‘make install’.

You can specify separate installation prefixes for architecture-specific files and architecture-independent files. If you give `configure` the option --exec-prefix=PATH, ‘make install’ will use PATH as the prefix for installing programs and libraries. Documentation and other data files will still use the regular prefix.

