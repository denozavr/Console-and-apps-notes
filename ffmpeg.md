### [Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links)

#### [Since GITHUB doesn't support text coloring, here some Unicodes](https://stackoverflow.com/a/36287428/2771704) + [MORE UNICODES ~ 800](https://apps.timwhitlock.info/emoji/tables/unicode)

### Cheatsheets links (test and select useful commands)

1. [https://devhints.io/ffmpeg](https://devhints.io/ffmpeg)
2. [https://www.cheatography.com/thetartankilt/cheat-sheets/ffmpeg/](https://www.cheatography.com/ffmpeg/)
3. [20+ FFmpeg Commands For Beginners (2019-05)](https://www.ostechnix.com/20-ffmpeg-commands-beginners/)

### Issues

1. Cannot play portrait video on my old LG TV (bought in 2013) after converting video using **ffmpeg** ([nothing worked from rotate post](https://stackoverflow.com/questions/3937387/rotating-videos-with-ffmpeg)), funny thing that original videos from phone (~100Mb for 1 minute) worked fine, but even if use Google Photos converting and download and try to play, same error on TV. _The only workaround that worked to play converted portrait videos on TV was using **force_original_aspect_ratio** from [this post](https://superuser.com/questions/547296/resizing-videos-with-ffmpeg-avconv-to-fit-into-static-sized-player)_

# Video

### This is sample of functions converting `mov`(any video you want actually) files to `mp4`!

> Command Flags

| Flag                | Options                                                                                                                     | Description                                                                                                                                                     |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-codec:a (= -c:a)` | libfaac, aac, libvorbis, [copy](https://stackoverflow.com/questions/38379412/what-does-copy-do-in-a-ffmpeg-command-line)    | Audio Codec                                                                                                                                                     |
| `-quality`          | best, good, realtime                                                                                                        | Video Quality                                                                                                                                                   |
| `-b:a`              | 128k, 192k, 256k, 320k                                                                                                      | Audio Bitrate                                                                                                                                                   |
| `-codec:v (= -c:v)` | mpeg4, libx264, libvpx-vp9, [copy](https://stackoverflow.com/questions/38379412/what-does-copy-do-in-a-ffmpeg-command-line) | Video Codec                                                                                                                                                     |
| `-b:v`              | 1000, 2500, 5000, 8000                                                                                                      | Video Bitrate                                                                                                                                                   |
| `-s`                | hd480, 640x360,720x480                                                                                                      | Size(widthxheight), `-vf scale` is more flexible                                                                                                                |
| `-vf scale`         | X:-1                                                                                                                        | [Resize Video (X is width)](https://trac.ffmpeg.org/wiki/Scaling)                                                                                               |
| `-pix_fmt`          | yuv420p, yuyv422, rgb24, gray                                                                                               | [Set pixel format](https://ffmpeg.org/ffmpeg.html#toc-Advanced-Video-options)                                                                                   |
| `-crf`              | From 0 (best) to 53 (worst)                                                                                                 | [Constant Rate Factor (CRF) for better quality default 23, custom advised values are from 15 to 29](https://trac.ffmpeg.org/wiki/Encode/H.264#crf)              |
| -----               | -------                                                                                                                     | -----------                                                                                                                                                     |
| `-map_metadata`     | 0 (most often, [more info in Docs](https://ffmpeg.org/ffmpeg.html))                                                         | `-map_metadata 0` keeps all info from **input** file, **works only for default meta**, for custom meta use [-movflags](https://video.stackexchange.com/a/26076) |
| -----               | -------                                                                                                                     | -----------                                                                                                                                                     |
| `-i`                | ??                                                                                                                          | means input file path (or URL) [see this link from docs](https://ffmpeg.org/ffmpeg.html#toc-Main-options)                                                       |

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

### Simplest way to convert video with metadata

`ffmpeg -i input.mp4 -map_metadata 0 -crf 22 output.mp4`

#### Convert all videos in folder (Windows)

Convert all mp4 videos in folder using configs: [Code for Linux](https://stackoverflow.com/questions/5784661/how-do-you-convert-an-entire-directory-with-ffmpeg)

&#x1F534;<mark style="background-color:orange">**if you run this command in a batch (.bat) file you need to double the % signs => %%**</mark> &#x1F534;

`for %A IN (*.mp4) DO ffmpeg -i "%A" OUTPUT_CONFIGS  "%A_new.mp4"`

Example:

`for %A IN (*.mp4) DO ffmpeg -i "%A" -preset slow -codec:a libvorbis -b:a 128k -codec:v libx264 -pix_fmt yuv420p -b:v 750k -minrate 400k -maxrate 1000k -bufsize 1500k -vf scale=360:-1  "%A_new.mp4"`

`for %A IN (*.mp4) DO ffmpeg -i "%A" -s 320x240 -c:v libx264 -crf 23 -c:a aac  "%A_new.mp4"`

### Convert video and keep the same quality (i.e. from _.mov to _.mp4 )

**[Link](https://stackoverflow.com/questions/25569180/ffmpeg-convert-without-loss-quality)**

According to link above we have several options (**option 2 seems to be the best**):

1. use `-crf` see the table on above (best values between **18 and 29**)
2. keep all codecs using `-vcodec copy -acodec copy -scodec mov_text` , where `-scodec` is [codec for subtitles (Section 5.9)](https://ffmpeg.org/ffmpeg.html#toc-Subtitle-options) <br><br>
   `for %a in ("*.mov") do ffmpeg.exe -i "%a" -vcodec copy -acodec copy -scodec mov_text "%~na.mp4"` will convert all files in folder from **MOV** to **MP4** and keep all codecs and the initial name
3. use `-qscale 0` OR `-qscale:v` for OLD codecs. It is ignored by libx264 and libx265 which use -crf instead.

#### Extract subs from video
- https://superuser.com/questions/583393/how-to-extract-subtitle-from-video-using-ffmpeg

#### Extract images from video

`ffmpeg -i video.mp4 -q:v 1 output/img_%05d.jpg`

Extract from **video.mp4** videofile to _output_ folder, `-q:v 1` means to use the best possible quality for exported pictures. Files will have name like **img_00001.jpg**.
<mark style="background-color: yellow">**output** folder should exist before implementin command, otherwise you will got an error.</mark>

Additional example(for several videos and **KEEP meta**)

`for %A IN (*.mp4) DO ffmpeg -i "%A" -map_metadata 0 -crf 22 out/"%A"`

#### Extract Sound from video and merge again

##### Extract Sound from video

`ffmpeg -i video.mp4 -vn -ar 44100 -ac 2 -ab 320K -f mp3 sound.mp3` (Extract 320kbs sound.mp3 from video.mp4)

- `-vn` -- skip video stream(layer)
- `-ar` -- [Set the audio sampling frequency.](https://ffmpeg.org/ffmpeg-all.html#toc-Audio-Options)
- `-ac` -- Set the number of audio channels.
- `-ab` -- Set bitrate of audio.
- `-f` -- file format ([check Docs](https://ffmpeg.org/ffmpeg.html#toc-Main-options))

Much simpler way to extract video([from here](https://superuser.com/questions/332347/how-can-i-convert-mp4-video-to-mp3-audio-with-ffmpeg)):

`ffmpeg -i filename.mp4 filename.mp3`

#### Merge video and audio

[(2011) see link](https://superuser.com/questions/277642/how-to-merge-audio-and-video-file-in-ffmpeg)

`ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac output.mp4`

##### Merge pictures and sound to video again

`ffmpeg -i img_%05d.jpg -i sound.mp3 -vcodec libx264 -preset veryslow -crf 10 -r 23.976 new_video.mp4`

Recreate our video based on exported images and sound, <mark style="background-color:yellow">Be careful **-r** (frames) should be the same as on original video, otherwise sound and pictures would not match (out of sync)</mark>.

#### Rotate video

[Rotate vertical video to 90 degrees](https://stackoverflow.com/questions/3937387/rotating-videos-with-ffmpeg) (and keep metadata), _will optimize and reduce output video size_, for keeping the better quality use **`-crf` flag like `-crf 22`**

`ffmpeg -i video.mp4 -map_metadata 0 -vf "transpose=2"  output.mp4`

[also pure metadata way can be used](https://stackoverflow.com/a/31683689/2771704) (**not supported by all devices**)
`ffmpeg -i input.mp4 -map_metadata 0 -metadata:s:v rotate="90" -codec copy output.mp4`

#### Concatenate/Merge videos

**With text file(list.txt) approach there are NO any pauses between concatenated videos using instructions below**
1. Like approach with text files ([some more info here + notes how to concat all files in folder](https://stackoverflow.com/a/41387530))

!!`creation_time` metadata works for **.mp4** files ([other type of files may need another metadata tag](https://stackoverflow.com/questions/40354172/change-avi-creation-date-with-ffmpeg))

`ffmpeg -f concat -i list.txt -metadata creation_time="2017-05-13 14:30:37" -c copy output.mp4`

- `-metadata creation_time="2017-05-13 14:30:37"` -- set **Media created** for new **.mp4** files (otherwise **Media created** will be empty )
- `-i list.txt` -- contains list of filenames which could be concatenated with the next commands
  ```:: Create File List
  echo file file1.mp4 >  list.txt
  echo file file2.mp4 >> list.txt
  echo file file3.mp4 >> list.txt
  ```
2. (Bash) [from here](https://stackoverflow.com/a/42104988/2771704) script to create file and merge files (joins all `mp4` files in folder into `joined-out.mp4` ) + good article about [Bash wildcards](https://linuxhint.com/bash_wildcard_tutorial/) (for 1 symbol use `?` like `0?.mp4` for files like `01.mp4`)

    ```
    [ -e list.txt ] && rm list.txt
    for f in *.mp4
    do
      echo "file $f" >> list.txt
    done

    ffmpeg -f concat -i list.txt -c copy joined-out.mp4 && rm list.txt
    ```

#### Slow down the video

- `ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=2.0*PTS[v];[0:a]atempo=0.5[a]" -map "[v]" -map "[a]" output2.mp4` -- slow down video (`setpts=2.0*PTS[v]`) and audio (`atempo=0.5`) 2 times
- `ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=3.0*PTS[v];[0:a]atempo=0.6,atempo=0.55[a]" -map "[v]" -map "[a]" output3.mp4` -- slow down video and audio(`atempo=0.6,atempo=0.55` - the result of multiplication should be 0.33) 3 times
- Useful links:
  - [(OFFICIAL DOCS) Speeding up/slowing down video](https://trac.ffmpeg.org/wiki/How%20to%20speed%20up%20/%20slow%20down%20a%20video)
    - `setpts` -- The filter works by changing the presentation timestamp (PTS) of each video frame. For example, if there are two succesive frames shown at timestamps 1 and 2, and you want to speed up the video, those timestamps need to become 0.5 and 1, respectively. Thus, we have to multiply them by 0.5.
    - The atempo filter is limited to using values between 0.5 and 2.0 (so it can slow it down to no less than half the original speed, and speed up to no more than double the input). If you need to, you can get around this limitation by stringing multiple atempo filters together. The following with quadruple the audio speed: `ffmpeg -i input.mkv -filter:a "atempo=2.0,atempo=2.0" -vn output.mkv`
  - [(2011) Change the frame rate of an MP4 video with ffmpeg](https://superuser.com/questions/320045/change-the-frame-rate-of-an-mp4-video-with-ffmpeg)
  - [(2017) Speed up video x1.5 but keep all frames](https://superuser.com/questions/1247462/speed-up-video-x1-5-but-keep-all-frames)

### Cut part of video

#### **Cut first 5 seconds**

- `ffmpeg -ss 00:00:05 -i orig.mp4 orig_minus_5_sec.mp4` - discard first 5 seconds of the video (used to delete some ads in the beginning to syn subtitles)
  - Interesting link: [What is difference between -ss and -itsoffset in ffmpeg?](https://superuser.com/questions/538031/what-is-difference-between-ss-and-itsoffset-in-ffmpeg)

#### **Cut part of video from the middle**

- `ffmpeg -i "input.mp4" -ss 00:10:00 -to 00:12:00 "output.mp4"`-- cut 2 minutes from the middle [see link](https://stackoverflow.com/questions/45004159/ffmpeg-ss-and-t-for-cutting-mp3)

### Useful links

1. [How to resize a video to make it smaller with FFmpeg](https://superuser.com/questions/624563/how-to-resize-a-video-to-make-it-smaller-with-ffmpeg)
2. [How do I change frame size, preserving width (using ffmpeg)?](https://video.stackexchange.com/questions/9947/how-do-i-change-frame-size-preserving-width-using-ffmpeg)
3. !!!!https://superuser.com/questions/523286/how-to-make-handbrake-preserve-capture-time-creation-time

# Audio

### Convert `wav/flac` formats to `mp3`

- `ffmpeg -i "mix_2020.wav" -vn -ar 44100 -ac 2 -b:a 320k output.mp3` - convert `wav` file to 320 kbps `mp3` (taken from [here](https://stackoverflow.com/questions/3255674/convert-audio-files-to-mp3-using-ffmpeg))


# Images

### Reduce size of images and delete metadata(EXIF) for all JPG in the current folder

`for %A IN (*.jpg) DO ffmpeg -i "%A" "%A_new.jpg"`
(if use **\*.bat** file don't forget to use **%%** like) : `for %%A IN (*.jpg) DO ffmpeg -i "%%A" "_%%A"`

### Useful links

1. https://stackoverflow.com/questions/28806816/use-ffmpeg-to-resize-image Delete Exif(metadata from images)
