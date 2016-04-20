---
layout:     post
title:      "我对windows10有意见"
subtitle:   "It's hard to solve Windows updates Bugs"
date:       2016-04-19
author:     "Lucas"
catalog: true
tags:
    - encoding
---

我的笔记本电脑是surface 3,操作系统是windows10，今天windows10又来了一次更新，更新之后,带来的问题非常多，而且非常难以解决。当前国内几乎很少人遇到这个bug或者很少有人写解决方案(毕竟是surface 3的windows10操作系统的更新)，所以百度是绝对不行的。作为一个计算机出身的我，很不爽，于是开始了google的漫漫的解决问题之旅。（因为surface没有bios，是没办法像一般电脑那样可以重装系统的，其次它是在香港买的，出了问题很麻烦的。又没办法回退到更新之前的状态，结果就是我一定得靠自己解决这个问题，心烦，微软的系统就是坑爹，我最喜欢Unix系的了。）


更新之后遇到的问题主要有以下几个（包含但不仅限）：

1.计算机界面变成全英的。

2.很多application都没法启动，比如cmd和powershell，包括一些绿色版软件。都是提示The application was unable to start correctly (0xc0000142).Click OK to close the application.

3.另外就是按键组合和之前不同了，比如截图的命令，像prtscn,现在无法使用

solution:

1. 对于界面变成全英文这个问题，其实我并不担忧，本人对自己的英文水平还是很自信的。通过在cmd中输入指令chcp,可以得到代码页936,这证明了当前操作系统的机器内码没有发生改变，还是GBK。如果想把界面设置回中文，还是很方便的。需要注意到，若要使用 Cortana，你的“区域和语言”设置必须相互匹配。如果区域在中国，但是语言是英语，Cortana助手是会被停用的。

2. 对于第二个问题，谷歌了很多网址。发现欧美很多人也遇到过，但是他们提到的很多方案都不行。这其中包括了:
>[用兼容模式打开软件](http://answers.microsoft.com/en-us/windows/forum/windows_7-windows_programs/the-application-was-unable-to-start/90a33b48-d0e3-458b-9095-921057e8e8a7)。很可惜的是并不是这个问题。

>[Clean boot troubleshooting或者SFC scan](http://answers.microsoft.com/en-us/windows/forum/windows_10-files/cmdexe-application-error-windows-10-0xc0000142/37c7026a-2e10-4ad9-9175-2ea5c9479a0d)。很可惜，surface并不能够Clean boot。另外Administrator command prompt和powershell都是无法启动的，无法SFC scan.

>[查看event log](http://answers.microsoft.com/en-us/windows/forum/all/cmdexe-error-0xc0000142/21efc574-3279-441b-b3fd-005e46914564?auth=1)。event log很难看，而且这个没有具体的解决方法。

>[deshack与网友的问答，更改修改注册表](http://deshack.net/windows-how-to-solve-application-error-0xc0000142-and-0xc0000005/#comment-67480)这个黑客很牛逼，不过很可惜他的方法并不适合，因为下载的autotuns这个软件也是出现了142错误，至于Autoruns这个软件的AppInit tab打开是空的。也不行，至于修改注册表的，很多地方需要修改根本就没法一个一个找。根据后来的测试，发现需要修复的注册表位置多达上千个。

>但是，还是最终在同一个网站上 [deshack与网友的问答](http://deshack.net/windows-how-to-solve-application-error-0xc0000142-and-0xc0000005/#comment-67480)找到了答案。真是柳暗花明又一村。其中deshack让网友去尝试tj的评论里面提到的方法，于是找到tj的回复，很简单just download advanced system care and let defrag you system solved it for me :-)。接下来就是动手尝试了，没想到这个问题就这么解决了。感谢谷歌,特别是deshack和tj。

以下是我的解决第二个问题的过程：

一开始的状态是软件的各种无法启动。

![cmd启动失败](http://7xt54p.com2.z0.glb.clouddn.com/image/windows10/cmdfailed.png)

![powershell启动失败](http://7xt54p.com2.z0.glb.clouddn.com/image/windows10/powershellfailed.png)

![schtask启动失败](http://7xt54p.com2.z0.glb.clouddn.com/image/windows10/schtasksfailed.png)

之后下载安装Advanced Systemcare,需注意到官网上去下载，避免携带病毒，另外应该注意到中文版本会携带很多的软件包或主页设置，应该在安装的时候勾选掉。

然后使用ASC对注册表进行修复
![ASC对注册表进行修复](http://7xt54p.com2.z0.glb.clouddn.com/image/windows10/ASC.jpg)


完成之后重启电脑，发现大功告成了。
![大功告成](http://7xt54p.com2.z0.glb.clouddn.com/image/windows10/cmd-success.PNG)

## 但是从此windows操作系统在我心里更加不好了。


3. 第三个问题无解，prtScn不能使用。只能用Snipping tool，坑爹啊啊啊啊啊啊