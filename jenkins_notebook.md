# jenkins笔记
## 使用docker安装Jenkins
1. 拉取Jenkins镜像
    >docker pull devopsjourney1/jenkins-blueocean:2.332.3-1 && docker tag devopsjourney1/jenkins-blueocean:2.332.3-1 myjenkins-blueocean:2.332.3-1
2. 创建网络:
    >docker network create jenkins
3. 运行容器
```shell
docker run --name jenkins-blueocean --restart=on-failure --detach \
--network jenkins --env DOCKER_HOST=tcp://docker:2376 \
--env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
--publish 8080:8080 --publish 50000:50000 \
--volume jenkins-data:/var/jenkins_home \
--volume jenkins-docker-certs:/certs/client:ro \
myjenkins-blueocean:2.414.2
```
4. 进入容器后获取密码
    1. 进入容器
        >docker exec jenkins-blueocean
    2. 获取密码
        >cat /var/jenkins_home/secrets/initialAdminPassword
5. 进入Jenkins网站进行配置

http://localhost:8080/ 输入获取到的密码进行安装配置