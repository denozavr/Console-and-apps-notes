### [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links)

### Cheatsheets links (test and select useful commands)
1. [https://devhints.io/ffmpeg](https://devhints.io/ffmpeg)
2. [https://www.cheatography.com/thetartankilt/cheat-sheets/ffmpeg/](https://www.cheatography.com/ffmpeg/)



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
| `-crf` | From 0 (best) to 53 (worst) | [Constant Rate Factor (CRF) for better quality default 23](https://trac.ffmpeg.org/wiki/Encode/H.264#crf) |

###### MP4 - 1080p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 4500k -minrate 4500k -maxrate 9000k -bufsize 9000k -vf scale=1080:-1 intro-1080p.mp4`

###### MP4 - 720p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 2500k -minrate 1500k -maxrate 4000k -bufsize 5000k -vf scale=720:-1 intro-720p.mp4`

###### MP4 - 480p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 1000k -minrate 500k -maxrate 2000k -bufsize 2000k -vf scale=854:480 intro-480p.mp4`

#### MP4 - 480p (alternative)

`ffmpeg -i input.mp4 -s hd480 -c:v libx264 -crf 23 -c:a aac output_480.mp4` (850x480)
`ffmpeg -i input.mp4 -s 480x320 -c:v libx264 -crf 23 -c:a aac output_480.mp4`

###### MP4 - 360p

`ffmpeg -i input.mov -preset slow -c:a libvorbis -b:a 128k -c:v libx264 -pix_fmt yuv420p -b:v 750k -minrate 400k -maxrate 1000k -bufsize 1500k -vf scale=360:-1 intro-360p.mp4`



### Useful links

1. [How to resize a video to make it smaller with FFmpeg](https://superuser.com/questions/624563/how-to-resize-a-video-to-make-it-smaller-with-ffmpeg)
