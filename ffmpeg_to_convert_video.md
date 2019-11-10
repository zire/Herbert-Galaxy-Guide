# Convert Video/Audio Files with ffmpeg

Convert video file without re-encoding, use `copy` flag. Re-encoding will take a very long time. Use `map` to map all streams from input to output.

```
$ ffmpeg -i Cars.2006.mkv -vcodec copy -acodec copy -map 0 Cars.2006.mp4
```

Say, there are 3 audio tracks on the input, in order to keep all 3 tracks on the output, 

```
$ ffmpeg -i in.mp4 -vcodec copy -c:a copy -map 0:0 -map 0:1 -map 0:2 out.mp4
```

To [batch-convert multiple media files into another format with ffmpeg](https://stackoverflow.com/questions/5784661/how-do-you-convert-an-entire-directory-with-ffmpeg):

```
$ for i in *.avi; do ffmpeg -i "$i" "${i%.*}.mp4"; done
```

To [join multiple files into one single media file](https://stackoverflow.com/questions/15186500/howto-merge-two-avi-files-using-ffmpeg):

Create a file, `mylist.txt`

```
file '/path/here/file1.avi'
file '/path/here/file2.avi'
file '/path/here/file3.avi'
```
Then pass that file to ffmpeg

```
$ ffmpeg -f concat -i mylist.txt video_draft.avi
```

Make a new list

```
$ ls *.avi | while read each; do echo "file '$each'" >> mylist.txt; done
```

Display video info

```
$ ffmpeg -i video_file.mp4 -hide_banner
```

Convert media format. This will trigger re-encoding, which can take quite a long time.

```
$ ffmpeg -i video_input.mp4 video_output.avi
$ ffmpeg -i audio_input.wav audio_output.flac
```

Convert file into multiple output formats

```
$ ffmpeg -i audio_input.wav audio_output_1.mp3 audio_output_2.ogg
```

To see a list of all the supported formats

```
$ ffmpeg -formats
```

Additionally, you could specify codecs you want to use, adding `-c:a` (for audio) and `-c:v` (for video) followed by the name of the codecs, or `copy`if you want to use the same codecs as the original file

```
$ ffmpeg -i video_input.mp4 -c:v copy -c:a libvorbis video_output.avi
```

To extract audio from a video file, you do a simple conversion and add the `-vn` flag:

```
$ ffmpeg -i video.mp4 -vn audio.mp3
```

Set bit rate for the output audio file

```
$ ffmpeg -i video.mp4 -vn -ab 128k audio.mp3
```

To mute audio in a video, use `-an` flag

```
$ ffmpeg -i video_input.mp4 -an -video_output.mp4
```

Add subtitles to a video

```
$ ffmpeg -i video.mp4 -i subtitles.srt -c:v copy -c:a copy -preset veryfast -c:s mov_text -map 0 -map 1 output.mp4
```

## References

[Official ffmpeg site](http://ffmpeg.org/)

[ffmpeg converting from mkv to mp4 without re-encoding](https://stackoverflow.com/questions/40077681/ffmpeg-converting-from-mkv-to-mp4-without-re-encoding)

[FFmpeg not copying all audio streams](https://stackoverflow.com/questions/37820083/ffmpeg-not-copying-all-audio-streams)

[The Complete Guide for Using ffmpeg in Linux](https://itsfoss.com/ffmpeg/)

[Handbrake settings to convert MKV to MP4 while retaining the original quality](https://superuser.com/questions/472420/handbrake-settings-to-convert-mkv-to-mp4-while-retaining-the-original-quality)

[What is a Codec (e.g. DivX?), and how does it differ from a File Format (e.g. MPG)?](https://superuser.com/questions/300897/what-is-a-codec-e-g-divx-and-how-does-it-differ-from-a-file-format-e-g-mp/300997#300997)



***

[Back to HitichHikder's Guide by Herbert](README.md)