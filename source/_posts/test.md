---
# Windows和Manjaro(kde) 双系统安装

作为电脑小白，想要学习使用linux系统，但是又不想舍弃使用多年的windows，于是折腾着安装双系统。
<img src="https://i.loli.net/2019/09/17/IPOb657jgvDerHk.png" width = "100%" height = "50%"  div align=center >

## 一、U盘写入镜像 
首先从[manjaro官网][1]上下载相应的镜像，然后写入u盘,我使用的是Rufus3.5,分区类型选择GPT，配置好后点击开始选择以dd模式写入镜像。
![image.png](https://i.loli.net/2019/09/18/zB6AXCRLbmYcQOp.png)
[1]:https://manjaro.org/
## 二、磁盘分区
在windows中打开磁盘管理器，为即将安装的manjaro系统分配空间，右键点击磁盘选择压缩卷，大小根据自己的需要而定，我选择的是150G，压缩成功后会有150G的未分配空间。
![image.png](https://i.loli.net/2019/09/18/I2EbhoqySl3a8N6.png)

## 三、开始安装
重启电脑，按F2进入BIOS界面（不同笔记本可能按键不同），security boot选项关闭，BOOT MODE中把UEFI启动改成LEGACY SURPPORT,保存重启进入U盘安装界面。
![image.png](https://i.loli.net/2019/09/18/gu4GjNAFQ7qcfJp.png)
时间和语言可改可不改，后面安装完还能设置，选择BOOT进入安装界面。带N卡的双显卡笔记本进入安装后，可能会卡在黑屏界面，只有白色光标闪烁，无法进入后面的图形安装界面。我的联想笔记本就遇到这样的问题。此时需要在U盘安装界面的BOOT选项按E进入编辑界面将nouveau.modeset=1改成0。

## 四、设置挂载点
顺利进入图形安装界面后，根据引导按下一步即可。直到设置分区步骤，选择手动分区。对第二步压缩出来的那块未分配空间进行分区并设置挂载点。
### /
根分区，分配20~30G
### /boot/efi
由于是双系统，需要将引导文件放在和windows同一个地方。也就是那个260MB的独立盘上，不同电脑大小可能不一样，挂载点选择/boot/efi，保留格式。
### swap
虚拟内存，内存够大可不分配
### home 
剩下全部空间

分配好后，跟着引导即可完成安装。








<div align=right>date: 2019-09-10 14:59:58 
--- 
