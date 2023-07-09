# ffmpeg-batch-srt-extractor
ffmpeg - Advanced SubStation Alpha (ASS) to SRT files

# Windows .bat file code

```
@echo off

for %%F in ("C:\path\*.mkv") do (
    ffmpeg -i "%%F" -map 0:s:0 "%%~dpnF.en.srt"
)

```
Automatically takes any .mkv file with .ASS subtitles and generates .en.srt subtitle files with the same name for PLEX.

![](https://i.imgur.com/nFzZo3e.gif)
# How to use

Open notepad and enter the above code with the proper path of where you saved your .mkv files and save as "subtitle_generator.bat"

Once saved, double click on the .bat file and you should see the .en.SRT files be generated for each .mkv file in that respective folder.
This preserves the original .mkv files and still contain the .ASS embedded subtitles but rips out .SRT file for Plex.
