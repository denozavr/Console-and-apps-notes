
REPLACE (**in bat file use `%%` instead of `%`**)

`for %A IN (*.jpg) DO convert "%A" -quality 70% "%A"`

`convert *.jpg -resize 10% output.jpg`

### *Optimal resize and quality*

`mogrify  -resize 75% -quality 90% *.jpg`