# 基于ffmpeg的针对telegram用户的动图制作小教程

## 制作"GIFS"。

为什么直接截取mp4片段上传telegram？
.gif是大家熟知的动态图片格式。许多聊天软件都使用该格式。不过，telegram在16年就已经将用户上传的.gif文件一律转码为了MPEG-4格式视频，也就是[x264编码的.mp4文件][1] 

[1]: https://telegram.org/blog/gif-revolution。

- gif格式只有256色，mp4->gif往往会有画质问题，比如potplayer录制gif（注1：解决办法，detail版notes）
- 在telegram有不错的解码器支持的情况下，mp4比gif体积小得多，效果也好

截取mp4的工具：ffmpeg

ffmpeg处理视频文件的功能强大，是各种播放器和其他工具的依赖。

ffmpeg入门（30分钟--1小时）:https://github.com/FiveYellowMice/how-to-convert-videos-with-ffmpeg-zh/blob/master/01-write-in-front.md

例子：LoliHouse小林家的妹抖龙09。

1. 先把大致的范围截取出来并解压为PNG图片

``
ffmpeg -ss 00:00:56 -t 3 -i "input.mkv" img%3d.png
``

2. 选择

``
ffmpeg -start_number 21 -framerate 24000/1001 -i img%3d.png -vframes 30 -c:v libx264 -pix_fmt yuv420p output1.mp4 
``

如果视频源是1080P，可能需要调整scale。（注2：安卓客户端可能会识别为"video"）
在解压图片时加入：

``
-vf "scale=400:226"
``

在本例子中，也就是修改第一行命令为

``
ffmpeg -ss 00:00:56 -t 3 -i "input.mkv" -vf "scale=400:226" img%3d.png
``

400是telegram显示"gif"的较长边的长度。如果需要节省整个制作过程的占用空间，以及上传流量，也可以这么做。

telegram的"gif"参数：

音频：无声音 -an 

视频: 
- format:x264
- fps:24000/1001?检查其他fps是否可行 尤其是手机可能出问题
- size:400x226? 400是拿截图工具量的，短边应该是225，但x264不支持非偶数

裁剪

references
[1]: https://telegram.org/blog/gif-revolution
