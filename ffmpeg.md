### This is sample of functions converting `mov`(any video you want actually) files to `mp4`!

> Command Flags

| Flag | Options | Description |
| ---- | ------- | ----------- |
| `-codec:a` | libfaac, aac, libvorbis | Audio Codec |
| `-quality` | best, good, realtime | Video Quality |
| `-b:a` | 128k, 192k, 256k, 320k | Audio Bitrate |
| `-codec:v` | mpeg4, libx264, libvpx-vp9 | Video Codec |
| `-b:v` | 1000, 2500, 5000, 8000 | Video Bitrate |
| `-vf scale` | -1:X | Resize Video (X is height) |
| `-qmin 10 -qmax 42` | ??? | I don't really know what is this for, help related to this is welcome... |

###### MP4 - 1080p

`ffmpeg -i input.mov -preset slow -codec:a libvorbis -b:a 128k -codec:v libx264 -pix_fmt yuv420p -b:v 4500k -minrate 4500k -maxrate 9000k -bufsize 9000k -vf scale=1080:-1 intro-1080p.mp4`

###### MP4 - 720p

`ffmpeg -i input.mov -preset slow -codec:a libvorbis -b:a 128k -codec:v libx264 -pix_fmt yuv420p -b:v 2500k -minrate 1500k -maxrate 4000k -bufsize 5000k -vf scale=720:-1 intro-720p.mp4`

###### MP4 - 480p

`ffmpeg -i input.mov -preset slow -codec:a libvorbis -b:a 128k -codec:v libx264 -pix_fmt yuv420p -b:v 1000k -minrate 500k -maxrate 2000k -bufsize 2000k -vf scale=854:480 intro-480p.mp4`

###### MP4 - 360p

`ffmpeg -i input.mov -preset slow -codec:a libvorbis -b:a 128k -codec:v libx264 -pix_fmt yuv420p -b:v 750k -minrate 400k -maxrate 1000k -bufsize 1500k -vf scale=360:-1 intro-360p.mp4`
