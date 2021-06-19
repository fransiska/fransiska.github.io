---
layout: post
title: Recording with ffmpeg
tags: [ffmpeg, video]
---

Get the list of video format, size, and framerate that your camera supports

```bash
v4l2-ctl --list-formats-ext
```

Record the stream using the camera's native h264 encoding, 1920x1080 resolution, save the video format as is, record for 1 minute, name the file with current date time.

```bash
ffmpeg -f v4l2 -input_format h264 -s 1920x1080 -i /dev/video0 -c:v copy -t 00:01:00 $(date +"%Y%m%d%H%M%S").mp4
```

It should say out the the input stream is

```
Input #0, video4linux2,v4l2, from '/dev/video0':
  Duration: N/A, start: 9005.983108, bitrate: N/A
    Stream #0:0: Video: h264 (Constrained Baseline), yuvj420p(pc, progressive), 1920x1080 [SAR 1:1 DAR 16:9], 30 fps, 30 tbr, 1000k tbn, 60 tbc
```

And the stream mapping is

```
Stream mapping:
  Stream #0:0 -> #0:0 (copy)
```

### Camera controls

(Resetted after reboot I think)

```bash
v4l2-ctl -d /dev/video3 -l
v4l2-ctl -d /dev/video3 --set-ctrl zoom_absolute=125
```

To turn off camera's LED, where video3 is the same index as the `/dev/video3`

```bash
uvcdynctrl -d video3 -s 'LED1 Mode' 0
```

### Streaming to vlc in the same network

Where `192.168.1.2` is the ip address of the viewer,

```bash
ffmpeg -f v4l2 -input_format mjpeg -s 800x600 -i /dev/video3 -tune zerolatency  -f mjpeg udp://192.168.1.2:23000?pkt_size=1316
```

In viewer's vlc, File -> Open Network `udp://@:23000?pkt_size=1316`


