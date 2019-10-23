---        
#    <center>metasploitable 3靶机安装</center>

安装metasploitable 3作渗透测试使用，但[github][1]上没有镜像文件，只有安装方法，接下来详细说明如何制作VMWARE适用的靶机镜像。主机系统是linux manjaro。
[1]:https://github.com/rapid7/metasploitable3

##    安装需要的软件
- packer

- vagrant和vagrant Reload Plugin

- vmware

##    packer制作镜像

打开终端，cd到要想要安装的目录，执行命令
```
git clone --depth=1 https://github.com/rapid7/metasploitable3

cd ./metasploitable3

paker build --only=vmware-iso ./paker/temlates/windows_2008_r2.json
```
然后packer就开始制作镜像文件，制作过程比较慢，耐心等待。

##    packer 打包报错
安装过程中遭遇两个问题

1.glassfish下载失败

![](https://i.loli.net/2019/10/20/79jBEnWN6PkJoMy.png)

解决方法：
将安装失败的镜像在vmware中删除后，在/metasploitable3/scripts/installs中找到并编辑setup_glassfish.bat。

修改:
```
powershell -Command "(New-Object System.Net.WebClient).DownloadFile('http://download.java.net/glassfish/4.0/release/glassfish-4.0.zip', 'C:\Windows\Temp\glassfish4.zip')" <NUL
```
为:
```
powershell -Command "[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; (New-Object System.Net.WebClient).DownloadFile('http://download.java.net/glassfish/4.0/release/glassfish-4.0.zip', 'C:\Windows\Temp\glassfish4.zip')" <NUL
```
2./tmp空间不足

解决方法:

修改/etc/fstab

在末尾添加一行
```
tmpfs /tmp tmpfs rw,nodev,nosuid, size=15G 0 0
```
reboot以后使用df -h 查看，可以发现/tmp已经变为15G.

##    vagrant 配置box文件

前面安装过程顺利的话会在/packer/builds下生成一个.box文件，vmware无法打开，需要vagrant进行配置。

```
vagrant box add /metasploitable3/packer/builds/windows_2008_r2_*_0.1.0.box --name=metasploitable3
```
完成后会生成在.vagrant.d/boxes目录下，用vmware打开即可。


 




2019-10-4 23:46:00

---     
