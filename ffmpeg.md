### [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links)

### Cheatsheets links (test and select useful commands)
1. [https://devhints.io/ffmpeg](https://devhints.io/ffmpeg)
2. [https://www.cheatography.com/thetartankilt/cheat-sheets/ffmpeg/](https://www.cheatography.com/ffmpeg/)


# Video

### This is sample of functions converting `mov`(any video you want actually) files to `mp4`!

> Command Flags

| Flag | Options | Description |
| ---- | ------- | ----------- |
| `-codec:a (= -c:a)` | libfaac, aac, libvorbis, [copy](https://stackoverflow.com/questions/38379412/what-does-copy-do-in-a-ffmpeg-command-line) | Audio Codec |
| `-quality` | best, good, realtime | Video Quality |
| `-b:a` | 128k, 192k, 256k, 320k | Audio Bitrate |
| `-codec:v (= -c:v)` | mpeg4, libx264, libvpx-vp9, [copy](https://stackoverflow.com/questions/38379412/what-does-copy-do-in-a-ffmpeg-command-line) | Video Codec |
| `-b:v` | 1000, 2500, 5000, 8000 | Video Bitrate |
| `-s` | hd480, 640x360,720x480  | Size(widthxheight), `-vf scale` is more flexible |
| `-vf scale` | X:-1 | [Resize Video (X is width)](https://trac.ffmpeg.org/wiki/Scaling) |
| `-pix_fmt` | yuv420p, yuyv422, rgb24, gray | [Set pixel format](https://ffmpeg.org/ffmpeg.html#toc-Advanced-Video-options) |
| `-crf` | From 0 (best) to 53 (worst) | [Constant Rate Factor (CRF) for better quality default 23, custom advised values are from 15 to 29](https://trac.ffmpeg.org/wiki/Encode/H.264#crf) |

###### MP4 - 1080p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 4500k -minrate 4500k -maxrate 9000k -bufsize 9000k -vf scale=1080:-1 intro-1080p.mp4`

###### MP4 - 720p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 2500k -minrate 1500k -maxrate 4000k -bufsize 5000k -vf scale=720:-1 intro-720p.mp4`

###### MP4 - 480p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 1000k -minrate 500k -maxrate 2000k -bufsize 2000k -vf scale=854:480 intro-480p.mp4`

#### MP4 - 480p (alternative)

`ffmpeg -i input.mp4 -s hd480 -c:v libx264 -crf 23 -c:a aac output_480.mp4` (850x480) <br/>
`ffmpeg -i input.mp4 -s 480x320 -c:v libx264 -crf 23 -c:a aac output_480.mp4`

###### MP4 - 360p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 750k -minrate 400k -maxrate 1000k -bufsize 1500k -vf scale=360:-1 intro-360p.mp4`

#### Convert all videos in folder (Windows)

Convert all mp4 videos in folder using configs: [Code for Linux](https://stackoverflow.com/questions/5784661/how-do-you-convert-an-entire-directory-with-ffmpeg)

**if you run this command in a batch (.bat) file you need to double the % signs => %%**

`for %A IN (*.mp4) DO ffmpeg -i "%A" OUTPUT_CONFIGS  "%A_new.mp4"`

Example:

`for %A IN (*.mp4) DO ffmpeg -i "%A" -preset slow -codec:a libvorbis -b:a 128k -codec:v libx264 -pix_fmt yuv420p -b:v 750k -minrate 400k -maxrate 1000k -bufsize 1500k -vf scale=360:-1  "%A_new.mp4"`

`for %A IN (*.mp4) DO ffmpeg -i "%A" -s 320x240 -c:v libx264 -crf 23 -c:a aac  "%A_new.mp4"`

#### Extract images from video

`ffmpeg -i video.mp4 -q:v 1 output/img_%05d.jpg`

Extract from **video.mp4** videofile to *output* folder, `-q:v 1` means to use the best possible quality for exported pictures. Files will have name like **img_00001.jpg**.
**output** folder should exist before implementin command, otherwise you will got an error.


#### Extract Sound from video and merge again
##### Extract Sound from video

`ffmpeg -i video.mp4 -vn -ar 44100 -ac 2 -ab 320K -f mp3 sound.mp3` (Extract 320kbs sound.mp3 from video.mp4)

* `-vn` -- skip video stream(layer)
* `-ar` -- [Set the audio sampling frequency.](https://ffmpeg.org/ffmpeg-all.html#toc-Audio-Options)
* `-ac` -- Set the number of audio channels.
* `-ab` -- Set bitrate of audio.

##### Merge pictures and sound to video again

`ffmpeg -i img_%05d.jpg -i sound.mp3 -vcodec libx264 -preset veryslow -crf 10 -r 23.976 new_video.mp4`

Recreate our video based on exported images and sound, <span style="background-color:yellow">Be careful **-r** (frames) should be the same as on original video, otherwise sound and pictures would not match (out of sync)</span>.

#### Rotate video

[Rotate vertical video to 90 degrees](https://stackoverflow.com/questions/3937387/rotating-videos-with-ffmpeg) (and keep metadata), *will optimize and reduce output video size*, for keeping the better quality use **`-crf` flag like `-crf 22`**

`ffmpeg -i video.mp4 -map_metadata 0 -vf "transpose=2"  output.mp4`

### Useful links

1. [How to resize a video to make it smaller with FFmpeg](https://superuser.com/questions/624563/how-to-resize-a-video-to-make-it-smaller-with-ffmpeg)
2. [How do I change frame size, preserving width (using ffmpeg)?](https://video.stackexchange.com/questions/9947/how-do-i-change-frame-size-preserving-width-using-ffmpeg)
3. !!!!https://superuser.com/questions/523286/how-to-make-handbrake-preserve-capture-time-creation-time 


# Images

### Reduce size of images and delete metadata(EXIF) for all JPG in the current folder

`for %A IN (*.jpg) DO ffmpeg -i "%A" "%A_new.jpg"`  
(if use ***.bat** file don't forget to use **%%** like) : `for %%A IN (*.jpg) DO ffmpeg -i "%%A" "_%%A"`


### Useful links

1. https://stackoverflow.com/questions/28806816/use-ffmpeg-to-resize-image Delete Exif(metadata from images)
