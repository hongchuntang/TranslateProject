Ubuntu每日贴士-Ubuntu One系统关闭，如何切换到Dropbox或者Box云服务
Canonical公司决定关闭Ubuntu One的云服务，你可能正在寻找备份你主机的其他服务器，尽管现在有很多云服务的提供商，但是仅有小部分支持linux,包括Ubuntu。
Dropbox全面支持Ubuntu，它有一个很好的整合了ubuntu桌面系统和其他通知栏的客户端。Box，官方的Box.net也可以通过WebDav协议支持linux。
这里有一段来自Canonical公司关于Ubuntu One的摘录：
As of today (April 2), it will no longer be possible to purchase storage or music from the Ubuntu One store. The Ubuntu One file services will not be included in the upcoming Ubuntu 14.04 LTS release, and the Ubuntu One apps in older version of Ubuntu and in the Ubuntu, Google and Apple stores will be updated appropriately.
也就是说我们在ubuntu中失去了这项有用的服务。另一方面，把你的数据移动到一个更稳定、更好信誉的网盘提供商是一个比较好的选择。
这里简要的说明一下怎样在ubuntu中运行DropBox或者Box云服务。

在ubuntu中安装DropBox云盘
关于这个话题我们已经写了很多，为了在ubuntu中安装DropBox云盘，你需要按照以下步骤去做，这里提供了一个在ubuntu中一步步安装和使用DropBox的步骤。
查看完整步骤，点这里，或者下面的链接：
http://www.liberiangeek.net/2013/03/how-to-install-dropbox-in-ubuntu-13-04-raring-ringtail/

在Ubuntu中使用Box网盘
自从Box不再提供给linux一个全功能的客户端，包括ubuntu，你必须使用WebDav协议来访问和存储你账户的东西。
按Ctrl – Alt – T来打开终端，终端被打开后，执行下面的命令来安装包：
sudo apt-get install davfs2
接下来，执行下面的命令来配置davfs2，选择Yes来允许没有权限的用户来挂载WebDav资源。
sudo dpkg-reconfigure davfs2
接下来通过执行下面的命令把davfs2目录复制到你的home目录：
sudo cp -r /etc/davfs2/ $HOME/.davfs2
然后执行下面命令获取文件夹的所有权：
sudo chown -R username $HOME/.davfs2/
用你的用户名代替username 
接下来打开密码文件输入你的登录凭证：
gedit ~/.davfs2/secrets
然后键入你的用户名（email地址）和密码，在文件末尾添加下面的行并保存。
https://dav.box.com/dav richard@liberiangeek.net  <box_password>
用你的账户信息替换上面的email地址和password。
接下来用下面的命令添加你的账户到davfs2组中：
sudo adduser <username> davfs2
然后用sudo gedit /etc/fstab 打开/etc/fstab在后面添加下面一行并保存：
https://dav.box.com/dav/ /home/<username>/box  davfs _netdev,rw,user 0 0 
最后创建一个挂载点并挂载Box
mkdir ~/box
重启你的电脑，Box能开机自动挂载了，
享受下吧！