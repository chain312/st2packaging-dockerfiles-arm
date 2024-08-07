# 用来生成构建arm版本st2安装包的Docker镜像


> *Note:*
这个项目是从[st2packaging-dockerfiles](https://github.com/StackStorm/st2packaging-dockerfiles)fork而来<br>
## 1. st2 容器镜像的构建过程
在此说明下st2容器镜像的构建过程。<br>
1、首先要先先构建st2的deb、或者rpm包。<br>
2、然后通过Dockerfile安装步骤1中构建st2安装包。<br>

## 2. st2 构建容器镜像所使用的项目
构建deb或者rpm包要使用[st2packaging-dockerfiles](https://github.com/StackStorm/st2packaging-dockerfiles)和[st2-packages](https://github.com/StackStorm/st2-packages),[st2packaging-dockerfiles](https://github.com/StackStorm/st2packaging-dockerfiles)项目是生成deb的容器，而[st2-packages](https://github.com/StackStorm/st2-packages)是启动生成deb安装包的项目，
<br>

## 3. 构建arm版本的deb安装包
在1和2中大概了解到st2有自己的CI/CD流程，要构建deb包，就要先把CI/CD使用的镜像构建成arm版本的<br>
首先构建arm版本的stackstorm/packagingbuild:focal，是在这个镜像中构建deb包的，进入到```./focal/```下，运行```docker build -t stackstorm/packagingbuild:focal .```,这样我们就有了arm版本的stackstorm/packagingbuild:focal镜像。<br>
packagingrunner是启动rake命令的容器，packagingrunner要通过ssh向packagingbuild发送命令执行打包命令，接下来，进入到```./packagingrunner/```下，运行```docker build -t stackstorm/packagingrunner:focal .```，这样我们就有了arm版本的stackstorm/packagingrunner:focal镜像。<br>
构建完这两个容器后就可以去[st2-packages-arm](https://github.com/chain312/st2-packages-arm)这个项目构建ARM的deb包了。

