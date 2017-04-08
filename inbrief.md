# 大纲

## 制作"gif"。

为什么直接截取mp4片段上传telegram？

1. telegram会将gif文件转换成mp4。
2. gif格式只有256色，mp4->gif往往会有画质问题，比如potplayer录制gif（注1：解决办法，detail版notes）
3. 在telegram有不错的解码器支持的情况下，mp4比gif体积小得多，效果也好

截取mp4的工具：ffmpeg

ffmpeg处理视频文件的功能强大，是各种播放器和其他工具的依赖。

ffmpeg入门（30分钟--1小时）:https://github.com/FiveYellowMice/how-to-convert-videos-with-ffmpeg-zh/blob/master/01-write-in-front.md

例子：LoliHouse小林家的妹抖龙09。
``
ffmpeg -ss 00:00:56 -t 3 -i "input.mkv" img%3d.png
``

先把大致的范围截取出来

``
ffmpeg -start_number 21 -framerate 24000/1001 -i img%3d.png -vframes 30 -c:v libx264 -pix_fmt yuv420p output1.mp4 
``


telegram的"gif"参数：

音频：无声音 -an 

视频: 
- format:x264
- fps:24000/1001?检查其他fps是否可行 尤其是手机可能出问题
- size:400x226? 400是拿截图工具量的，短边应该是225，但x264不支持非偶数

裁剪
