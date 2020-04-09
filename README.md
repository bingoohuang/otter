# 环境搭建 & 打包

## 环境搭建

1. `sh install.sh`，或者 `install.bat`
1. `mvn clean install`

## 打包

1. `mvn clean install -Dmaven.test.skip -Denv=release`
1. 发布包位置：`target`

## 项目背景

阿里巴巴B2B公司，因为业务的特性，卖家主要集中在国内，买家主要集中在国外，所以衍生出了杭州和美国异地机房的需求，同时为了提升用户体验，整个机房的架构为双A，两边均可写，由此诞生了otter这样一个产品。

otter第一版本可追溯到04~05年，此次外部开源的版本为第4版，开发时间从2011年7月份一直持续到现在，目前阿里巴巴B2B内部的本地/异地机房的同步需求基本全上了otte4。

目前同步规模：

1. 同步数据量6亿
1. 文件同步1.5TB(2000w张图片)
1. 涉及200+个数据库实例之间的同步
1. 80+台机器的集群规模

## 项目介绍

1. 名称： otter \['ɒtə(r)\]
1. 译意： 水獭，数据搬运工
1. 语言： 纯java开发
1. 定位： 基于数据库增量日志解析，准实时同步到本机房或异地机房的mysql/oracle数据库. 一个分布式数据库同步系统

## 工作原理

![image](https://user-images.githubusercontent.com/1940588/78868865-36a90e80-7a76-11ea-9dae-b1884262959c.png)

### 原理描述

1. 基于[Canal](https://github.com/alibaba/canal)开源产品，获取数据库增量日志数据。
2. 典型管理系统架构，manager(web管理)+node(工作节点)
    - manager运行时推送同步配置到node节点
    - node节点将同步状态反馈到manager上
3. 基于zookeeper，解决分布式状态调度的，允许多node节点之间协同工作. 

### 什么是canal? 

otter之前开源的一个子项目，[开源链接地址](http://github.com/alibaba/canal)
 
### 文档

1. [Introduction](https://github.com/alibaba/otter/wiki/Introduction)
1. [QuickStart](https://github.com/alibaba/otter/wiki/QuickStart)
1. [AdminGuide](https://github.com/alibaba/otter/wiki/Adminguide)
1. [相关PPT PDF](https://github.com/alibaba/otter/wiki/%E7%9B%B8%E5%85%B3ppt%26pdf)
1. [常见问题](https://github.com/alibaba/otter/wiki/Faq)
1. (otter开源版本从内部演变而来，所以初始版本直接从4.x开始) [建议版本：4.2.15](https://github.com/alibaba/otter/releases)

### 相关开源

1. 阿里巴巴mysql数据库binlog的增量订阅&消费组件[canal](http://github.com/alibaba/canal)
1. 阿里巴巴去Oracle数据迁移同步工具(目标支持MySQL/DRDS)[yugong](http://github.com/alibaba/yugong)
