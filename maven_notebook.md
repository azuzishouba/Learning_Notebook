# Maven笔记
![](https://www.runoob.com/wp-content/uploads/2018/09/maven-logo-128.png)

Maven 翻译为"专家"、"内行"，是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。

Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。

 Maven 功能

Maven 能够帮助开发者完成以下工作：
* 构建
* 文档生成
* 报告
* 依赖
* SCMs
* 发布
* 分发
* 邮件列表
##  约定配置

Maven 提倡使用一个共同的标准目录结构，Maven 使用约定优于配置的原则，大家尽可能的遵守这样的目录结构。如下所示：
|目录 |目的
|:--|:--
|${basedir} |存放pom.xml和所有的子目录
|${basedir}/src/main/java |项目的java源代码
|${basedir}/src/main/resources |项目的资源，比如说property文件，springmvc.xml
|${basedir}/src/test/java |项目的测试类，比如说Junit代码
|${basedir}/src/test/resources |测试用的资源
|${basedir}/src/main/webapp/WEB-INF |web应用文件目录，web项目的信息，比如存放web.xml、本地图片、jsp视图页面
|${basedir}/target |打包输出目录
|${basedir}/target/classes |编译输出目录
|${basedir}/target/test-classes |测试编译输出目录
|Test.java |Maven只会自动运行符合该命名规则的测试类
|~/.m2/repository |Maven默认的本地仓库目录位置

## Windows上Maven的安装
1. 下载 Maven：
   * 访问 Maven 官方网站。
   * 在 "Files" 部分，下载 Binary zip archive（例如，apache-maven-3.x.x-bin.zip）。

2. 解压文件：
    * 下载完成后，解压 .zip 文件到你选择的目录，例如 C:\Program Files\Apache\maven。

3. 配置环境变量：
   * 打开 系统属性 > 高级系统设置 > 环境变量。
   * 在系统变量中，点击 Path 变量，然后点击 编辑，添加 Maven 的 bin 目录路径（例如 C:\Program Files\Apache\maven\apache-maven-3.x.x\bin）。

4. 设置 MAVEN_HOME 环境变量：
   * 在系统变量中，点击 新建，设置变量名为 MAVEN_HOME，变量值为 Maven 的安装路径（例如 C:\Program Files\Apache\maven\apache-maven-3.x.x）。

5. 验证安装：
   * 打开 命令提示符（Command Prompt），输入以下命令来验证是否安装成功：
```shell
mvn -version
```
如果一切正常，你应该看到 Maven 的版本信息。

## Maven 构建生命周期
Maven 构建生命周期定义了一个项目构建跟发布的过程。

一个典型的 Maven 构建（build）生命周期是由以下几个阶段的序列组成的：

![](https://www.runoob.com/wp-content/uploads/2018/09/maven-package-build-phase.png)

|阶段 |处理 |描述
|:--|:--|:--|
|验证 validate |验证项目 |验证项目是否正确且所有必须信息是可用的
|编译 compile |执行编译 |源代码编译在此阶段完成
|测试 Test |测试 |使用适当的单元测试框架（例如JUnit）运行测试。
|包装 package |打包 |将编译后的代码打包成可分发的格式，例如 JAR 或 WAR
|检查 verify |检查 |对集成测试的结果进行检查，以保证质量达标
|安装 install |安装 |安装打包的项目到本地仓库，以供其他项目使用
|部署 deploy |部署 |拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程

 为了完成 default 生命周期，这些阶段（包括其他未在上面罗列的生命周期阶段）将被按顺序地执行。

Maven 有以下三个标准的生命周期：

1. Clean 生命周期：

*  clean：删除目标目录中的编译输出文件。这通常是在构建之前执行的，以确保项目从一个干净的状态开始。

2. Default 生命周期（也称为 Build 生命周期）：

* validate：验证项目的正确性，例如检查项目的版本是否正确。
* compile：编译项目的源代码。
* test：运行项目的单元测试。
* package：将编译后的代码打包成可分发的格式，例如 JAR 或 WAR。
* verify：对项目进行额外的检查以确保质量。
* install：将项目的构建结果安装到本地 Maven 仓库中，以供其他项目使用。
* deploy：将项目的构建结果复制到远程仓库，以供其他开发人员或团队使用。

3. Site 生命周期：

* site：生成项目文档和站点信息。
* deploy-site：将生成的站点信息发布到远程服务器，以便共享项目文档。