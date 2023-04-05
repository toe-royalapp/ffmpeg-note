ffmpeg
** basic syntax
$ ffmpeg -i input.mp4 output.mp3
$ ffplay output.mp3

** specifying quality
$ ffmpeg -i <input file> -q <qty> <out file>
$ ffmpeg -i atom.avi -q 23 quality_23.mp4
//(q 1 -> 100) lower q -> lower size
$ ffmpeg -i <input file> -crf <qty> <out file>

** to specify exact bitrates
$ ffmpeg -i <input file> -b:a <bitrate> <out file> //for audio
$ ffmpeg -i <input file> -b:v <bitrate> <out file> //for video

** volume tweak
$ ffmpeg -i <input file> -filter:a "volume=2" <out file> // 2 - double vol

** channel remapping
$ ffmpeg -i <input file> -filter:a "channelmap=0-0|0-1" <out file>

** cropping
$ ffmpeg -i <input file> -filter:v "crop=w=640:h=480:x=100:y=200" <out file>
// w, h, x, y = width, height, top, left corner
$ ffmpeg -i <input file> -filter:v "crop=w=2/3*in_w:h=2/3*in_h" <out file>

** rotation
$ ffmpeg -i <input file> -filter:v "rotate=45*PI/180" <out file>

** unsharp photo
$ ffmpeg -i inp.jpg -filter "unsharp" out.jpg

** scaling
$ ffmpeg -i <input file> -filter:v "scale=w=640:h480" <out file>
$ ffmpeg -i <input file> -filter:v "scale=w=2/3*in_w:h=2/3*in_h" <out file>
$ ffmpeg -i <input file> -filter:v "scale=w=852:h=-1" <out file>

$ ffmpeg -i atom.mp4 -c:v vp9 -c:a libvorbis out.webm

$ ffmpeg -i atom.mp4 -c:a copy -c:v libx264 -b:v 99K output.mp4

$ ffmpeg -i atom.mp4 -c:a copy -c:v libx264 -b:v 3M output.mp4

$ ffmpeg -i atom.mp4 -c:a copy -c:v libx264 -r 24 output.mp4
// 24 is frame rate (if 1 = like photo)

$ ffmpeg -i atom.mp4 -c:a copy -c:v libx264 -s 920x1200 output.mp4
// -s size, 920x1200 width x height

$ ffmpeg -i atom.mp4 -c:a copy -c:v libx264 -r 1 -s 920x1200 output.mp4
// frame rate 1 with size 920x1200

$ ffmpeg -i atom.mp4 -c:a copy -c:v libx264 -b:v 1M -r 1 -s 1800x4200 output.mp4

$ ffmpeg -i atom.mp4 -ss 00:00:6 -t 2 output.mp4
// start from 6 second, finish after 2 second

$ ffmpeg -i atom.mp4 -vn output.mp4
// like mp3 

$ ffmpeg -i atom.mp4 -i audio.m4a -map 0:v:0 -map 1:a:0 -c:v copy output.mp4

$ ffmpeg -i atom.mp4 -i audio.m4a -map 0:v:0 -map 1:a:0 -filter:a volume=0.5 -c:v copy output.mp4
// merge with filter

$ ffmpeg -i atom.mp4 -i audio.m4a -filter:a volume=2.0 output.mp4
// with high volume

$ ffmpeg -i atom.mp4 -i audio.m4a -filter:v "crop=120:72:0:0" output.mp4
// crop the with and side

$ ffmpeg -i atom.mp4 -i watermark.jpg -filter_complex "overlay=200:200" output.mp4
// add watermark with overlay position

$ ffmpeg -i atom.mp4 -c:v vp9 -filter:v "chromakey=0x00ff00:0.2:0.9" output.mp4

$ ffmpeg -i atom.mp4 -i atom2.mp4 -filter_complex "[0:v][1:v] overlay=250:250" output.mp4
// overlay with input2

$ ffmpeg -i atom.mp4 -vf scale=1920:-2 -an output.mp4
//optimize video for web

$ ffmpeg -i atom.mp4 -c:v libx264 -vf scale=1920:-2 -an output.mp4
// web tast with caniuse site

$ ffmpeg -i atom.mp4 -c:v libx264 -crf 24 -vf scale=1920:-2 -movflags faststart -an output.mp4
// with faststart , no sound

$ ffmpeg -i atom.mp4 -c:v libvpx-vp9 -crf 40 -vf scale=1920:-2 -an output.mp4
// with lib v9 

mux
demux => input.mp4 (demux) encode/decode (

file format
-----------
mp4 (youtube), webm(website) and ogg support by html
avi is best quality & large size (Microsoft)
mov is quick time (apple)

codec (coder and decoder)
-------------------------
The most used codec is H.264/ MPEG-4 AVC. H.264 
VP9 (Google)

specification
------------
mp4 - high-quality videos with a small file size.
mov - QuickTime - quite similar to MP4 but solves the major drawback of MP4
WMV - for online streaming and sharing video (produces videos in small sizes with decent quality)
WebM - best file format for embedding videos on websites (Google, open-source)
avi - low compression, resulting in large file sizes (Microsoft)
MKV - audio stream, video stream, and all metadata in a single file (does not compress data - all in one video and audio in single format)


https://caniuse.com/
https://docs.imagekit.io/