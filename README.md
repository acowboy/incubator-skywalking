Sky Walking
==========

<img src="http://wu-sheng.github.io/sky-walking/images/skywalking.png" alt="Sky Walking logo" height="90px" align="right" />

SkyWalking: Large-Scale Distributed Systems Tracing Infrastructure, 是一个对JAVA分布式应用程序集群的业务运行情况进行追踪、告警和分析的系统。

[![Build Status](https://travis-ci.org/wu-sheng/sky-walking.svg?branch=master)](https://travis-ci.org/wu-sheng/sky-walking)
![license](https://img.shields.io/aur/license/yaourt.svg)

# 简介 / abstract
* 核心理论为[Google Dapper论文：Dapper, a Large-Scale Distributed Systems Tracing Infrastructure](http://research.google.com/pubs/pub36356.html),英语有困难的同学可参考[国内翻译](http://duanple.blog.163.com/blog/static/70971767201329113141336/)
* 本分析系统能通过动态字节码技术，对现有的JAVA应用或J2EE应用进行监控和数据收集，并针对应用进场进行准实时告警。此外提供大量的调用性能分析功能，解决目前的监控系统主要监控进程、端口而非应用实际性能的问题。
* 支持国内常用的dubbo以及dubbox等常见RPC框架，支持应用异常的邮件告警
* skywalking-sdk层面提供的埋点API，同步阻塞访问时间小于100μs
* 通过[byte-buddy](https://github.com/raphw/byte-buddy)，插件将通过动态字节码机制，避免代码侵入性，完成监控。动态代码模式埋点，同步阻塞访问时间应在200-300μs
* 提供一定的日志数据分析和展现能力，减少或者避免使用团队的二次开发
* SkyWalking is an open source Large-Scale Distributed Systems Tracing Infrastructure, also been known as APM(Application Performance Management) tool. SkyWalking provides a solution to help monitor and analysis a Large-Scale Distributed Systems.
* SkyWalking supports popular rpc frameworks, such as [dubbo](https://github.com/alibaba/dubbo), [dubbox](https://github.com/dangdangdotcom/dubbox), etc., supports email-alert when application occurs unexpected exception。
* SkyWalking's basic API, execution time of blocking saving span must less than 100μs.
* By using [byte-buddy](https://github.com/raphw/byte-buddy) (Thanks to [raphw](https://github.com/raphw)), plugins use dynamic byte code generation to avoid invasive codes. plugins API, execution time of blocking saving span must between 200μs and 300μs, including execution time of dynamic byte code.
* Provide trace log analysis and presentation capabilities, Reduce or avoid add-on functions development.

|plugins|using config file|using dynamic byte code| coding |remarks|
| ----------- |---------| ----------|----------|----------|
|web-plugin|web.xml| - | - | - |
|spring-plugin| spring config file | - | - | - |
|tomcat8-plugin| - | YES | - | - |
|dubbo-plugin| - | YES | - | - |
|jdbc-plugin| jdbc config file | - | - | - |
|httpClient-4.x-plugin| - | YES | - | - |
|jedis-2.x-plugin| - | YES | - | - |



# 主要贡献者 / Contributors
* 吴晟 [wusheng](https://github.com/wu-sheng) &nbsp;&nbsp;wu.sheng@foxmail.com
* 张鑫 [zhangxin](https://github.com/ascrutae) &nbsp;&nbsp;

# 交流
<img src="http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/chatapp/toutiao.JPG" alt="Sky Walking TouTiao" height="280px" align="left" />
* Mail to：wu.sheng@foxmail.com
* QQ群：392443393，请注明“Sky Walking交流”
* 谁在使用Sky Walking?[点击进入](https://github.com/wu-sheng/sky-walking/issues/34)。同时请各位使用者反馈下，都在哪些项目中使用。
* if you are using SkyWalking，[Report to us](https://github.com/wu-sheng/sky-walking/issues/34) please.
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# 整体架构图
![整体架构图](http://wu-sheng.github.io/sky-walking/sample-code/images/skywalkingClusterDeploy.jpeg)

# 典型页面展现 / Typical UI show
* 支持浏览器：Firefox/Chrome

## 实时调用链路
* 实时链路追踪展现
![追踪连路图1](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/callChain.png)
* 实时链路追踪详细信息查看
![追踪连路图2](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/callChainDetail.png)
* 实时链路追踪日志查看
![追踪连路图3](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/callChainLog.png)
* 实时链路异常告警邮件
![告警邮件](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/alarmMail.png)
* 添加应用
![添加应用](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/addApp.png)
* 应用列表展现
![应用列表展现](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/appList.png)

## 分析汇总
* 分析结果查询，根据viewpoint模糊匹配查询。查询方式为viewpoint: + 关键字
![应用列表展现](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/searchAnalysisResult.png)
* 分析结果展现，通过分析结果查询页面点击进入
![应用列表展现](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/analysisResult.png)
* 分析典型调用链展现
![应用列表展现](http://wu-sheng.github.io/sky-walking/sample-code/screenshoot/1.0b/typicalAnalysisResult.png)

# Quick Start
- master用于迭代开发，需要稳定版本请参见[Releases](releases)。1.0b的完整代码，请参见 [1.0-beta-tag](https://github.com/wu-sheng/sky-walking/tree/1.0-beta)
- Developing of version 1.0-Final on branch Master. The source code of version [1.0-beta-tag](https://github.com/wu-sheng/sky-walking/tree/1.0-beta)

## 部署第三方软件 / Required of third party softwares
- JDK 1.7
- zookeeper 3.4.6
- apache hbase 1.1.2
- mysql
- tomcat 7
- redis-3.0.5

## 插件支持的JDK / Supported jdk version
- 1.7以上版本 / support 1.7+

## 编译与部署 / Build and deploy
- 服务端发布版本[下载](https://github.com/wu-sheng/sky-walking/releases)  (.tar.gz)
- Download Server release version. [Download](https://github.com/wu-sheng/sky-walking/releases)  (.tar.gz)
- [配置应用服务器](CONFIG_DOC.md)
- [config servers](CONFIG_DOC.md)
- 如果您想自己编译最新版本，可参考《[代码编译说明](BUILD_DOC.md)》
- [Code compilation instructions](BUILD_DOC.md)


## 下载官方的agent / Download offical agent
[ ![Download](https://api.bintray.com/packages/wu-sheng/skywalking/com.ai.cloud.skywalking-agent/images/download.svg) ](https://bintray.com/wu-sheng/skywalking/com.ai.cloud.skywalking-agent/_latestVersion)

- 官方agent通过[skywalking bintray官网](https://bintray.com/wu-sheng/skywalking/)托管，可使用公网仓库[https://jcenter.bintray.com/](https://jcenter.bintray.com/)下载。
- use public repository  [https://jcenter.bintray.com/](https://jcenter.bintray.com/) to download sdk


## 使用-javaagent 启动应用程序 / start application with -javaagent
- 为应用程序添加启动参数
```shell
java -jar ...  -javaagent:/..ospath../skywalking-agent-x.x-Final.jar
```

## 下载并设置授权文件 / Download auth file
- 注册并登陆过skywalking-webui，创建应用。（一个用户代表一个逻辑集群，一个应用代表一个服务集群。如前后端应用应该设置两个应用，但归属一个用户）
- Sign up and login in skywalking-webui. Create application as needed.
- 下载授权文件，并在运行时环境中，将授权文件加入到CLASSPATH或LIB中
- download auth file(*.jar), and add the jar file to the CLASSPATH or lib.

## 在运行时环境中设置环境变量 / set environment variables 
```
export SKYWALKING_RUN=true
```
- 设置完成后，SkyWalking将随应用启动运行
- After set env, SkyWalking will be working, when application startup.

# 在应用程序中显示traceid / How to find tid
- [Find TID](HOW_TO_FIND_TID.md)

# QA
- [SkyWalking SDK是否已经工作？ Is SkyWalking SDK Running?](QA/IS_RUNNING.md)
- [tid在web-ui上无法查询. tid can't be search on web-ui](QA/TID_CANNOT_BE_SEARCH.md)
- [SkyWalking Server的运行情况. The status of SkyWalking Server](QA/SERVER_RUNNING_STAUTS.md)
- [SkyWalking Analysis部署运行常见问题. The FAQ of SkyWalking Analysis deployment](QA/deploy-sw_analysis-problem.md)

# 源代码说明
* [追踪日志明细存储结构说明. the storage structure of tracking logs](skywalking-server/doc/hbase_table_desc.md)
