# Encode-Stream
A BASH Script to encode VHS / Camera / Cassette Streams

## *Basics*
This script file is designed for use by any-user (no root access required) within a Terminal. It’s principal purpose is to make it easy & reliable to encode a stream from a VHS, Camera or Cassette player to a video file. It has been used extensively by myself to transfer all my VHS tapes (using a EasyCAP UTV007 USB converter) & cassettes (using a USB-powered cassette player) to disc under *Devuan* (a systemD-free version of *Debian*). In addition to BASH, the main utility required is FFMPEG. Note that zero efforts are made to test for the presence of FFMPEG before use.

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

   OUTPUT_NAME     filename of mp4 video       (DEFAULT; no need for .mp4 suffix                      )
               or, filename of m4a sound file  (needs .m4a suffix                                     )
               or, filename of mp3 sound file  (needs .mp3 suffix                                     )
   VIDEO_DEVICE    eg 'dev/video0' (try "v4l2-ctl --all"                                              )
   AUDIO_DEVICE    eg 'hw:2,0'     (try "arecord -l" or "arecord -L" or "cat /proc/asound/cards"      )
   REGION          eg 'PAL'
   PIX_FMT         eg 'yuv420p'    (v4l2 default is yuyv422, but that prevents display on some devices)

Note:
  Only use "q" to quit from the running process in the terminal
```
