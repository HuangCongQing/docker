# 02Docker常用命令

## 1帮助命令
```shell
docker version # 显示docker版本信息
docker info   # 显示docker系统信息（包括镜像和容器的数量）
docker 命令 --help  # 万能命令
```
帮助文档地址：[https://docs.docker.com/reference/](https://docs.docker.com/reference/)<br />例如查看 **docker images  --help**<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1601973458704-0d5f21bc-3b25-49a3-ae36-baebd33e882b.png#align=left&display=inline&height=270&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=270&originWidth=797&size=42031&status=done&style=none&width=797)<br />
<br />docker --help（中文注解）<br />

```powershell
Usage:
docker [OPTIONS] COMMAND [arg...]
       docker daemon [ --help | ... ]
       docker [ --help | -v | --version ]
A
self-sufficient runtime for containers.
Options:
  --config=~/.docker              Location of client config files  #客户端配置文件的位置
  -D, --debug=false               Enable debug mode  #启用Debug调试模式
  -H, --host=[]                   Daemon socket(s) to connect to  #守护进程的套接字（Socket）连接
  -h, --help=false                Print usage  #打印使用
  -l, --log-level=info            Set the logging level  #设置日志级别
  --tls=false                     Use TLS; implied by--tlsverify  #
  --tlscacert=~/.docker/ca.pem    Trust certs signed only by this CA  #信任证书签名CA
  --tlscert=~/.docker/cert.pem    Path to TLS certificate file  #TLS证书文件路径
  --tlskey=~/.docker/key.pem      Path to TLS key file  #TLS密钥文件路径
  --tlsverify=false               Use TLS and verify the remote  #使用TLS验证远程
  -v, --version=false             Print version information and quit  #打印版本信息并退出
Commands:
    attach    Attach to a running container  #当前shell下attach连接指定运行镜像
    build     Build an image from a Dockerfile  #通过Dockerfile定制镜像
    commit    Create a new image from a container's changes  #提交当前容器为新的镜像
    cp    		Copy files/folders from a container to a HOSTDIR or to STDOUT  #从容器中拷贝指定文件或者目录到宿主机中
    create    Create a new container  #创建一个新的容器，同run 但不启动容器
    diff   	 Inspect changes on a container's filesystem  #查看docker容器变化
    events    Get real time events from the server#从docker服务获取容器实时事件
    exec  	  Run a command in a running container#在已存在的容器上运行命令
    export    Export a container's filesystem as a tar archive  #导出容器的内容流作为一个tar归档文件(对应import)
    history   Show the history of an image  #展示一个镜像形成历史
    images    List images  #列出系统当前镜像
    import    Import the contents from a tarball to create a filesystem image  #从tar包中的内容创建一个新的文件系统映像(对应export)
    info   		Display system-wide information  #显示系统相关信息
    inspect   Return low-level information on a container or image  #查看容器详细信息
    kill    	Kill a running container  #kill指定docker容器
    load   		Load an image from a tar archive or STDIN  #从一个tar包中加载一个镜像(对应save)
    login     Register or log in to a Docker registry#注册或者登陆一个docker源服务器
    logout    Log out from a Docker registry  #从当前Docker registry退出
    logs      Fetch the logs of a container  #输出当前容器日志信息
    pause     Pause all processes within a container#暂停容器
    port      List port mappings or a specific mapping for the CONTAINER  #查看映射端口对应的容器内部源端口
    ps        List containers  #列出容器列表
    pull      Pull an image or a repository from a registry  #从docker镜像源服务器拉取指定镜像或者库镜像
    push      Push an image or a repository to a registry  #推送指定镜像或者库镜像至docker源服务器
    rename    Rename a container  #重命名容器
    restart   Restart a running container  #重启运行的容器
    rm        Remove one or more containers  #移除一个或者多个容器
    rmi  		  Remove one or more images  #移除一个或多个镜像(无容器使用该镜像才可以删除，否则需要删除相关容器才可以继续或者-f强制删除)
    run  		  Run a command in a new container  #创建一个新的容器并运行一个命令
    save  	  Save an image(s) to a tar archive#保存一个镜像为一个tar包(对应load)
    search    Search the Docker Hub for images  #在dockerhub中搜索镜像
    start    Start one or more stopped containers#启动容器
    stats    Display a live stream of container(s) resource usage statistics  #统计容器使用资源
    stop    Stop a running container  #停止容器
    tag         Tag an image into a repository  #给源中镜像打标签
    top       Display the running processes of a container #查看容器中运行的进程信息
    unpause    Unpause all processes within a container  #取消暂停容器
    version    Show the Docker version information#查看容器版本号
    wait         Block until a container stops, then print its exit code  #截取容器停止时的退出状态值

Run 'docker COMMAND --help' for more information on a command.  #运行docker命令在帮助可以获取更多信息
docker search  hello-docker  # 搜索hello-docker的镜像
docker search centos # 搜索centos镜像
docker pull hello-docker # 获取centos镜像
docker run  hello-world   #运行一个docker镜像，产生一个容器实例（也可以通过镜像id前三位运行）
docker image ls  # 查看本地所有镜像
docker images  # 查看docker镜像
docker image rmi hello-docker # 删除centos镜像
docker ps  #列出正在运行的容器（如果创建容器中没有进程正在运行，容器就会立即停止）
docker ps -a  # 列出所有运行过的容器记录
docker save centos > /opt/centos.tar.gz  # 导出docker镜像至本地
docker load < /opt/centos.tar.gz   #导入本地镜像到docker镜像库
docker stop  `docker ps -aq`  # 停止所有正在运行的容器
docker  rm `docker ps -aq`    # 一次性删除所有容器记录
docker rmi  `docker images -aq`   # 一次性删除所有本地的镜像记录
```

<br />
<br />

<a name="GdTNR"></a>
## 2 镜像命令  images serach pull rmi

**docker images  # 查看所有主机上的镜像**

![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592066626773-66d7e8dc-04c0-4724-828f-272c919b7dfc.png#align=left&display=inline&height=98&margin=%5Bobject%20Object%5D&name=image.png&originHeight=139&originWidth=1021&size=166059&status=done&style=none&width=718)

```shell
docker images  # 查看所有主机上的镜像

# 可选项
-a # 列出所有镜像
-q # 只显示镜像的id
```
**docker search # 搜索镜像（等同于在hub上搜索）**<br />

```shell
docker search mysql --filte=STARS=3000 # filter 过于stars大于3000
```
**docker pull  镜像名:tag    # 如果不写tag。默认latest**
```shell
docker pull  mysql:5.7    # 下载镜像
```

<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592066410124-88c6cd40-d75d-42cc-b5ac-e9dead0e9ea5.png#align=left&display=inline&height=351&margin=%5Bobject%20Object%5D&name=image.png&originHeight=701&originWidth=1008&size=489312&status=done&style=none&width=504)<br />
<br />**docker rmi 删除镜像**<br />

```shell
docker rmi -f 容器id  # 删除指定镜像
docker rmi -f $(docker images -aq)  # 删除全部镜像
```
![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1601982310786-7565e994-b567-47d6-b544-58f7fb403378.png#align=left&display=inline&height=106&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=106&originWidth=483&size=30078&status=done&style=none&width=483)
<a name="kzqER"></a>
## 3 容器命令
说明：**有了镜像才可以创建容器**
```shell
docker pull centos
```
<a name="RKtaL"></a>
#### 新建容器并启动 docker run 
每一次run就是新创建一个容器

docker run [可选参数]  镜像名
```shell
# 启动并进入容器
docker run -it centos /bin/bash  # 启动并进入容器
```


```shell
docker run [可选参数] image

# 参数说明 常用itd
--name="Name"  容器名字	 tomcat01 tomcat02 用来区分容器
-d  # 后台方式运行
-it 使用交互方式进行，进入容器查看内容。
-P 指定容器端口  8080
	
-p 随机指定端口
# 启动并进入容器
docker run -it centos /bin/bash  # 启动并进入容器
# 退出容器   
exit 回车
```

<br />
<br />

<a name="itA0s"></a>
#### 列出所有运行的容器 docker ps
docker ps
```shell
docker ps 

-a  列出当前正在运行的容器 + 历史运行过的容器
-n=数字  # 显示最近创建的容器
-q 只显示容器的编号。

Options:
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -l, --latest          Show the latest created container (includes all states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display numeric IDs
  -s, --size            Display total file sizes

```
<a name="XcVGS"></a>
#### 退出容器 exit
```shell
exit # 直接容器停止并退出
ctrl + P + Q  # 不停止，退出
```


<a name="iVPI8"></a>
#### 启动和停止容器操作 start  stop


```shell
docker start  容器id    # 启动容器
docker restart  容器id  # 重启容器
docker  stop  容器id    # 停止当前正在运行的容器
docker  kill  容器id    # 	强制停止当前容器
```
<a name="trs5d"></a>
#### 进入当前正在运行的容器 attach exec
启动容器： docker start id名字
```shell
# 进入一些容器修改一些配置

# 命令1
docker exec -it 容器id /bin/bash
# 命令2也可
docker attach 容器id  # 进入正在运行的命令行

# 比较
docker exec # 进入容器后开启一个新的终端
docker attach # 进入容器正在执行的终端   
```

<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592110115609-63dba84b-7db1-41a8-ba17-6f9defd437aa.png#align=left&display=inline&height=203&margin=%5Bobject%20Object%5D&name=image.png&originHeight=405&originWidth=1327&size=336526&status=done&style=none&width=663.5)
<a name="xP0nP"></a>
#### 删除容器 rm


```shell
docker rm 容器id   # 删除指定容器，不能删除正在运行的容器，如果要强制删除 rm -f
docker rm -f $(docker ps -aq)  # 删除所有
```

<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1601976787070-db5fd251-bd5d-43d3-a900-cb8f86c60d45.png#align=left&display=inline&height=317&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=317&originWidth=1437&size=80919&status=done&style=none&width=1437)<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592068378379-25a455b3-95b3-46b3-8ad9-28fe38e70a4e.png#align=left&display=inline&height=169&margin=%5Bobject%20Object%5D&name=image.png&originHeight=337&originWidth=1246&size=291708&status=done&style=none&width=623)<br />
<br />

<a name="GYMxX"></a>
## 4 常用其他命令
[P1111、日志、元数据、进程的查看](https://www.bilibili.com/video/BV1og4y1q7M4?p=11)<br />

<a name="JNE7C"></a>
#### 后台启动容器 -d
```shell
# 命令 docker run -d 镜像名

# 问题docker ps，发现centos停止了

# 常见的坑：docker容器使用后台运行，必须要有一个前台进程。如果没有应用，就会自动停止。
```

<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592104811335-9cfdcaad-fa45-4b5b-bfed-1b49e1c8a6d5.png#align=left&display=inline&height=184&margin=%5Bobject%20Object%5D&name=image.png&originHeight=369&originWidth=1386&size=255791&status=done&style=none&width=693)
<a name="FRStX"></a>
#### 查看日志 docker logs -ft --tails 10


```shell
docker logs -ft --tails 10
```
![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592109539507-a6469a46-f7b2-4106-9b14-85485e6e8a6f.png#align=left&display=inline&height=189&margin=%5Bobject%20Object%5D&name=image.png&originHeight=377&originWidth=1079&size=189727&status=done&style=none&width=539.5)<br />

<a name="eIavF"></a>
#### 查看容器中进程信息 top
docker top 容器id<br />pid 当前进程id<br />ppid 父进程id<br />
<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592109546733-28401f8a-7e57-4880-9f52-49206a09032c.png#align=left&display=inline&height=84&margin=%5Bobject%20Object%5D&name=image.png&originHeight=168&originWidth=1112&size=85551&status=done&style=none&width=556)<br />

<a name="HoL4K"></a>
#### 查看镜像的元数据 inspect
docker inspect 容器信息<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592109857428-d9f6ceb2-2af9-4140-b646-dd1b0a4d6f7e.png#align=left&display=inline&height=164&margin=%5Bobject%20Object%5D&name=image.png&originHeight=327&originWidth=963&size=176459&status=done&style=none&width=481.5)<br />

<a name="n9MdW"></a>
#### 


<a name="COg10"></a>
#### 从容器内拷贝文件到主机 cp


```shell
docker cp  容器id:xxx  xxx
```
拷贝是一个手动过程，后面我们使用-v卷的技术，可以实现自动同步<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592110643150-df71697e-c3c3-4a48-8525-10bfb64362af.png#align=left&display=inline&height=233&margin=%5Bobject%20Object%5D&name=image.png&originHeight=466&originWidth=1261&size=339248&status=done&style=none&width=630.5)<br />
<br />

<a name="UIpxM"></a>
## 5 命令小结(附图片)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592110858160-9a33f734-dc95-48d3-a0f4-b1237337296b.png#align=left&display=inline&height=536&margin=%5Bobject%20Object%5D&name=image.png&originHeight=748&originWidth=1042&size=465433&status=done&style=none&width=746)



```powershell
Usage:
docker [OPTIONS] COMMAND [arg...]
       docker daemon [ --help | ... ]
       docker [ --help | -v | --version ]
A
self-sufficient runtime for containers.
Options:
  --config=~/.docker              Location of client config files  #客户端配置文件的位置
  -D, --debug=false               Enable debug mode  #启用Debug调试模式
  -H, --host=[]                   Daemon socket(s) to connect to  #守护进程的套接字（Socket）连接
  -h, --help=false                Print usage  #打印使用
  -l, --log-level=info            Set the logging level  #设置日志级别
  --tls=false                     Use TLS; implied by--tlsverify  #
  --tlscacert=~/.docker/ca.pem    Trust certs signed only by this CA  #信任证书签名CA
  --tlscert=~/.docker/cert.pem    Path to TLS certificate file  #TLS证书文件路径
  --tlskey=~/.docker/key.pem      Path to TLS key file  #TLS密钥文件路径
  --tlsverify=false               Use TLS and verify the remote  #使用TLS验证远程
  -v, --version=false             Print version information and quit  #打印版本信息并退出
Commands:
    attach    Attach to a running container  #当前shell下attach连接指定运行镜像
    build     Build an image from a Dockerfile  #通过Dockerfile定制镜像
    commit    Create a new image from a container's changes  #提交当前容器为新的镜像
    cp    		Copy files/folders from a container to a HOSTDIR or to STDOUT  #从容器中拷贝指定文件或者目录到宿主机中
    create    Create a new container  #创建一个新的容器，同run 但不启动容器
    diff   	 Inspect changes on a container's filesystem  #查看docker容器变化
    events    Get real time events from the server#从docker服务获取容器实时事件
    exec  	  Run a command in a running container#在已存在的容器上运行命令
    export    Export a container's filesystem as a tar archive  #导出容器的内容流作为一个tar归档文件(对应import)
    history   Show the history of an image  #展示一个镜像形成历史
    images    List images  #列出系统当前镜像
    import    Import the contents from a tarball to create a filesystem image  #从tar包中的内容创建一个新的文件系统映像(对应export)
    info   		Display system-wide information  #显示系统相关信息
    inspect   Return low-level information on a container or image  #查看容器详细信息
    kill    	Kill a running container  #kill指定docker容器
    load   		Load an image from a tar archive or STDIN  #从一个tar包中加载一个镜像(对应save)
    login     Register or log in to a Docker registry#注册或者登陆一个docker源服务器
    logout    Log out from a Docker registry  #从当前Docker registry退出
    logs      Fetch the logs of a container  #输出当前容器日志信息
    pause     Pause all processes within a container#暂停容器
    port      List port mappings or a specific mapping for the CONTAINER  #查看映射端口对应的容器内部源端口
    ps        List containers  #列出容器列表
    pull      Pull an image or a repository from a registry  #从docker镜像源服务器拉取指定镜像或者库镜像
    push      Push an image or a repository to a registry  #推送指定镜像或者库镜像至docker源服务器
    rename    Rename a container  #重命名容器
    restart   Restart a running container  #重启运行的容器
    rm        Remove one or more containers  #移除一个或者多个容器
    rmi  		  Remove one or more images  #移除一个或多个镜像(无容器使用该镜像才可以删除，否则需要删除相关容器才可以继续或者-f强制删除)
    run  		  Run a command in a new container  #创建一个新的容器并运行一个命令
    save  	  Save an image(s) to a tar archive#保存一个镜像为一个tar包(对应load)
    search    Search the Docker Hub for images  #在dockerhub中搜索镜像
    start    Start one or more stopped containers#启动容器
    stats    Display a live stream of container(s) resource usage statistics  #统计容器使用资源
    stop    Stop a running container  #停止容器
    tag         Tag an image into a repository  #给源中镜像打标签
    top       Display the running processes of a container #查看容器中运行的进程信息
    unpause    Unpause all processes within a container  #取消暂停容器
    version    Show the Docker version information#查看容器版本号
    wait         Block until a container stops, then print its exit code  #截取容器停止时的退出状态值

Run 'docker COMMAND --help' for more information on a command.  #运行docker命令在帮助可以获取更多信息
docker search  hello-docker  # 搜索hello-docker的镜像
docker search centos # 搜索centos镜像
docker pull hello-docker # 获取centos镜像
docker run  hello-world   #运行一个docker镜像，产生一个容器实例（也可以通过镜像id前三位运行）
docker image ls  # 查看本地所有镜像
docker images  # 查看docker镜像
docker image rmi hello-docker # 删除centos镜像
docker ps  #列出正在运行的容器（如果创建容器中没有进程正在运行，容器就会立即停止）
docker ps -a  # 列出所有运行过的容器记录
docker save centos > /opt/centos.tar.gz  # 导出docker镜像至本地
docker load < /opt/centos.tar.gz   #导入本地镜像到docker镜像库
docker stop  `docker ps -aq`  # 停止所有正在运行的容器
docker  rm `docker ps -aq`    # 一次性删除所有容器记录
docker rmi  `docker images -aq`   # 一次性删除所有本地的镜像记录
```

<br />

- 启动docker<br />sudo service docker start
- 停止docker<br />sudo service docker stop
- 重启docker<br />sudo service docker restart
- 列出Docker CLI命令<br />docker<br />docker container --help
- 显示Docker版本和信息<br />docker --version<br />docker version<br />docker info
- Execute Docker image<br />docker run hello-world
- 列出镜像列表<br />docker image ls
- 列出docker容器 (running, all, all in quiet mode)<br />docker container ls<br />docker container ls --all<br />docker container ls -aq


<br />

<a name="zXraT"></a>
### 命令大全：[https://www.runoob.com/docker/docker-command-manual.html](https://www.runoob.com/docker/docker-command-manual.html)
**容器生命周期管理**

- [run](https://www.runoob.com/docker/docker-run-command.html)
- [start/stop/restart](https://www.runoob.com/docker/docker-start-stop-restart-command.html)
- [kill](https://www.runoob.com/docker/docker-kill-command.html)
- [rm](https://www.runoob.com/docker/docker-rm-command.html)
- [pause/unpause](https://www.runoob.com/docker/docker-pause-unpause-command.html)
- [create](https://www.runoob.com/docker/docker-create-command.html)
- [exec](https://www.runoob.com/docker/docker-exec-command.html)

**容器操作**

- [ps](https://www.runoob.com/docker/docker-ps-command.html)
- [inspect](https://www.runoob.com/docker/docker-inspect-command.html)
- [top](https://www.runoob.com/docker/docker-top-command.html)
- [attach](https://www.runoob.com/docker/docker-attach-command.html)
- [events](https://www.runoob.com/docker/docker-events-command.html)
- [logs](https://www.runoob.com/docker/docker-logs-command.html)
- [wait](https://www.runoob.com/docker/docker-wait-command.html)
- [export](https://www.runoob.com/docker/docker-export-command.html)
- [port](https://www.runoob.com/docker/docker-port-command.html)

**容器rootfs命令**

- [commit](https://www.runoob.com/docker/docker-commit-command.html)
- [cp](https://www.runoob.com/docker/docker-cp-command.html)
- [diff](https://www.runoob.com/docker/docker-diff-command.html)

**镜像仓库**

- [login](https://www.runoob.com/docker/docker-login-command.html)
- [pull](https://www.runoob.com/docker/docker-pull-command.html)
- [push](https://www.runoob.com/docker/docker-push-command.html)
- [search](https://www.runoob.com/docker/docker-search-command.html)

**本地镜像管理**

- [images](https://www.runoob.com/docker/docker-images-command.html)
- [rmi](https://www.runoob.com/docker/docker-rmi-command.html)
- [tag](https://www.runoob.com/docker/docker-tag-command.html)
- [build](https://www.runoob.com/docker/docker-build-command.html)
- [history](https://www.runoob.com/docker/docker-history-command.html)
- [save](https://www.runoob.com/docker/docker-save-command.html)
- [load](https://www.runoob.com/docker/docker-load-command.html)
- [import](https://www.runoob.com/docker/docker-import-command.html)

**info|version**

- [info](https://www.runoob.com/docker/docker-info-command.html)
- [version](https://www.runoob.com/docker/docker-version-command.html)


<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />


