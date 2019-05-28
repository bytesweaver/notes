#显示所有的容器，过滤出Exited状态的容器，取出这些容器的ID，

sudo docker ps -a|grep Exited|awk '{print $1}'

#查询所有的容器，过滤出Exited状态的容器，列出容器ID，删除这些容器

```shell
sudo docker rm `docker ps -a|grep Exited|awk '{print $1}'`
```

## Docker Compose

compose负责实现对docker容器集群的快速编排

**概念**

服务（service）：一个应用的容器，实际上可以包括若干运行相同镜像的容器实例

项目（project）：由一组关联的应用容器组成的一个完整业务单元，在 `docker-compose.yml` 文件中定义

## Dockerfile

```
VOLUME /data
docker run -d -v mydata:/data xxxx
```

重启Docker服务

sudo systemctl restart docker

```
sudo docker exec -it [containerID] cat /etc/hosts #执行命令
docker container cp [containID]:[/path/to/file] . #将docker中的文件拷贝到本地
docker container logs [containerID] #查看日志
docker logs --tail 100 [containerID]
docker run --rm #容器停止运行后，自动删除容器文件

```

