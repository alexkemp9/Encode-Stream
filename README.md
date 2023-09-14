# Encode-Stream
A BASH Script to encode VHS / Camera / Cassette Streams

## *Basics*
This script file is designed for use by any-user (no root access required) within a Terminal. It’s principal purpose is to make it easy & reliable to encode a stream from a VHS, Camera or Cassette player to a video file. It has been used extensively by myself to transfer all my VHS tapes (using a EasyCAP UTV007 USB converter - example below) & cassettes (using a USB-powered cassette player) to disc under *Devuan* (a systemD-free version of *Debian*). In addition to BASH, the main utility required is FFMPEG. Note that zero efforts are made to test for the presence of FFMPEG before use.
![EasyCAP UTV007 USB](Images/easycap.png)

## *Begin*
The following will assume that you have created a dir `~/.local/sbin` within which you store the bash-file; this is to set the script as executable for current user only:

```bash
$ chmod 0700 ~/.local/sbin/encode_stream
$ la ~/.local/sbin/add_chapters
-rwx------ 1 user user 5846 Dec 21  2021 /home/user/.local/sbin/encode_stream
```
## *Help*
Attempting to run the bare script with zero parameters shows a Help message:

```bash
$ ~/.local/sbin/encode_stream
!Fatal Error! No OUTPUT_NAME in command.

usage: /home/user/.local/sbin/encode_stream OUTPUT_NAME [AUDIO_DEVICE] [VIDEO_DEVICE] [REGION] [PIX_FMT]

Encodes input from a VHS / Camera / Cassette stream to a mp4 video.

   OUTPUT_NAME     filename of mp4 video       (DEFAULT; no need for mp4 suffix                   )
               or, filename of m4a sound file  (needs m4a suffix                                  )
               or, filename of mp3 sound file  (needs mp3 suffix                                  )
   VIDEO_DEVICE    eg '/dev/video0' (try "v4l2-ctl --all"                                         )
   AUDIO_DEVICE    eg 'hw:2,0'      (try "arecord -l" or "arecord -L" or "cat /proc/asound/cards" )
   REGION          eg 'PAL'         (qv4l2 tool (QT v4l2 test utility) will help test for Region  )
   PIX_FMT         eg 'yuv420p'     (v4l2 default is yuyv422; will prevent display on some devices)

Note:
  Only use "q" to quit from the running process in the terminal
```
## *Hardware*
This may be the hardest part.    
I chose *EasyCAP UTV007* because others had reported that it was recognised by Linux & did the job (which it did). If you have any problems at this stage I cannot help, but *can* report on what happens in the background.

Plugging the USB2 lead into the desktop computer auto-creates video + audio devices via the interaction of V4L with the kernel:–
```
$ ls -l /dev/video*
crw-rw----+ 1 root video 81, 0 Sep 12 08:34 /dev/video0
crw-rw----+ 1 root video 81, 1 Sep 12 08:34 /dev/video1
```

## *Software*
You may need to install ffmpeg.    
You may need to install Video for Linux (`v4l-utils` + `qv4l2` as a minimum):
```bash
$ apt search v4l
Sorting... Done
Full Text Search... Done
…
dov4l/stable,now 0.9+repack-1+b1 amd64 [installed]
  program to set and query settings of video4linux devices

dv4l/stable,now 1.0-5+b2 amd64 [installed]
  Redirect V4L API to access a camcorder from a V4L program

libv4l-0/stable,now 1.22.1-5+b2 amd64 [installed,automatic]
  Collection of video4linux support libraries

libv4l2rds0/stable,now 1.22.1-5+b2 amd64 [installed,automatic]
  Video4Linux Radio Data System (RDS) decoding library

libv4lconvert0/stable,now 1.22.1-5+b2 amd64 [installed,automatic]
  Video4linux frame format conversion library

qv4l2/stable,now 1.22.1-5+b2 amd64 [installed]
  Test bench application for video4linux devices

v4l-conf/stable,now 3.107-1.1 amd64 [installed]
  tool to configure video4linux drivers

v4l-utils/stable,now 1.22.1-5+b2 amd64 [installed]
  Collection of command line video4linux utilities
```

## *Final Check*
Beware your user!

Once you have discovered your Video + Audio device locations, then use `ls -l` to discover the user-permissions. It may be necessary to act-as-root with this script for it to be effective. Alternatively, if necessary you could:

    `sudo chmod a+r /dev/video0`

...to change the file-mode to allow your user permission to access the device(s).
