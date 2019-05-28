** 安装下载和上传命令 **
1. yum安装
yum install -y lrzsz

** Yum: Cannot find a valid baseurl for repo **
You can try uncommenting the baseurl in /etc/yum.repos.d/CentOS-Base.repo
From:[nethserver](https://community.nethserver.org/t/yum-cannot-find-a-valid-baseurl-for-repo/8984/3)
CentOS-Base.repo是基本yum源文件（也是网络yum源）
（新机器）Yum安装的时候报错，内网环境，通过修改CentOS-Base.repo（拷贝已有机器上的文件内容）,成功解决问题

将文件系统与目录树相结合的操作成为挂载
挂载点一定是目录，该目录为进入该文件系统的入口
操作系统中负责管理和存储文件信息的软件机构称为文件管理系统，简称文件系统
du:评估文件系统的磁盘使用量（常用于评估目录使用量）
df:列出文件系统的整体磁盘使用量

tmpfs,临时文件系统，是一种基于内存的文件系统，它和虚拟磁盘ramdisk比较类似像，但不完全相同，和ramdisk一样，tmpfs可以使用RAM，但它也可以使用swap分区来存储，而且传统的ramdisk是个块设备，要用mkfs来格式化它，才能真正地使用它；而tmpfs是一个文件系统，并不是块设备，只是安装它，就可以使用了。tmpfs是最好的基于RAM的文件系统

IDE的英文全称为“Integrated Drive Electronics”，即“电子集成驱动器”
SATA是Serial ATA的缩写，即串行ATA

主分区中不能再划分其他类型的分区，因此每个主分区都相当于一个逻辑磁盘（在这一点上主分区和逻辑分区很相似，但主分区是直接在硬盘上划分的，逻辑分区则必须建立于扩展分区中）

扩展分区也就是除主分区外的分区，但它不能直接使用，必须再将它划分为若干个逻辑分区才行。
逻辑分区也就是我们平常在操作系统中所看到的D、E、F等盘。



[apk 包管理命令](https://www.hi-linux.com/posts/64839.html)
  update:从远程镜像源中更新本地镜像源索引
  add:安装PACKAGES并自动解决依赖关系
  del:卸载并删除PACKAGES
  upgrade:升级当前已安装的软件包
  search:搜索软件包
  info:列出PACKAGES或镜像源的详细信息


  awk命令
  awk '{pattern + action}' {filenames}

秘钥

```
ssh-keygen
```

linux 解压命令小结

```
unzip filename. zip.
tar -zxvf filename. tar.gz.
tar -Jxvf filename. tar.xz.
tar -Zxvf filename. tar.Z.
tar --help.
tar -xvf filename. tar.gz tar -xvf filename.
```

日志查看命令

```
cat log.log -n #显示行号，包括空白行
sed -n "840,900p" error.log #查看840-900行的内容
```

