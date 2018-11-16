** 安装下载和上传命令 **
1. yum安装
yum install -y lrzsz

** Yum: Cannot find a valid baseurl for repo **
You can try uncommenting the baseurl in /etc/yum.repos.d/CentOS-Base.repo
From:[nethserver](https://community.nethserver.org/t/yum-cannot-find-a-valid-baseurl-for-repo/8984/3)
CentOS-Base.repo是基本yum源文件（也是网络yum源）
（新机器）Yum安装的时候报错，内网环境，通过修改CentOS-Base.repo（拷贝已有机器上的文件内容）,成功解决问题
