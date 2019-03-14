# docker使用
[doker命令](https://yeasy.gitbooks.io/docker_practice/image/dockerfile/copy.html)
FROM: 指定基础镜像
RUN： 执行命令
```
#shell格式
RUN 命令
#exec格式
RUN ["可执行文件","参数1","参数2"]
```
Dockerfile 支持 Shell 类的行尾添加 \ 的命令换行方式，以及行首 # 进行注释的格式
镜像构建上下文（Context）
Docker 在运行时分为 Docker 引擎（也就是服务端守护进程）和客户端工具
默认情况下，如果不额外指定 Dockerfile 的话，会将上下文目录下的名为 Dockerfile 的文件作为 Dockerfile
COPY：
ADD：
所有的文件复制均使用 COPY 指令，仅在需要自动解压缩的场合使用 ADD
--chown=<user>:<group> 选项来改变文件的所属用户及所属组
CMD：CMD 指令就是用于指定默认的容器主进程的启动命令的，格式同RUN指令
  例：CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT：入口点，格式同RUN，CMD 的含义发生了改变，不再是直接的运行其命令，而是将 CMD 的内容作为参数传给 ENTRYPOINT 指令
ENV：设置环境变量
```
#格式一
ENV <key><value>
#格式二
ENV <key1>=<value1> <key2>=<value2>...
```

docker ps -a 命令 查看 当前 系统 中 容器 的 列表
docker start [容器名/容器ID] #重启已经关闭的容器
docker attach [容器名/容器ID] #附着到容器
docker logs -f -t #获取容器日志 -f 同tail -f, -t 加上时间戳
docker top #查看容器内进程
docker exec #容器内额外启动新进程
docker run -d --restart=always --name #后台，是否重启，容器名字
sudo docker inspect #查看容器状态
---
卷是在一个或多个容器中特殊指定的目录，卷会绕过联合文件系统，为持久化数据和共享数据提供几个有用的特性  
docker run --volumes-from#把指定容器的卷加入新创建的容器中
删除最后一个使用卷的容器，卷将被删除
sudo docker port [容器] 端口号 #查看端口映射
