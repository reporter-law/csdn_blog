# 原创

： moviepy使用教程

# moviepy使用教程

### moviepy使用教程

# 一、剪辑成果

未来

# 二、遇到问题

尝试使用ffmpeg、moviepy、pydub，其中pydub主要是对音频的处理，moviepy对视频音频处理，ffmpeg视频、音频均可以，只是ffmpeg是命令行，在pycharm用起来不习惯，moviepy和pydub都是基于ffmpeg的python模块，<br/>
而ffmpeg也有python命令调用模块——ffmpeg-python是ffmpeg的命令调用库,链接: [ffmpeg-python](https://github.com/kkroening/ffmpeg-python).<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200722164005775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

但是csdn上大部分都是moviepy的教程，关于ffmpeg-python的教程非常少，因而再次我用的也是moviepy

moviepy和pydub直接用pip安装即可

```
pip install moviepy
pip install pydub

```

遇到问题：

```
AttributeError: 'str' object has no attribute 'decode'
UnicodeDecodeError: 'utf-8' codec can't decode byte 0x80 in position 7: invalid start byte

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020072216463125.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
第一个报错比较好解决，就是将decode去掉，但是造成第二个报错，两个报错互相循环，在github提问也没有回复。后来我下载了python3.8（原来用的是python3.7），重新pip installer
moviepy之后就好了，pudub也是如此

# 三、moviepy方法分享

方法推送到了github上，下载地址：链接: [video_method](https://github.com/reporter-law/video_method).

## 一、音频剪辑方法

```
from pydub import AudioSegment
from ffmpeg import audio


class Pydub_method():
def __init__(self,path1,path2,path3):
    # 1秒=1000毫秒
    self.SECOND = 1000#单位必须是毫秒
    self.path1 = path1
    self.path2 = path2
    self.path3 = path3



def get_audio(self,start_time,end_time):
    """音频剪辑"""
    song = AudioSegment.from_file(self.path1, format="mp3")
    # song_ = AudioSegment.from_file(r"J:\\vedio\\manager\\audio\\千秋令和朝代歌\\弥撒与千秋令混合.mp3", format="mp3")-6
    # song_ =song_.fade_in(5000).fade_out(5000)
    # newsong_1 = song[:55*SECOND]
    # newsong = newsong_1+song_+ song[60*SECOND:]
    newsong = song[start_time* self.SECOND:end_time * self.SECOND]
    newsong.export(self.path2)

def audio_concat(self):
    """音频混合"""
    sound1 = AudioSegment.from_file(self.path1) - 1
    sound2 = AudioSegment.from_file(self.path2) - 6
    sound2.fade_in(5000).fade_out(5000)

    played_togther = sound1.overlay(sound2)
    played_togther.export(self.path3)

def audio_fade(self,start_time,end_time):
    """音频淡入淡出"""
    song= AudioSegment.from_file(self.path1)
    song_1 = song.fade_in(start_time*self.SECOND).fade_out(end_time*self.SECOND)
    song_1.export(self.path2)


def audio_fast(self,speed):
    """音频加速，没有找到pydub中的音频加速"""
    audio.a_speed(self.path1, speed, self.path2)

```

## 二、视频剪辑方法

```
from moviepy.editor import *

class Moviepy_method():
def __init__(self,path1,path2,path3="‪J:\vedio",path4 = "‪J:\vedio\original"):
    self.input_path = path1.strip("\u202a")
    self.path2 = path2.strip("\u202a")
    self.path3 = path3.strip("\u202a")
    self.path4 = path4.strip("\u202a")

def Getaudio(self):
    """音频提取"""
    vedio1 = VideoFileClip(self.input_path.strip("\u202a"))
    audio1 = vedio1.audio
    audio1.write_audiofile(self.path2)


def getvideo(self,start_time,end_time):
    """视频提取"""
    vedio1 = VideoFileClip(self.input_path)
    # vedio2 = vedio1.without_audio()
    video2 = vedio1.subclip(start_time, end_time)
    # video4 = vedio2.subclip(9,-1)
    video2.write_videofile(self.path2)


def video_fast(self,number):
    """视频加速"""
    clipVideo = VideoFileClip(self.input_path)
    newclip = clipVideo.fl_time(lambda t: number * t, apply_to=['mask'], keep_duration=True)
    duration = int(clipVideo.duration / 2)
    newclip = newclip.subclip(0,duration)
    newclip.write_videofile(self.path2)

def video_drop(self):
    """视频无声"""
    video = VideoFileClip(self.input_path)
    video = video.without_audio()
    video.write_videofile(self.path2)

def video_concat(self):
    """视频合成"""
    video1 = VideoFileClip(self.input_path).fx(vfx.resize, width=848)
    video2 = VideoFileClip(self.path2).fx(vfx.resize, width=848)
    video3 = VideoFileClip(self.path3).fx(vfx.resize, width=848)
    # video4 = VideoFileClip(path4)
    final_clip = concatenate_videoclips([video1, video2, video3], method="compose")
    final_clip.to_videofile(self.path4, fps=24, remove_temp=False)

def audio_concat_vedio(self,audio_path):
    """音频视频合成"""
    video = VideoFileClip(self.path)
    audio = AudioFileClip(audio_path)
    video = video.set_audio(audio)  # 不能直接是audio的路径
    video.write_videofile(self.path2)

```
