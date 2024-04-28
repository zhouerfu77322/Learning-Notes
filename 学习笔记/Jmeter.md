# Jmeter

### 前言

jmeter这个软件工具主要用于服务端系统的性能测试；

所以 学习jmeter之前，必须掌握一些基础知识：http协议、api的概念、HTML、JSON的基础知识



### 安装

#### 前置条件：已安装JDK且已配置环境变量（https://www.oracle.com/java/technologies/downloads/）

#### jmeter下载地址：https://jmeter.apache.org/download_jmeter.cgi

![image-20240423102027363](https://s2.loli.net/2024/04/23/2ZnWMSmhdKkA7Ru.png)

#### jmeter配置环境变量：

##### 新增JMETER_HOME环境变量，变量值为JMeter解压的路径

![image-20240423102849573](https://s2.loli.net/2024/04/23/A4WVOf1oReBDQEZ.png)

##### 编辑CLASSPATH变量，加上

%JMETER_HOME%\lib\ext\ApacheJMeter_core.jar;%JMETER_HOME%\lib\jorphan.jar;%JMETER_HOME%\lib\logkit-2.0.jar;

![image-20240423103023268](https://s2.loli.net/2024/04/23/MV5lwpu6L2O9sT3.png)

#### 设置中文（永久设置中文）

找到jmeter下的bin目录，打开jmeter.properties 文件

![image-20240423103130298](https://s2.loli.net/2024/04/23/vQrBeyD4oMdpYtx.png)

第三十七行修改为

language=zh_CN

去掉前面的#

![image-20240423103229075](https://s2.loli.net/2024/04/23/Qbj8tkNHyfxJFd1.png)

保存重启jmeter

![image-20240423103244026](https://s2.loli.net/2024/04/23/3Ky9ZLUS2RnoCNc.png)

### 测试计划和线程组

线程数：就是模拟用户的数量

Ramp-U时间：模拟的这些用户数量，需要在多少时间内操作完成

(线程数-1)/Ramp-Up=间隔时间

![image-20240423105758999](https://s2.loli.net/2024/04/23/t3m7JIKjHDr5EdL.png)

### 取样器







### 调试运行





### HTTP请求默认值配置







### 录制流量







### 模拟间隔时间







### 执行压力测试







### 统计表







### Cookie管理器







### 消息数据关联-变量和后置处理器









### CSV数据文件设置









### 断言







### 循环和前置处理



