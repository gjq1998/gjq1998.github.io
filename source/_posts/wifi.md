---  
##manjaro系统wifi无法使用问题

装好manjaro-kde系统以后，发现wifi选项无法勾选上。这是联想拯救者笔记本会出现的问题，不确定其他笔记本情况。

首先终端输入`rfkill list all`,结果如下
![](https://i.loli.net/2019/09/19/r2Hxl17EZKuNjoa.png)

会发现无线模块被 hard blocked了。解决方法如下： 

终端输入

`sudo vim /etc/modprobe.d/blacklist.conf`

在建立的文件中输入

`blacklist ideapad_laptop`


保存后重启即可。

重启后再次输入`rfkill list all` 会变成
![](https://i.loli.net/2019/09/19/ydJHn57heXoUQlB.png)

此时就会发现wifi能用了



2019-09-19 08:30:36

---  
