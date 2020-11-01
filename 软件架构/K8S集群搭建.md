[docker部署k8s](https://blog.csdn.net/ysk_xh_521/article/details/81668631)

**环境信息**

```
Linux VM_0_10_centos 3.10.0-862.el7.x86_64 #1 SMP Fri Apr 20 16:44:24 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

```



# 1. docker安装

1. **安装device-mapper**

   ```bash
   #查看是否安装device-mapper
   ls -l /sys/class/misc/device-mapper
   #安装device-mapper
   sudo yum install -y device-mapper
   #加载dm_mod内核模块
   sudo modprobe dm_ mod
   
   ```

2.  **安装docker**

   ```bash
   #安装docker
   sudo yum -y install docker-io
   #启动docker
   sudo systemctl start docker
   #开机时启动docker
   sudo systemctl enable docker
   ```

   

3.  **docker配置国内加速镜像**

   [docker仓库和镜像](https://www.cnblogs.com/wushuaishuai/p/9984228.html)

   ```
    vim /etc/docker/daemon.json
    {
     "registry-mirrors": ["<your accelerate address>"]
   }
   sudo systemctl daemon-reload 
   sudo systemctl restart docker
   
   ```

   

4.  

5. 



# 2. K8S集群安装

1. **安装etcd**

   ```bash
   yum install etcd -y
   systemctl start etcd
   systemctl enable etcd
   etcdctl -C http://localhost:2379 cluster-health
   ```

   

2.  **安装K8S**

   ```bash
   yum install kubernetes -y
   vim /etc/kubernetes/apiserver 
   systemctl start kube-apiserver.service 
   systemctl enable kube-apiserver.service 
   systemctl start kube-controller-manager
   systemctl enable kube-controller-manager
   systemctl start kube-scheduler.service 
   systemctl enable kube-scheduler
   systemctl start kubelet
   systemctl enable kubelet
   systemctl start kube-proxy
   systemctl enable kube-proxy
   kubectl get nodes
   ```

   

3.  **创建覆盖网络flannel**

   ```bash
   yum install flannel
   vim /etc/sysconfig/flanneld
   etcdctl mk /atomic.io/network/config '{ "Network": "10.0.0.0/16" }'
   systemctl enable flanneld  
   systemctl start flanneld
   service docker restart
   systemctl restart kube-apiserver
   systemctl restart kube-controller-manager
   systemctl restart kube-scheduler
   systemctl restart kubelet
   systemctl restart kube-proxy
   ```

   

4.  

5. 

https://blog.csdn.net/wucong60/article/details/81458409