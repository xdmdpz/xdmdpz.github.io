---
layout: "about"
title: "About"
date: 2016-04-21 04:48:33
description: "找工作中，欢迎联系"
header-img: "img/if/光绘水晶球.jpg"
comments: true
---

![](http://xdmdpz.com/img/header_img/bg_1.jpg)

------------- 简历 -----------------
---- LastUpdate 2021-03-15 -----

吉林长白山人 |  1995.11

天津城建大学 | 软件工程 | 2018毕业 | 统招本科 | 全日制 | 学信网可查

手机号：MTg1MDIyNjI1NzU=

邮箱：eGRtZHB6QGZveG1haWwuY29t

---

### 技能

```shell
- 精通Java基础扎实，熟练掌握常用设计模式，JVM、多线程、io;
- 具备良好的编程思想、编程习惯,拥有良好的编码能力;
- 在业务开展中，能正确理解产品需求和问题分析定位能力，合理评估开发时间，对进行任务分解与实现;
- 精通主流Spring，SpringMVC，Mybatis，SpringDataJPA等开源技术;
  熟练使用Springboot、SpringCloud(Netflix/alibaba);
  熟练使用Zookeeper、Kafka、Mycat、Datax、Sqoop、Canal等中间件;
- 熟练使用Mysql，具有数据库设计、慢查询优化相关经验;
	熟练使用Redis、MongoDB等Nosql;
- 熟练掌握Docker、Ranchar、k8s,Vagrant、Docker-compose等容器以及编排技术;
	熟练部署编排容器，集群搭建，大数据环境搭建;
- 熟练使用Git、Maven项目管理及构建工具;
  熟练使用Ansible、Jenkins、Prometheus、Grafanas实现自动化运维及监控;
- 熟练使用ZeroTier、Frp搭建线上办公环境;
- 平常工作在mac与ubuntu系统，黑苹果爱好者;
- 多年一线研发经验，带过多个项目、实习生，有团队经验; 
- 小程序「职前公社」、「小象无忧」服务端、爬虫负责人
- 北极代码贡献者（Arctic Code Vault Contributor）
```

---

### 工作经验

##### Java研发工程师&大数据工程师：天津泰凡科技有限公司-大数据研发部(2018.6~至今)

```
- 项目服务端研发工作及架构设计
- 中国银行大数据相关的技术支持
- 搭建基础设施Nexus、Jenkins、LDAP（后使用华为DevCloud）
- 负责部门的容器定制，流水线制作
```
---

##### Java研发工程师：小米互娱-游戏发行部（2017.7~2018.6）（在校）

```
- 参与unity开发者站
- 负责小米互娱项目管理系统
- 解决IOS渠道包打包问题
```

##### Java研发工程师：联合华通（天津）科技有限公司-产品研发部（2016.6-2017.7）(在校)

```
- 全程参与一卡通整个平台的设计与实现，公交卡充值消费
- 大学期间收入来源，公司在学校里面，弹性工作
```

---

### 项目经验

---

#### 智慧武清综合运营中心 - 泰凡科技

```
> 智慧武清综合运营中心主要包括总体态势、政务服务、社会治理、公共安全、创城成效和城市数据等专题，通过汇聚政府数据和社会数据形成城市大数据
> 涉及技术：SpringCloud、SpringBoot、Eureka、Gateway、Ribbon、Hystrix、Feign、MybatisPlus 、docker、MariaDB、JWT、swagger、OKHTTP、Jeval、Redis
> 工作内容
  - 对接委办局、数据中台、原型，根据数据情况调整指标
  - 架构设计、微服务拆分根据需求使用velocity完善后端脚手架
  - 指标模块服务，维护指标信息、计算方法
  - 定时计算服务，按照指标原始数据更新频率定时计算，推送实时数据
  - 实现数据展示服务，统一数据格式，支撑图表表格等数据的展示
  - 实现数据查询模块，兼容多种数据源查询
  - 实时数据、多次请求的数据，提前缓存在redis中，降低了服务器的压力
  - 基于字符串表达式的指标构建
  - 视频数据对接，SmartEarth数据对接，社会数据对接
  - 容器制作、部署脚本编写，测试、生产服务器发布使用Redis缓存机制，降低了服务器的压力
  - 在整体安全性方面使用布隆过滤器可以有效减少恶意访问的问题，避免缓存击穿问题
```
#### 数据可视化平台 - 泰凡科技

```
> 此项目是一款基于浏览器的可视化平台，主要包括用户管理、项目管理、添加数据源、可视化编辑、管理驾驶舱几大模块，能够便捷的对文本类型数据、关系型数据库数据以及部分大数 据库数据进行可视化展示，并基于驾驶舱实现对可视化图表的管理和展示，提高业务人员的工作 效率，提升管理者决策能力
> 涉及技术 SpringBoot、SpringDataJpa 、docker、MariaDB、JWT、swagger、calcite-csv、多种数据库
- 工作内容
  - 产品从0到1构建，技术调研、参与需求设计、负责架构设计、服务端研发
  - 使用vagrant + docker-comose 统一开发测试环境
  - 设计绘图规则，统一数据格式
  - 使用velocity按需编写数据库代码生成
  - 数据源导入模块：关系型数据库：mysql、oracle、SQLserver、db2 | 大数据数据库：hive、impala |文件（calcite与sqlite）：csv、txt、excel
  - Sql解析模块，用druid将绘图sql抽象成AST语法树，实现SQL检验
  - 使用token+Redis实现用户登录的身份验证
  - 容器制作、部署脚本编写，测试、生产服务器发布
```



#### 数据分析平台 - 泰凡科技

```
> 此项目是一款基于大数据的分析平台，平台主要包括用户管理、数据对接、项目管理、数据分析(多维分析和算法分析)、任务监控以及数据查询模块。平台支持文本数据、数据库数据的对接，提供多维分析和算法分析功能，通过构建数据模型和数据立方体，对原始数据进行预计算，并把计算结果保存在Hbase数据库中，通过标准SQL语句，实现对海量数据交互式查询的能力。
> 涉及技术： SpringBoot、SpringDataJpa 、MariaDB、calcite、Sqoop、Hadoop、Hive、Hbase、kylin、docker
- 工作内容
  - 产品从0到1构建，参与需求分析，负责技术调研、架构设计、服务端研发
  - 使用vagrant + docker-comose + ansible 统一开发测试环境、大数据环境
  - 调研实现数据源导入、日志
  - 调研kylin，对接Kylin的RestfulApi
  - 数据源导入模块：关系型数据库：mysql、oracle、SQLserver、db2 | 大数据数据库：hive、hbase、impala
  - 使用token+Redis实现用户登录的身份验证
  - 日志管理，自定义日志注解按需记录
  - 容器制作、部署脚本编写，测试、生产服务器发布
```


#### 知识图谱大数据平台- 泰凡科技

```
> 本项目是基于neo4j图数据库的可视化分析平台。平台分为用户管理、图谱管理、领域知识检索、图谱可视查询、模式管理、模型定义、图谱生成和图谱维护八大模块，支持图谱从无到有的便捷创建，最终以3D可视化效果呈现不同实体之间的关联关系，直观的向用户展现数据之间的潜在价值 。
> 涉及技术：SpringBoot、、MybatisPlus 、docker、MariaDB、JWT、swagger、OKHTTP、redis、Springboot + mybatis + mysql + neo4j
> 工作内容
  - 产品从0到1构建，参与需求分析设计
  - 知识图谱相关技术调研、服务端架构设计
  - Neo4J交互模块研发
  - 文档分析模块研发研发
```

---
#### 项目管理系统 - 小米互娱

```
- 解决渠道包测试混乱，项目管理等现存问题
- 将游戏公司发来的包重新签名，并上架到不同应用商店
- SpringBoot、SpringDataJpa、vrgrant 、docker、MariaDB、SpringSecurity、xcodebuild
- vue、elementUI、axios、vuex、vue-router
- 全栈开发
- 技术调研、参与需求设计、项目环境搭建，基础代码编写
- 实现IOS渠道包静默打包
- 编写权限模块并接入小米cas
- 使用vagrant统一开发环境
- 使用velocity编写符合需求以及技术栈的代码模板(后台页面、逻辑删除、乐观锁等)
- 容器制作、部署脚本编写
```


