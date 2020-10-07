# 03 Dockerfile

<a name="JDjcU"></a>
## 1 Dockerfile介绍
> Dockerfile 是一个用来**构建镜像**的文本文件，文本内容包含了一条条构建镜像所需的指令和说明。

**构建步骤**

1. 编写一个dockerfile文件
1. docker build 构建 一个镜像
1. docker run 运行镜像
1. docker push 发布镜像（DockerHub，阿里云镜像）


<br />
<br />[https://www.runoob.com/docker/docker-dockerfile.html](https://www.runoob.com/docker/docker-dockerfile.html)<br />哔哩哔哩：[https://www.bilibili.com/video/BV1og4y1q7M4?p=24](https://www.bilibili.com/video/BV1og4y1q7M4?p=24)<br />
<br />
<br />**查看官方dockerhub中的Dockerfile：**

- 很多官方的镜像都是基础包，很多功能没有，我们通常自己搭建自己的镜像


<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602051615328-ec932cf7-4ce9-4883-a240-57d0fa744f5e.png#align=left&display=inline&height=225&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=763&originWidth=1347&size=253202&status=done&style=none&width=398)![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602051647339-4304796a-fdb1-43ee-b4a6-72dc34d0f031.png#align=left&display=inline&height=256&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=829&originWidth=1070&size=305411&status=done&style=none&width=330)<br />
<br />
<br />
<br />

<a name="YiTUc"></a>
## 2 Dockerfile构建

<br />**基础知识：**

1. 镜像是一层一层的，dockerfile中每行命令都是一层
   1. **注意**：Dockerfile 的指令每执行一次都会在 docker 上新建一层。所以过多无意义的层，会造成镜像膨胀过大。可用 **&&** 连接
2. 文件格式（区分大小写）：  指令（大写） 参数(小写)
2. **#** 表示注释

![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602052004146-d1df9b0e-4fd0-4026-857c-5be4e4ba2407.png#align=left&display=inline&height=366&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=366&originWidth=528&size=137892&status=done&style=none&width=528)<br />
<br />

<a name="lYbC1"></a>
### 简易版Dockerfile
```dockerfile
FROM centos
VOLUME ["volume01", [volume02]]
CMD echo "------end--------"
CMD /bin/bash
```
构建镜像image,找到当前目录的Dockerfile，开始构建<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1601990812357-338e6f3c-a782-4fcc-b384-fe3445e3afaa.png#align=left&display=inline&height=137&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=185&originWidth=673&size=47524&status=done&style=none&width=497)<br />

```powershell
# docker build 
# docker build -t 镜像名称:镜像标签 .
docker build -f dockerfile-simple -t hcq/centos .

	-f dockerfile文件路径
	-t   . 代表本次执行的上下文路径
 
 # 创建容器
 docker run -it hcq/centos /bin/bash
```
![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1601990348392-5f18115d-e281-4ae4-b6c5-69197f533e03.png#align=left&display=inline&height=354&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=354&originWidth=765&size=84565&status=done&style=none&width=765)<br />
<br />

<a name="RalEP"></a>
## 3 Dockerfile命令

```shell
FROM    		#制作base image 基础镜像，尽量使用官方的image作为base image
MAINTAINER 	# maintainer 镜像作者（姓名+邮箱）
RUN					# docker镜像构建时需要运行的命令
ADD  				# 步骤： tomcat镜像 这个tomcat
WORKDIR 		# 镜像的工作目录
VOLUME 			# 挂载的目录
EXPOST   		# 暴露端口配置
CMD 				# 指定容器启动时要运行的命令，只有最后一个会生效，可被替代
ENTRYPOINT 	# 指定容器启动时要运行的命令，可追加命令
ONBUILD   	# 当构建一个被继承Dockerfile，这个时候运行ONBUILD指令	触发指令
COPY 				# 类似ADD ，将文件拷贝到镜像中
ENV   			# 构建时，设置环境变量 ，后续的指令中，就可以使用这个环境变量 $<key>
						# ENV <key> <value>
						# ENV <key1>=<value1> <key2>=<value2>...
```

<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602052278234-84858818-07c3-436a-b1ba-b551cb5c430b.png#align=left&display=inline&height=478&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=478&originWidth=854&size=458026&status=done&style=none&width=854)<br />
<br />
<br />

## 4 实战测试
Docker Hub中，99%的镜像都是从**scratch**基础镜像来的<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602054584385-e918f48a-7642-41a8-9532-96e882268b69.png#align=left&display=inline&height=570&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=570&originWidth=689&size=67948&status=done&style=none&width=689)
```powershell
# 1. 编写Dockerfile的镜像
FROM  centos
MAINTAINER hcq<1756260160@qq.com>
ENV MYPATH /usr/local
WORKDIR $MYPATH
RUN yum -y install vim
RUN yam -y install net-tools
EXPOSE 80
CMD echo $MYPATH
CMD /bin/bash

# 2 通过这个文件构建镜像
docker build -f mydockerfile -t mycentos:0.1 .

# 3 测试运行
 docker run -it  mycentos:0.1
```

<br />基础镜像<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602055748042-d4c06bdc-d662-4add-a14c-93dff3fde306.png#align=left&display=inline&height=248&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=248&originWidth=799&size=158903&status=done&style=none&width=799)<br />增强后<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602055784304-226d5078-114a-438e-8801-f7cca0b9ea21.png#align=left&display=inline&height=517&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=517&originWidth=856&size=421713&status=done&style=none&width=856)<br />
<br />
<br />通过**docker history 镜像id名 ** 查看镜像时怎么一步一步构建的<br />
<br />![图片.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1602055873200-7e318f55-1c1b-4e32-a7e2-2c8f82367249.png#align=left&display=inline&height=332&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=332&originWidth=1061&size=471370&status=done&style=none&width=1061)<br />
<br />

<a name="pVCn7"></a>
### CMD和ENTRYPOINT的区别
```shell
CMD 				# 指定容器启动时要运行的命令，只有最后一个会生效，可被替代
ENTRYPOINT 	# 指定容器启动时要运行的命令，可追加命令
```


```shell
# 1 写dockerfile文件 dockerfile-cmd
FROM centos
CMD ["ls", "-a"]

# 2 通过这个文件构建镜像
docker build -f dockerfile-cmd -t cmd-test .

# 3 测试 # -l覆盖 
 docker run cmd-test  -l  # -l 
```


```shell
# 1 写dockerfile文件 dockerfile-entrypoint
FROM centos
ENTRYPOINT ["ls", "-a"]

# 2 通过这个文件构建镜像
docker build -f dockerfile-entrypoint -t test-entrypoint .

# 3 测试 # -l追加
 docker run test-entrypoint -l 
```


<a name="enImx"></a>
### Tomcat镜像 todo

<br />[https://www.bilibili.com/video/BV1og4y1q7M4?p=30](https://www.bilibili.com/video/BV1og4y1q7M4?p=30)<br />
<br />
<br />
<br />
<br />
<br />

