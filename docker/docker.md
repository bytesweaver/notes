#显示所有的容器，过滤出Exited状态的容器，取出这些容器的ID，

sudo docker ps -a|grep Exited|awk '{print $1}'

#查询所有的容器，过滤出Exited状态的容器，列出容器ID，删除这些容器

```shell
sudo docker rm `docker ps -a|grep Exited|awk '{print $1}'`
```

