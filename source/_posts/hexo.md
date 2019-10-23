---      
#    <center>搭建hexo博客</center>

##    环境准备

- git
- node.js


##    github

1.注册github帐号

注册好后，创建一个新仓库并改名为“用户名.github.io”的形式

![](https://i.loli.net/2019/10/21/km5lzGYxr17I2Pi.png)

2.设置ssh密钥

windows打开powershell, 输入：
```
ssh-keygen -t rsa -C "github"

   -t 指定密钥类型 默认rsa   
   
   -C 设置注释文字
```
接着按三下回车即可完成（第一次是设置文件名，后面两次是设置push时候的密码，直接回车是使用默认设置）。

完成后会提示你id_rsa的地址，找到打开文件并复制其中内容。在github中setting找到ssh的设置，创建新的ssh key然后将复制的内容粘贴上去，完成创建。

![](https://i.loli.net/2019/10/23/8f9MTqylovjd5a4.png)

测试创建是否成功，在powershell或者terminal中输入:
```
ssh -T git@github.com
```
##    hexo

新建一个文件夹存储管理博客文件，进入文件夹右键运行git bush,输入

```
npm install -g hexo-cli

hexo init blog
```
hexo常用命令:

```
hexo n "name"     新建名为name的文章

hexo g 生成

hexo s 本地服务预览，运行后可在浏览器输入localhost:4000预览

hexo d 部署
```
部署至github还需要修改主目录中的_config.yml，末尾添加一段(注意冒号后面要加空格):
```
deploy:

type: git

repo: https://github.com/gjq1998/gjq1998.github.io.git

branch: master
```
完成后在浏览器输入地址username,github.io即可查看自己博客。



 2019-10-2 23:46:00

---          
