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
Automatically takes any .mkv file with .ASS subtitles and generates .en.srt subtitle files with the same name for PLEX. 

![](https://i.imgur.com/nFzZo3e.gif)


⚠ **You need to install ffmpeg installed on your machine before you can run these scripts** ⚠

<details>
    <summary>For multi-stream subtitles, click here</summary>

    
### Find the English .ass stream
    
1. Run <code>ffmpeg -i your_file.mkv</code>to find the english subtitle stream number that it outputs, it should look like something below:

```
Stream #Z:X(language:... English)
```
2. Remember this number X
3. Paste this code output below and replace the X as the number that was saved in the previous step. This will tell ffmpeg which stream to extract.

```bat
@echo off

setlocal enabledelayedexpansion

set "input_folder=%CD%"

for %%F in ("%input_folder%\*.mkv") do (
    set "filename=%%~nF"
    set "filename=!filename:.=!"
    set "output_file=%%~dpnF.en.srt"
    ffmpeg -i "%%F" -map 0:X -c:s srt "!output_file!"
)

endlocal

```
    
</details>

# How to use on Windows

Open notepad and enter the above code where you saved your .mkv files and save as "subtitle_generator.bat"

Once saved, double click on the .bat file in the same folder as the mkv and you should see the .en.SRT become generated for each .mkv file in that respective folder.
This preserves the original .mkv files and still contain the .ASS embedded subtitles but rips out .SRT file for Plex so that you 

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
Save the file with a .sh extension, for example, subtitle_extraction.sh.
run `chmod u+x subtitle_extraction.sh` to make it executable
run `./subtitle_extraction.sh` in the folder of the mkv files
You should see the generated en.srt files


