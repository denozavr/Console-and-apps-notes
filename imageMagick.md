
REPLACE (**in bat file use `%%` instead of `%`**)

`for %A IN (*.jpg) DO convert "%A" -quality 70% "%A"`

`convert *.jpg -resize 10% output.jpg`

### *Optimal resize and quality*

`mogrify  -resize 75% -quality 90% -taint *.jpg`

* `-taint` -- [keep metadata(EXIFI) during converting](https://imagemagick.org/script/command-line-options.php)

### Change size (with center)

`mogrify -resize x150 -background white -gravity center -extent 150x150 *.jpg`  -- replace image with changing its size to 150px(1 side) and if there is space fill it with **white** color and center

If cut image wrong try:
`mogrify -resize 150x150 -background white -gravity center -extent 150x150 *.jpg`

### Combine several images

#### In grid ([montage command](http://www.imagemagick.org/Usage/montage/))

`montage 1.jpg 2.jpg -background white -tile 2x -geometry +50+50 50.jpg`

where
* `1.jpg 2.jpg` - input images (could be more)
* `-background white` - background for the spacing (padding) (white is default **none** means black)
* `-tile 2x` - (*tile*) keep original size of images in grid, otherwise they will be shrinked to default 120x120 pixel boxes
  * `2x` -- means 2 images on a row (more info in [Tile Layout Controls section]((http://www.imagemagick.org/Usage/montage/)))
* `+50+50` - spacings in pixels (horizontally + vertically), for NO SPACING use `+0+0`
* `50.jpg` - name of output image (for png can use `PNG32:50.png`)
