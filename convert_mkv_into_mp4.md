# Convert MKV Video into MP4 Format

Use `ffmpeg` is probably the easiest method. 

```
$ ffmpeg -i Cars.2006.mkv -codec copy Cars.2006.mp4
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
$ ffmpeg -f concat -i mylist.txt -c copy video_draft.avi
```

Make a new list

```
ls *.avi | while read each; do echo "file '$each'" >> mylist.txt; done
```

***

[Back to HitichHikder's Guide by Herbert](README.md)