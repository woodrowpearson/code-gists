# Vim

```text
" Insert text in the end of each line
" s/ - substitute.
" $ - the end of the line.
" / - change it to.
" , - a comma.
:%s/$/,
```

```text
" Lowercase line
Vu
```

```text
" Find char backwards
F<char>
```

```text
" Delete backwards until char
dT<char>
```

```text
" Visually select until char
v/<char><return>
```

```text
" Delete all lines in file
:%d
```

```text
" Yank two inner words
" Yanks first and second words (with the trailing space) in the unnamed register
y2aw
```

```text
" Delete until start of line
d0
```

```text
" Yank entire file
:%y+
```

```text
" Select entire block
Vat
```

```text
" Visually select until end of line
v$
```

```text
" Visually select paragraph or function
V}
```

```text
" See whats in a buffer
" See insides of q buffer
:echo @q
```

```text
" See registers
:registers
```

```text
" Delete until end of file
VGx
```

```text
" Visually select block
V%
```

```text
" Start recording macro
" Record to register d
qd
```

```text
" Delete char under cursor
x
```

```text
" Yank inside tag. Can yank an XML tag for example
yat
```

```text
" Make multi line search. https://vim.fandom.com/wiki/Search_across_multiple_lines
" Will carry over to new line
\_s
```

```text
" Inclusive search
/foo/e
```

```text
" Delete until searched string. Won't delete string itself.
d/string
```

```text
" Search and replace
:%s/<search>/<replace>/g
```

```text
" Run command on startup
" Run ':Goyo' on startup. Put it in .vimrc
autocmd VimEnter * Goyo"
```

```text
" Insert text at start of each line in file
" Insert // at start of each line in file
:%s!^!//!
```

```text
" Replay last macro
@@
```

```text
" Delete until character
df<char>
```

```text
" Centre current line
zz
```

```text
" Put results of command into a register
" In normal mode, will put results of d$ command into _ (black hole register)
"_d$
```

```text
" Run macro on whole file
:%normal @x " will run macro x
```

