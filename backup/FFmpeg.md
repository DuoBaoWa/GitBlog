FFmpeg 是一个非常强大的开源工具，常用于处理视频和音频文件。它支持转换格式、剪切视频、提取音频等多种功能。下面是一些 **FFmpeg 常用功能**：

### 1. **视频格式转换**

将视频从一种格式转换为另一种格式。

```bash
ffmpeg -i input.mp4 output.avi
```

这里，`input.mp4` 是输入文件，`output.avi` 是输出文件。



### 2. **提取视频中的音频**

将视频中的音频提取为 MP3 格式。

```bash
ffmpeg -i input.mp4 -vn -acodec mp3 output.mp3
```

- `-vn` 表示不处理视频部分。
- `-acodec mp3` 指定音频编码为 MP3。

### 3. **提取视频封面（第一帧）**

从视频中提取封面图（第一帧）。

```bash
ffmpeg -i input.mp4 -ss 00:00:01 -vframes 1 output.jpg
```

- `-ss` 指定从视频的某一时刻开始提取（这里是 1 秒）。
- `-vframes 1` 表示提取 1 帧。

### 4. **裁剪视频（截取部分时间段）**

裁剪视频，只保留指定的时间段。

```bash
ffmpeg -i input.mp4 -ss 00:01:00 -to 00:05:00 -c copy output.mp4
```

- `-ss` 指定开始时间。
- `-to` 指定结束时间。
- `-c copy` 表示复制流，不重新编码，保证速度和质量。

### 5. **合并多个视频**

将多个视频文件合并为一个文件（要求所有视频格式、编码一致）。

```bash
ffmpeg -f concat -safe 0 -i filelist.txt -c copy output.mp4
```

- ```
  filelist.txt
  ```

   是包含视频文件路径的文本文件，格式如下：

  ```
  file 'video1.mp4'
  file 'video2.mp4'
  ```

### 6. **压缩视频（调整视频大小）**

通过改变分辨率来压缩视频大小。

```bash
ffmpeg -i input.mp4 -vf "scale=1280:720" -c:a copy output.mp4
```

- `-vf "scale=1280:720"` 指定视频的输出分辨率。

### 7. **添加水印（图片或文字）**

在视频上添加图片水印。

```bash
ffmpeg -i input.mp4 -i watermark.png -filter_complex "overlay=10:10" -c:a copy output.mp4
```

- `-i watermark.png` 是水印图片。
- `overlay=10:10` 设置水印的位置，左上角偏移 10px。

### 8. **调整视频帧率**

更改视频的帧率（例如将视频的帧率设置为 30fps）。

```bash
ffmpeg -i input.mp4 -r 30 output.mp4
```

### 9. **视频转GIF**

将视频转换为 GIF 动图。

```bash
ffmpeg -i input.mp4 -vf "fps=10,scale=320:-1:flags=lanczos" output.gif
```

- `fps=10` 设置 GIF 的帧率。
- `scale=320:-1` 保持宽度为 320px，自动计算高度，`-1` 代表自动调整。

### 10. **提取视频的音频并设置比特率**

提取音频并设置比特率（例如 128kbps）。

```bash
ffmpeg -i input.mp4 -vn -acodec mp3 -ab 128k output.mp3
```

- `-ab 128k` 设置比特率为 128kbps。

### 11. **调整视频速度（快放或慢放）**

将视频速度加快 2 倍。

```bash
ffmpeg -i input.mp4 -filter:v "setpts=0.5*PTS" output.mp4
```

- `setpts=0.5*PTS` 将视频速度加快两倍（0.5 表示加速）。

### 12. **添加字幕**

在视频中添加字幕文件。

```bash
ffmpeg -i input.mp4 -i subtitle.srt -c:v copy -c:a copy -c:s srt output.mp4
```

- `-i subtitle.srt` 是字幕文件。

### 13. **查看视频信息**

查看视频文件的详细信息（包括时长、分辨率、编码等）。

```bash
ffmpeg -i input.mp4
```

输出将包括视频流和音频流的详细信息。

### 14. **将视频转换为小片段（按时间切割）**

从视频中提取指定时间段的小片段。

```bash
ffmpeg -i input.mp4 -ss 00:02:00 -t 00:01:00 -c copy output.mp4
```

- `-ss` 是起始时间。
- `-t` 是持续时间。

### 15. **音频视频同步**

如果音频和视频不同步，可以通过调整音频延迟来同步它们。

```bash
ffmpeg -i input.mp4 -itsoffset 00:00:02 -i input.mp4 -map 0:v -map 1:a -c:v copy -c:a aac output.mp4
```

- `-itsoffset 00:00:02` 将音频延迟 2 秒来同步。

以下是更多 **FFmpeg 常用功能**，进一步展示 FFmpeg 在音视频处理中的强大功能：

### 16. **调整音频音量**

增加或减少音频的音量。

```bash
ffmpeg -i input.mp4 -filter:a "volume=1.5" output.mp4
```

- `volume=1.5` 表示音量增大 1.5 倍。如果设置为 `0.5`，则音量减小至原来的 50%。

### 17. **视频转码并调整质量**

通过设置视频编码器和 CRF（Constant Rate Factor，常量质量因子）来控制输出视频的质量，CRF 值越低，质量越高（同时文件也越大）。

```bash
ffmpeg -i input.mp4 -c:v libx264 -crf 23 output.mp4
```

- `-c:v libx264` 使用 H.264 编码器。
- `-crf 23` 设置质量，范围是 0 到 51，默认值是 23，值越小质量越好。

### 18. **合并音频和视频**

将视频和音频文件合并为一个文件。

```bash
ffmpeg -i video.mp4 -i audio.mp3 -c:v copy -c:a aac -strict experimental output.mp4
```

- `-c:v copy` 表示视频流不重新编码。
- `-c:a aac` 使用 AAC 编码器来处理音频。

### 19. **提取视频特定时段的截图**

从视频中截取某一时段的截图。

```bash
ffmpeg -i input.mp4 -ss 00:01:30 -vframes 1 output.jpg
```

- `-ss 00:01:30` 从 1 分 30 秒开始提取。
- `-vframes 1` 提取 1 帧。

### 20. **将视频转为黑白**

将视频转换为黑白模式。

```bash
ffmpeg -i input.mp4 -vf hue=s=0 output.mp4
```

- `hue=s=0` 将饱和度（saturation）设置为 0，达到黑白效果。

### 21. **视频翻转**

将视频上下翻转或左右翻转。

- 上下翻转：

  ```bash
  ffmpeg -i input.mp4 -vf "vflip" output.mp4
  ```

- 左右翻转：

  ```bash
  ffmpeg -i input.mp4 -vf "hflip" output.mp4
  ```

### 22. **将多个音频合并为一个文件**

将多个音频文件合并成一个文件。

```bash
ffmpeg -i "concat:audio1.mp3|audio2.mp3" -acodec copy output.mp3
```

- `concat:` 用于连接音频文件。

### 23. **将视频帧提取为图片**

从视频中提取多帧图片（例如每 10 帧提取一张图片）。

```bash
ffmpeg -i input.mp4 -vf "fps=1" output%d.png
```

- `fps=1` 表示每秒提取一帧。
- `output%d.png` 会生成按数字命名的图片文件。

### 24. **为视频添加背景音乐**

将音频文件添加为视频的背景音乐。

```bash
ffmpeg -i input.mp4 -i background_music.mp3 -c:v copy -c:a aac -strict experimental output.mp4
```

- `-i input.mp4` 是原始视频文件。
- `-i background_music.mp3` 是背景音乐文件。
- `-c:a aac` 使用 AAC 编码器进行音频编码。

### 25. **视频和音频格式转换**

将视频文件的音频部分转换为不同的格式，并保存为新的视频文件。

```bash
ffmpeg -i input.mp4 -vn -acodec libmp3lame output.mp3
```

- `-vn` 不处理视频部分。
- `-acodec libmp3lame` 使用 MP3 编码器处理音频。

### 26. **视频加速或减速**

改变视频播放速度。通过修改 `setpts` 和音频的 `atempo` 来调整速度。

- 加速视频播放（例如 2 倍速）：

  ```bash
  ffmpeg -i input.mp4 -filter:v "setpts=0.5*PTS" -filter:a "atempo=2" output.mp4
  ```

- 减慢视频播放（例如 0.5 倍速）：

  ```bash
  ffmpeg -i input.mp4 -filter:v "setpts=2.0*PTS" -filter:a "atempo=0.5" output.mp4
  ```

### 27. **去除视频中的音频**

从视频中移除音频部分，只保留视频。

```bash
ffmpeg -i input.mp4 -an output.mp4
```

- `-an` 表示不处理音频部分。

### 28. **调整视频的音频轨道**

如果视频文件有多个音频轨道，可以选择合并其中一个音频轨道。

```bash
ffmpeg -i input.mp4 -map 0:v -map 0:a:1 -c copy output.mp4
```

- `-map 0:v` 选择视频流。
- `-map 0:a:1` 选择第二个音频轨道（假设音频轨道从 0 开始计数）。

### 29. **提取视频的封面（ID3 标签）**

从视频文件的元数据中提取封面图片。

```bash
ffmpeg -i input.mp4 -an -vn -f image2 output.jpg
```

- `-an` 忽略音频流。
- `-vn` 忽略视频流。

### 30. **视频旋转**

对视频进行旋转，常用于修正视频的方向。

- 旋转 90 度：

  ```bash
  ffmpeg -i input.mp4 -vf "transpose=1" output.mp4
  ```

- `transpose=1` 旋转 90 度顺时针。

- 旋转 180 度：

  ```bash
  ffmpeg -i input.mp4 -vf "transpose=2,transpose=2" output.mp4
  ```

以下是更多 **FFmpeg 的实用功能和高级用法**：

------

### 31. **改变音频采样率**

调整音频的采样率（例如从 48kHz 转为 44.1kHz）。

```bash
ffmpeg -i input.mp3 -ar 44100 output.mp3
```

- `-ar 44100` 设置采样率为 44.1kHz。

------

### 32. **调整视频的码率**

通过改变码率来控制视频文件的大小和质量。

```bash
ffmpeg -i input.mp4 -b:v 1000k output.mp4
```

- `-b:v 1000k` 设置视频比特率为 1000kbps。

------

### 33. **音频降噪**

对音频文件进行简单的降噪处理。

```bash
ffmpeg -i noisy_audio.mp3 -af "highpass=f=200, lowpass=f=3000" clean_audio.mp3
```

- `highpass` 和 `lowpass` 滤波器可以移除音频中的低频和高频噪声。

------

### 34. **在视频上添加文字**

在视频上添加静态文字。

```bash
ffmpeg -i input.mp4 -vf "drawtext=text='Hello World':fontcolor=white:fontsize=24:x=10:y=10" output.mp4
```

- `drawtext` 滤镜用于添加文本。
- `x=10:y=10` 设置文本位置。

------

### 35. **多线程加速编码**

指定使用多个线程来加速处理。

```bash
ffmpeg -i input.mp4 -c:v libx264 -threads 4 output.mp4
```

- `-threads 4` 表示使用 4 个线程。

------

### 36. **生成缩略图序列**

从视频中按固定间隔生成多个缩略图。

```bash
ffmpeg -i input.mp4 -vf "fps=1" thumbnail_%03d.jpg
```

- `fps=1` 表示每秒提取一帧。
- `thumbnail_%03d.jpg` 生成按序编号的图片。

------

### 37. **更改视频分辨率**

调整视频分辨率。

```bash
ffmpeg -i input.mp4 -vf "scale=1920:1080" output.mp4
```

- `scale=1920:1080` 设置分辨率为 1920x1080。

------

### 38. **调整音频通道**

将立体声音频（双声道）转换为单声道。

```bash
ffmpeg -i stereo.mp3 -ac 1 mono.mp3
```

- `-ac 1` 将音频通道数设置为 1（单声道）。

------

### 39. **提取视频元数据**

提取视频文件的元数据并显示详细信息。

```bash
ffmpeg -i input.mp4 -f ffmetadata metadata.txt
```

- 输出的 `metadata.txt` 包含视频的详细元数据信息。

------

### 40. **循环播放音频**

将音频文件循环播放指定次数。

```bash
ffmpeg -stream_loop 2 -i input.mp3 -c copy output.mp3
```

- `-stream_loop 2` 表示循环播放两次。

------

### 41. **截取视频最后几秒**

提取视频的最后 10 秒。

```bash
ffmpeg -sseof -10 -i input.mp4 -c copy output.mp4
```

- `-sseof -10` 表示从视频结尾倒数 10 秒开始。

------

### 42. **移除视频文件的元数据**

清除视频文件的所有元数据信息。

```bash
ffmpeg -i input.mp4 -map_metadata -1 -c:v copy -c:a copy output.mp4
```

- `-map_metadata -1` 删除所有元数据。

------

### 43. **创建视频幻灯片**

将一系列图片转换为视频。

```bash
ffmpeg -framerate 1 -i img%d.jpg -c:v libx264 -pix_fmt yuv420p slideshow.mp4
```

- `-framerate 1` 表示每秒播放一张图片。
- `img%d.jpg` 表示图片按序编号。

------

### 44. **动态模糊视频**

为视频添加动态模糊效果。

```bash
ffmpeg -i input.mp4 -vf "boxblur=10:1" output.mp4
```

- `boxblur=10:1` 设置模糊半径和强度。

------

### 45. **添加背景颜色**

为视频添加背景颜色（通常用于竖屏视频的两侧）。

```bash
ffmpeg -i input.mp4 -vf "pad=ceil(iw/2)*2:ceil(ih*3/2):color=black" output.mp4
```

- `pad` 滤镜用于调整画布大小和填充背景颜色。

------

### 46. **视频帧间去重**

移除重复的帧，压缩视频时长。

```bash
ffmpeg -i input.mp4 -vf mpdecimate -vsync vfr output.mp4
```

- `mpdecimate` 用于去掉重复帧。
- `-vsync vfr` 保持可变帧率。

------

### 47. **视频实时流传输**

将视频以 RTMP 协议实时推流。

```bash
ffmpeg -re -i input.mp4 -c:v libx264 -f flv rtmp://server/live/stream_key
```

- `-f flv` 指定输出格式为 FLV（Flash 视频流）。
- `rtmp://server/live/stream_key` 是推流地址。

------

### 48. **视频分段切割**

将视频文件切割为多个小文件。

```bash
ffmpeg -i input.mp4 -f segment -segment_time 60 -c copy output%03d.mp4
```

- `-segment_time 60` 每段视频的时长为 60 秒。
- `output%03d.mp4` 输出文件按编号命名。

------

### 49. **实时录屏**

通过 FFmpeg 录制屏幕内容。

```bash
ffmpeg -f gdigrab -i desktop -framerate 30 -c:v libx264 output.mp4
```

- `-f gdigrab` 是 Windows 下的屏幕捕获模式。
- `desktop` 表示捕获整个屏幕。

------

### 50. **将音频转换为波形图**

将音频生成一个波形图视频。

```bash
ffmpeg -i input.mp3 -filter_complex "showwavespic=s=640x240" -frames:v 1 waveform.png
```

- `showwavespic` 生成波形图片。

------

### 51. **提取多路音频**

如果视频文件包含多条音轨，可以提取特定音轨。

```bash
ffmpeg -i input.mp4 -map 0:a:1 output_audio2.mp3
```

- `-map 0:a:1` 提取第二条音轨。

------

### 52. **音视频同步修正**

修正音频和视频不同步的问题（手动设置延迟）。

```bash
ffmpeg -i input.mp4 -itsoffset 0.5 -i input.mp4 -map 0:v -map 1:a -c copy output.mp4
```

- `-itsoffset 0.5` 将音频延迟 0.5 秒。



---

## **一、烧录字幕（硬字幕）到视频中**

这种方法会将字幕直接渲染到视频画面中，无法关闭。

### **步骤：**

1. **准备字幕文件**：确保您有与视频匹配的字幕文件，一般为SRT或ASS格式。

2. **使用FFmpeg命令烧录字幕**：

   **对于SRT字幕：**

   ```bash
   ffmpeg -i input.mp4 -vf subtitles=subtitles.srt -c:a copy output.mp4
   ```

   **对于ASS字幕：**

   ```bash
   ffmpeg -i input.mp4 -vf ass=subtitles.ass -c:a copy output.mp4
   ```

   - `input.mp4`：您的原始视频文件。
   - `subtitles.srt`或`subtitles.ass`：您的字幕文件。
   - `-vf subtitles=subtitles.srt`或`-vf ass=subtitles.ass`：使用视频滤镜将字幕烧录到视频中。
   - `-c:a copy`：复制音频，不重新编码。

### **注意事项：**

- **字幕编码**：确保字幕文件的编码为UTF-8，无BOM头，避免出现乱码。
- **字体问题**：对于ASS字幕，若涉及自定义字体，需确保播放设备支持，或将字体嵌入字幕文件。

---

## **二、嵌入软字幕到视频中**

这种方法会将字幕作为独立的流嵌入视频文件，播放时可以选择开启或关闭字幕。

### **步骤：**

1. **准备字幕文件**：SRT、ASS等格式均可。

2. **选择合适的容器格式**：

   - **MKV容器**：支持多种字幕格式，兼容性好。
   - **MP4容器**：支持的字幕格式有限，一般为mov_text。

3. **将字幕嵌入MKV文件**：

   ```bash
   ffmpeg -i input.mp4 -i subtitles.srt -c copy -c:s srt output.mkv
   ```

   - `-c copy`：复制所有流，不重新编码。
   - `-c:s srt`：指定字幕编码格式为SRT。

4. **将字幕嵌入MP4文件**：

   ```bash
   ffmpeg -i input.mp4 -i subtitles.srt -c copy -c:s mov_text output.mp4
   ```

   - `-c:s mov_text`：将字幕转换为MP4容器支持的mov_text格式。

### **注意事项：**

- **播放器支持**：并非所有播放器都支持MP4中的软字幕，MKV的兼容性更好。
- **字幕格式限制**：MP4容器对字幕格式有限制，可能需要转换字幕格式。

---

## **三、附加技巧**

### **1. 多语言字幕**

可以同时嵌入多条字幕轨道：

```bash
ffmpeg -i input.mp4 -i english.srt -i chinese.srt -map 0 -map 1 -map 2 -c copy -c:s srt output.mkv
```

- `-map`参数用于指定流的映射。

### **2. 指定字幕语言**

为字幕流添加语言标签：

```bash
ffmpeg -i input.mp4 -i subtitles.srt -c copy -c:s srt -metadata:s:s:0 language=eng output.mkv
```

- `-metadata:s:s:0 language=eng`：为第一个字幕流指定语言为英语。

### **3. 字幕样式调整**

对于ASS字幕，可以自定义样式，或使用FFmpeg滤镜调整：

```bash
ffmpeg -i input.mp4 -vf "ass=subtitles.ass:fontsdir=/path/to/fonts" -c:a copy output.mp4
```

- `fontsdir`：指定字体文件所在目录。

---

## **总结**

- **硬字幕**适用于希望字幕永久显示的情况，兼容性高，但无法关闭。
- **软字幕**提供了灵活性，用户可以选择开启或关闭，但需要考虑播放器的支持情况。
- **容器格式**：MKV容器对字幕支持更友好，推荐使用。

希望以上方法能帮助您成功在视频中插入字幕！

