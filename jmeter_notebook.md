# jmeter 笔记
## jmeter的安装
1. 首先确保安装了java,并配置了java_home
    > java --version
    > javac --version
2. 下载apache jmeter
 
    https://jmeter.apache.org/download_jmeter.cgi
3. 下载解压后点击/bin/jmeter.bat或者在bin目录下执行cmd输入jmeter.bat打开jmeter
## jmeter GUI
![jmeter_GUI](/screen_shot/jmeter_GUI.png)
## jmeter创建测试用例
1. 创建测试计划
2. 创建线程组
    ![theard_group_interface](/screen_shot/theard_group_interface.png)
    * Number of threads:用户数量
    * Ramp -up time:在多少秒内启动这些用户数
    * loop:循环多少次
3. 添加请求样本(Sampler),并保存
    ![http_sampler_interface](/screen_shot/http_sampler_interface.png)
    * protocol:协议,是http还是https
    * server name:域名,例如www.Google.com
    * path:接口路径,例如https://google.com
4. 添加listener(监听器)view result tree,保存
5. 点击运行
## thread groups(线程组)
![theard_group_interface](/screen_shot/theard_group_interface.png) 
   * Number of theards:用户数量
   * Ramp -up time:在多少秒内启动这些用户数
   * loop:循环多少次
   * same user on each interation:在迭代中使用相同用户
   * delay thread creation until needed:延迟线程的创建直到需要
   * specify thread lifetime:指定线程生命周期
## sampler(请求样本)
![http_sampler_interface](/screen_shot/http_sampler_interface.png)
   * protocol:协议,是http还是https
   * server name:域名,例如www.Google.com
   * path:接口路径,例如https://google.com
   * timeouts:设置连接和读取超时时间,单位为ms,超时则报错
   * follow redirects:跟随重定向,如果启用此选项，当服务器返回重定向响应时（例如，HTTP 301），JMeter 会自动发送新的请求到重定向的 URL。如果禁用，JMeter 会直接处理重定向响应，而不会发起新的请求。
   * use keepalive:如果启用，JMeter 会在一个连接上发送多个请求，避免每个请求都建立新的连接，从而提高性能。禁用此选项将会每次请求建立新的连接，增加延迟。
## listener(监听器)
![listener_interface](/screen_shot/listener_interface.png)
* connect time:从开始直到连接上接口的时间
* latency:延迟,请求发送到接收到响应开始之间的时间差,是指请求到响应开始的时间,即从请求发起到接收到第一个字节的响应的时间间隔。
* response time:整个周期,从发送请求都返回完整数据的时间
## recording(记录)
1. 创建thread group,在thread group创建controller ->recording controller
2. 在test plan下创建 non-test elements->http(s) test script recorder
3. 在target controller选择test plan>thread group>recording controller
4. 端口号默认8888即可
5. 在Firefox中设置中搜索certificate(证书)导入jmeter bin目录下证书,如果没有运行一下
6. 在Firefox设置中搜索proxy(代理)手动设置代理,端口号8888,主页设置localhost
![firefox_proxy_interface](/screen_shot/firefox_proxy_interface.png)
7. 运行,执行网页相关操作
## assertion(断言)
* response assertion
  1. 在线程组或者请求下添加断言,可以是response assertion
![response_assertion_interface](/screen_shot/response_assertion_interface.png)
  2. 选择response code,add pattern to text,状态码设为200
* duration assertion
1. 在线程组或者请求下添加duration assertion断言
![duration_assertion_interface](/screen_shot/duration_assertion_interface.png)
2. 在duration in milliseconds(ms)里填写最多的时间
* size assertion
1. 填写最大byte,再选择比较关系
![size_assertion_interface](/screen_shot/size_assertion_interface.png)
## CSV数据驱动测试
1. 创建csv数据配置
  ![csv_interface](/screen_shot/csv_interface.png)
2. 创建csv数据集并添加数据
3. 对照数据集设置参数
4. 对照数据集的值使用${}来传参
![java_response](/screen_shot/java_response.png)
## CMD命令行
1. 在bin目录下执行cmd,并在指定位置生成测试报告(须在bin目录下执行cmd)
```shell
jmeter -n -t "location of test file" -l "location of result file"
```
eg:
```shell
jmeter -n -t "D:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\HTTP Request 1.jmx" -l "D:\360MoveData\Users\YAN\Desktop\reports\result.csv"
```
1. 在生成报告后,根据报告生成html报告(须在bin目录下执行cmd)

eg：
```shell
jmeter -n -t "D:\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\HTTP Request 1.jmx" -l "D:\360MoveData\Users\YAN\Desktop\reports\result.csv" -e -o "D:\360MoveData\Users\YAN\Desktop\reports\html reports"
```
***执行时测试文件result.csv需要重新生成***
***-e -o 是专门生成html测试报告的参数***