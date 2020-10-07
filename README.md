<!--
 * @Description: 
 * @Author: HCQ
 * @Company(School): UCAS
 * @Date: 2020-10-06 21:13:33
 * @LastEditors: HCQ
 * @LastEditTime: 2020-10-07 17:09:04
-->
# docker
docker容器

@ [ChungKing](https://github.com/HuangCongQing/AI_competitions)，若fork或star请注明来源


website： https://www.docker.com

* [01 Docker介绍](01Docker介绍.md)
* [02 Docker常用命令](02Docker常用命令.md)
* [03 Dockerfile](03Dockerfile.md)


# Docker介绍

![](https://cdn.nlark.com/yuque/0/2020/png/232596/1592043513145-b9a847bd-fb7b-4f1d-83bd-81267c6c5725.png#align=left&display=inline&height=119&margin=%5Bobject%20Object%5D&originHeight=119&originWidth=199&size=0&status=done&style=none&width=199)<br />

<a name="7DM2I"></a>
## 官方文档
Docker 官网：[https://www.docker.com](https://www.docker.com/)<br />Github Docker 源码：[https://github.com/docker/docker-ce](https://github.com/docker/docker-ce)<br />
<br />文档：[https://docs.docker.com/](https://docs.docker.com/)   Docker文档是超级详细的！！<br />仓库（类似github）： [https://hub.docker.com/](https://hub.docker.com/)<br />帮助文档地址：[https://docs.docker.com/reference/](https://docs.docker.com/reference/)<br />

<a name="uhDST"></a>
## 介绍

- Docker 是一个开源的应用容器引擎，基于 [Go 语言](https://www.runoob.com/go/go-tutorial.html) 并遵从 Apache2.0 协议开源。
- 可以将你的**开发环境、代码、配置文件等一并打包**到这个容器中，并发布和应用到任意平台中。
- 容器是完全沙箱，之间不会有任何接口（类似 iPhone 的 app）,容器性能开销极低。
> Docker的前身是名为dotCloud的小公司，主要提供的是基于 PaaS（Platform as a  Service，平台及服务）平台为开发者或开发商提供技术服务，并提供的开发工具和技术框架。因为其为初创的公司，又生于IT行业，dotCloud受到了IBM，亚马逊，google等公司的挤压，发展举步维艰。于是，在2013年dotCloud  的创始人，年仅28岁的Solomon Hykes做了一个艰难的决定：**将dotCloud的核心引擎开源！**然而一旦这个基于 LXC（Linux  Container）技术的核心管理引擎开源，dotCloud公司就相当于走上了一条"不归路"。可正是这个孤注一掷的举动，却带来了全球技术人员的热潮，众程序员惊呼：太方便了，太方便了。也正是这个决定，让所有的IT巨头也为之一颤。一个新的公司也随之出世，它就是：Docker。可以说，Docker是一夜成名的！！


<br />

- 官方注册服务器（[hub.docker.com](https://hub.docker.com/)）的仓库中pull下CentOS的镜像

Docker类比于**虚拟机+操作系统**<br />
<br />**镜像：**提供运行环境，类似模板

- 好比一个模板，可以通过模板来创建容器服务
- tomcat==》tomcat01容器（提供服务），通过镜像可以创建多个容器（最终服务运行正在容器中）
- Docker官方网站专门有一个页面来存储所有可用的镜像，网址是：[index.docker.io](http://index.docker.io/)

**容器**：类似沙盒，可以将其看作一个极简的Linux系统环境（包括root权限、进程空间、用户空间和网络空间等）

- 容器是从镜像创建的运行实例。它可以被**启动、开始、停止、删除。**
- 独立运行一个或者一组应用。通过镜像创建
- **启动 开始 停止 删除基本命令**
- 可以理解为一个linux系统

**仓库：**类似于代码仓库，用来存放镜像文件（比如，各种版本的Ubuntu）的地方

- 仓库注册服务器（Registry）上往往存放着多个仓库，**每个仓库中又包含了多个镜像，**每个镜像有不同的标签**（tag）**
- 分为**共有仓库和私有仓库**
- 阿里云等都有容器服务（配置镜像加速）
- Docker Hub仓库存放镜像的地方，都存放在[hub.docker.com](https://hub.docker.com/)


<br />
<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/232596/1592048275075-6dfb9e07-9d06-4f4d-9883-2fae7d03d596.png#align=left&display=inline&height=400&margin=%5Bobject%20Object%5D&name=image.png&originHeight=595&originWidth=1110&size=483979&status=done&style=none&width=746)



### License

Copyright (c) [ChungKing](https://github.com/HuangCongQing/docker). All rights reserved.

Licensed under the [MIT](./LICENSE) License.