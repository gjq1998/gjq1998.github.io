---     
#    <center>分支管理博客</center>
双系统电脑在更换系统后无法更新博客，为解决这个问题可在github仓库新建一个分支来储存hexo的源文件，这样在切换电脑或者系统后能下载hexo的源文件方便的进行管理和更新。

##    在创建博客的电脑上

在github新建branch，取名为hexo，并设置为默认分支,此时的hexo和master分支的内容是一样的。

在本地输入命令下载仓库：
```
git clone git@github.com:username/username.github.io username为用户名
```
打开下载的仓库文件夹，将除了.git以外的内容删除掉，然后将之前建好的博客文件夹中的内容复制到这个目录。并执行命令：
```
git add .   将新创建或修改的文件提交暂存区

git commit -m "new"   添加描述信息

git push origin hexo  上传至远程仓库
```
此时在github上看hexo分支，内容已经变成博客的源文件。

##    新电脑上

安装好git和node.js后。

```
git clone git@github.com:username/username.github.io 下载仓库
```
在仓库文件夹中

```
npm install hexo
```
这样就创建了和原来电脑一模一样的博客源文件夹，和原来一样：
```
hexo g

hexo d

部署博客的静态网页
```
```
git add .

git commit -m "xxx"

git push origin hexo

上传博客源文件
```
##    附：retext

在linux manjaro下用retext写博客，发现无法实时预览外部图床的图片。需要修改/home/ueser/.config/ReText project/ReText.conf的配置文件。添加：
```
useWebKit=true
```
其他配置选项可参考[官网](https://github.com/retext-project/retext/blob/master/configuration.md)


 2019-10-8 21:17:02

---      
