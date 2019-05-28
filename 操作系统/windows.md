[Windows中杀死占用某个端口的进程](https://blog.csdn.net/wangjunjun2008/article/details/9407219)
netstat -ano | findstr 端口号
tasklist | findstr 进程号
taskkill -PID <进程号> -F //强制关闭某个进程

etstat –ano|findstr “<端口号>

tasklist|findstr “<PID号>”