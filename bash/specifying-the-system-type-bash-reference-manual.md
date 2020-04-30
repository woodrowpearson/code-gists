# Specifying the System Type \(Bash Reference Manual\)

## 10.5 Specifying the System Type

There may be some features `configure` can not figure out automatically, but need to determine by the type of host Bash will run on. Usually `configure` can figure that out, but if it prints a message saying it can not guess the host type, give it the --host=TYPE option. ‘TYPE’ can either be a short name for the system type, such as ‘sun4’, or a canonical name with three fields: ‘CPU-COMPANY-SYSTEM’ \(e.g., ‘i386-unknown-freebsd4.2’\).

See the file support/config.sub for the possible values of each field.

