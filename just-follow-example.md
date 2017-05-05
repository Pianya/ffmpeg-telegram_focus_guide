# 

ffmpeg -ss 00:00:57 -t 3 -i input.mkv -vf "scale=1280:720" img%3d.png
ffmpeg -start_number 21 -framerate 24000/1001 -i img%3d.png -c:v libx264 -vframes 30 -pix_fmt yuv420p output.mp4
