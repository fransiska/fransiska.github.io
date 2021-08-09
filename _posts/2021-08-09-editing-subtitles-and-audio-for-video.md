---
layout: post
title: Editing subtitles and audio for video
---

1. Took video with iPhone
2. Copy video to MacBook using AirDrop
3. Edit video sequence (cut and paste and rearrange), change speed, transition. Subtitling in iMovie sucks, so I only do the video transitions here, which is what it does best. Cropping and rearranging is very smooth.
4. Export video using `File -> Share -> File`
5. Use [Aegisub](https://github.com/Aegisub/Aegisub/releases) to create a subtitle file. I've known this program since a long time ago and it's amazing that it still works with Mac OS Catalina. The audio spectrum display is amazing as well. It's really stable. I'm very impressed.
6. Extract audio from the video, use m4a, saving it with aac extension will cause the audio to have incorrect length. I specified the bitrate and sampling frequency.
   ```bash
   ffmpeg -i video.mp4 -vn -b:a 102k -ar 48000 -acodec copy video.m4a
   ```
7. Open in Audacity (To open m4a files, make sure to download and install the ffmpeg library from [Audacity guide](https://manual.audacityteam.org/man/installing_ffmpeg_for_mac.html), it requires a specific version and it says it won't get conflict with ffmpeg installed using brew), check the high pitch frequency using `Anaylze -> Plot Spectrum`
8. Select All (Cmd + A), Apply `Effect -> Low Pass Filter` with desired frequency and 48db for Roll-off to remove the high pitched noise
9. Replace old video's audio with the edited audio without reencoding the video (Really fast!)
   ```bash
   ffmpeg -i video.mp4 -i audio.m4a -c:v copy -map 0:v:0 -map 1:a:0 new_video.mp4
   ```
10. Open Handbrake, load the video. In the Subtitles tab, at the dropdown for Tracks, click `Add External Subtitles Track...` and select the previously created subtitle (works with Aegisub's .ass file)
11. Start encoding!
