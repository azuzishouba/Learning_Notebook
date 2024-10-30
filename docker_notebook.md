# docker笔记
![docker](https://www.runoob.com/wp-content/uploads/2016/04/docker01.png)
## docker的安装
1. 启用Windows功能：
   * 打开“控制面板”，选择“程序”，然后点击“启用或关闭Windows功能”。
   * 在弹出的窗口中，勾选“虚拟机平台”和“适用于Linux的windows子系统”，点击“确定”并重启电脑。
2. 下载docker desktop安装包
   * 访问docker官网,windows-11版本下载: https://docs.docker.com/desktop/install/windows-install/
   * 下载好后别安装
3. 安装wsl
   * 执行命令:
        >wsl --install
    * 检查wsl版本
        >wsl --status
    * 需要升级wsl执行以下命令:
        >wsl --updated
    * 更新失败需手动下载Linux内核更新包：
        >https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-3---enable-virtual-machine-feature
    * 卸载安装好的ubuntu，重新执行:
        >wsl --install
    * 设置默认wsl版本
        >wsl --set-default-version 2 
    * 完成后输入用户名，密码能够显示正常Linux界面就是安装成功
    * 最后运行以下命令代表安装成功:
        >docker --verision 
## docker的image与container的关系
   * 镜像：包含了运行某个应用所需的一切内容，比如操作系统层、应用代码、库和依赖等。它是静态的，只读的。

   * 容器：是从镜像启动出来的运行实例，才是真正的运行环境。每个容器都有自己的进程、文件系统和网络接口，可以在其中执行代码。
## docker 镜像的使用
* 查看docker所有的镜像:
    >docker images
* 拉取镜像:
    >docker pull (images_name)

    > docker pull (images_name):(tag_name) 下载特定版本的镜像
## docker 镜像的推送
镜像推送将本地的镜像推送到远程网络仓库中
1. 登录 Docker Hub

    首先，确保你已登录到 Docker Hub：
    ```bash
    docker login
    ```
    输入你的 Docker Hub 用户名和密码。

2. 需要在Docker Hub创建好仓库类似于GitHub仓库
    repositoies->create repositoies
 
3. 标记镜像

    将 app 镜像标记为目标仓库的格式：
    ```bash
    docker tag target_app:tag_name username/repository_name:tag_name
    ```
    app的标签名尽量要和仓库的标签名保持一致

4. 推送镜像

    使用 docker push 命令将镜像推送到 azuzishouba/test 仓库：

    ```bash
    docker push username/repository_name:tag_name
    ```

## docker容器的使用
* 查看docker所有的镜像:
    >docker images
* 拉取镜像:
    >docker pull (images_name)

    > docker pull (images_name):(tag_name) 下载特定版本的镜像
*  运行容器:
    >docker run (images_name):(tag_name) 镜像可以存在也可以不存在，不存在直接拉取并运行容器

    >docker run -it (images_name):(tag_name) /bin/bash 进入容器并且以命令行模式进入容器
    
    参数说明：
    * -i: 交互式操作。
    * -t: 终端。
    * ubuntu: ubuntu 镜像。
    * /bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

    要退出终端，直接输入 exit:
    ```shell
    root@ed09e4490c57:/# exit
    ```
    >docker run -d (images_name):(tag_name) 在后台运行程序不显示运行信息，只显示运行ID

    >docker logs ID 显示容器的运行日志
* 查看正在运行的容器:
    >docker ps

    >docker ps -a  查看所有的容器包括不运行的
* 停止容器
    >docker stop (container_id)

    >docker restart (container_id) 停止的容器可以通过restart重启
* 进入容器
    在使用 -d 参数时，容器启动后会进入后台。此时想要进入容器，可以通过以下指令进入：
    * docker attach :退出容器时会导致容器的停止
    * docker exec:推荐大家使用 docker exec 命令，因为此命令会退出容器终端，但不会导致容器的停止。
#### attach 命令
下面演示了使用 docker attach 命令。
```shell
$ docker attach 1e560fca3906
```
![attch命令](https://www.runoob.com/wp-content/uploads/2016/05/docker-attach.png)
注意： 如果从这个容器退出，会导致容器的停止。
#### exec 命令
exec命令相当于进入容器的内部可以执行一些命令，可以改环境变量等，dockers用的是轻量化Linux，输入exit退出
下面演示了使用 docker exec 命令。
```shell
docker exec -it 243c32535da7 /bin/bash
```
![exec命令](https://www.runoob.com/wp-content/uploads/2016/05/docker-exec.png)
注意： 如果从这个容器退出，容器不会停止，这就是为什么推荐大家使用 docker exec 的原因。

更多参数说明请使用 <kbd>docker exec --help</kbd> 命令查看。
### docker容器的连接
#### docker容器的互联
##### 容器命名
当我们创建一个容器的时候，docker 会自动对它进行命名。另外，我们也可以使用 **--name** 标识来命名容器，例如：
```shell
runoob@runoob:~$  docker run -d -P --name runoob training/webapp python app.py
43780a6eabaaf14e590b6e849235c75f3012995403f97749775e38436db9a441
```
我们可以使用 docker ps 命令来查看容器名称。
```shell
runoob@runoob:~$ docker ps -l
CONTAINER ID     IMAGE            COMMAND           ...    PORTS                     NAMES
43780a6eabaa     training/webapp   "python app.py"  ...     0.0.0.0:32769->5000/tcp   runoob
```
#### docker容器网络端口映射
* 将容器内部端口映射到本地主机中:
    >docker run -d -p 9000:80 nginx:1.23
    ```shell
    $ docker ps
    CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                  NAMES
    a4251c3f32b9   nginx:1.23   "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes   0.0.0.0:9000->80/tcp   beautiful_ardinghelli
    ```
## docker dockerfile
### 指令详解
|Dockerfile指令|说明|
|:--|:--|
|FROM|指定基础镜像，用于后续的指令构建。|
|LABEL|添加镜像的元数据，使用键值对的形式。|
|RUN|在构建过程中在镜像中执行命令。|
|CMD|指定容器创建时的默认命令。|
|ENTRYPOINT|设置容器创建时的主要命令。|
|EXPOSE|声明容器运行时监听的特定网络端口。|
|ENV|在容器内部设置环境变量。|
|ADD|将文件、目录或远程URL复制到镜像中。|
|COPY|将文件或目录复制到镜像中。|
|VOLUME|为容器创建挂载点或声明卷。|
|WORKDIR|设置后续指令的工作目录。|
|USER|指定后续指令的用户上下文。|
|ARG|定义在构建过程中传递给构建器的变量，可使用 "docker build" 命令设置。|
|ONBUILD|当该镜像被用作另一个构建过程的基础时，添加触发器。|
|STOPSIGNAL|设置发送给容器以退出的系统调用信号。|
|HEALTHCHECK|定义周期性检查容器健康状态的命令。|
|SHELL|覆盖Docker中默认的shell，用于RUN、CMD和ENTRYPOINT指令。|

```dockerfile
#通常指定语言依赖包
FROM (language):(verision)
# 设置工作目录
WORKDIR /app
#构建中执行的命令，通常安装依赖包
RUN 
#指定需要的文件
COPY
# 暴露应用运行的端口
EXPOSE 3000
#指定容器创建最终执行的命令
CMD
```