## Some regex that I used, maybe delete it later (or NOT):

1. `[\s|(A-Za-z)]+` -- RegEx replace spaces OR text in ()

2. `^(\d.*)|(\n)` (replace with ` ` just space) -- replace multiple Subtitles (SRT) lines with 1 line
3. `\s{2,}` (replace with ` ` just space) -- replace multiple spaces with 1


### Work regex
1. `^\n+(?!\n)` (replace with ``) -- replace multiple 2 newlines with 1 newline (negative lookahead)
2. `^\n+` (replace with `\n`) -- replace multiple newlines with 1