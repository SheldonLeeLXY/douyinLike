### 代码基本为原作者 [tomxin7](https://github.com/tomxin7) 所写，我改了一些逻辑处理和更新API。  

## 什么是抖音

> 抖音是2016年9月上线的一款音乐创意短视频社交软件，是一个专注年轻人的15秒音乐短视频社区。用户可以通过这款软件选择歌曲，拍摄15秒的音乐短视频，形成自己的作品。


## 效果
抖音经常能刷到很多高质量的视频，特别是我们使用的越多，头条的算法给我们推荐的内容越精准。**那么我们可不可以写一个小型的程序，根据自己设置的特征筛选视频并且自动点赞存入我们的收藏夹中呢？比如漂亮的小姐姐，帅气的小哥哥或者是可爱的喵星人。。。**
<!--more-->


![](https://github.com/zhanglihow/DouYinFaceTech/blob/master/20180418_000727.gif)
## 原理说明

##### 本程序与抖音无关，主要供学习用途

1，将手机打开抖音的推荐视频界面

2，用 ADB 工具获取当前手机截图，并用 ADB 将截图 pull 上来

```
adb shell screencap -p /sdcard/autojump.png
adb pull /sdcard/autojump.png .
```

3，将图片进行压缩,并调用[百度人脸识别API](http://ai.baidu.com/tech/face)（目前使用的是v3的API）

4，获得百度返回的数据进行判断分析

5，如果满足要求，使用ADB点赞

6，上滑切换新视频 





## 使用教程


#### 1、获取源码

git命令
```
git clone https://github.com/zhanglihow/DouYinFaceTech.git
``` 
#### 2、依赖
```
Python：3.6.3
ADB下载：http://adbshell.com/downloads
依赖：pip install pillow 
```
#### 3、准备
```
使用数据线连接手机与电脑，并开启调试模式
申请百度人脸检测申请Key FaceMain.py中替换token的host链接

```
#### 4、运行

```
手机打开抖音首页
DouYinFaceTech目录下直接运行FaceMain.py

```
#### 5、可能遇到的问题


1，运行py文件不成功，出现cmd后闪退，建议这样运行有错误提示

```
cd 项目目录
python FaceMain.py
```

  
  2，检测到中意的人脸后代码执行 GetDouYinImg.py 的 click_like() 方法时，手机未能点击成功
  

```
def click_like():
    os.system("adb shell input tap 950 850")#点击事件
```
需要对应你的手机来更改位置
可以用AndroidStudio  

<img src="https://github.com/zhanglihow/DouYinFaceTech/blob/master/pic/as1.jpg" width="500" hegiht="500" align=center />
<img src="https://github.com/zhanglihow/DouYinFaceTech/blob/master/pic/as2.png" width="500" hegiht="500" align=center />
<img src="https://github.com/zhanglihow/DouYinFaceTech/blob/master/pic/as3.png" width="500" hegiht="500" align=center />

这样就拿到这个‘喜欢’按钮的像素位置，取个中心值就可以了。

### 有遇到问题欢迎提issues,我尽量帮忙

参考：  
[https://github.com/tomxin7/DouYinFaceTech](https://github.com/tomxin7/DouYinFaceTech)  
[https://github.com/wangshub/Douyin-Bot](https://github.com/wangshub/Douyin-Bot)
