# ffmpeg-batch-srt-extractor
ffmpeg - Advanced SubStation Alpha (ASS) to SRT files

# Windows .bat file code

```bat
@echo off

setlocal enabledelayedexpansion

set "input_folder=%CD%"

for %%F in ("%input_folder%\*.mkv") do (
    set "filename=%%~nF"
    set "filename=!filename:.=!"
    set "output_file=%%~dpnF.en.srt"
    ffmpeg -i "%%F" -map 0:s:0 "!output_file!"
)

endlocal


```
Automatically takes any .mkv file with .ASS subtitles and generates .en.srt subtitle files with the same name for PLEX. You must have ffmpeg installed on your machine.

![](https://i.imgur.com/nFzZo3e.gif)
# How to use on Windows

Open notepad and enter the above code where you saved your .mkv files and save as "subtitle_generator.bat"

Once saved, double click on the .bat file and you should see the .en.SRT files be generated for each .mkv file in that respective folder.
This preserves the original .mkv files and still contain the .ASS embedded subtitles but rips out .SRT file for Plex.

# Linux bash script

```bash
#!/bin/bash

input_folder=$(pwd)

for file in "$input_folder"/*.mkv; do
    filename=$(basename -- "$file")
    filename="${filename%.*}"
    output_file="${file%.*}.en.srt"
    ffmpeg -i "$file" -map 0:s:0 "$output_file"
done
```

# How to use on Linux
Open a text editor and copy the above code into a new file.
Modify the input_folder variable with the actual path to your folder containing the MKV files.
Save the file with a .sh extension, for example, subtitle_extraction.sh.
