title: "It Starts with iGaze: Visual Attention Driven Networkingwith Smart Glasses"
date: 2014-11-21 11:25:38
tags: Paper
---

#1. 简  介

- 可穿戴计算设备的出现引起的世界的关注, 其中智能眼镜集成了许多传感器,  许多研究致力于改善只能眼镜的界面和体验, 
- 本论文主要探究使用智能眼镜开发一种新型网络模式,  使用者可以直接发送信息而不需要交换一些信息, 并能够通过视线收集感兴趣物体的信息


为了达到使用智能眼镜建立新型网络连接, 通过视线与目标建立网络连接, 需要解决一下挑战：

- 如何精确捕获用户的视线方向
- 如何通过用户视线进行目标设备目标匹配

<!--more-->

论文成就 :

1. 实现通过用户视线建立网络连接的新模式, 引入用户通过视线与周围交流或者交换信息的系统.
2. 提出新颖的捕获视线和目标的方案
3. 设计实现了iGaze平台, 用来精准捕获视线方向和建立物体设备连接
4. 对系统进行各种情形的测试.


#2. iGaze系统概述

- iGaze模块化硬件和软件, 可以运行与现存的高层协议
- iGaze用于网络连接不需要事先交换信息的网络场景.
- iGaze假设拥有用于捕获视线的相机, 处理计算, 网络功能和一些传感器.
- iGaze要求建立连接的目标静止. 


双向模式与单向模式 :

> 两个穿戴智能设备的用户, 通过眼部交流建立网络连接, 这种模式称为双向模式.


> 用户想要听过视线获取目标物体的信息(物体需要有设备进行相应), 这种模式称为单向模式


系统架构之软件

- 视线向量获取部分(实时眼部追踪模块,眼部追踪模块, 视线向量决策模块)
- 设备向量估计部分(信号追踪和设备方向决策模块)
- 视线驱动网络(定义信息形式和通信处理)


![向量](http://byson.img42.wal8.com/img42/434369_20140909170142/14164911962.png)

1. 双向模式中,给定视线交互的用户, 他们的视线向量方向相反
2. 单向模式中, 所有观察者设备到所有设备向量, 只有设备向量到实现目标的设备与视线向量一致.

双向模式中,给定视线交互的用户, 他们的视线向量方向相反

    单向模式中, 所有观察者设备到所有设备向量, 只有设备向量到实现目标的设备与视线向量一致.
    
![设备](http://byson.img42.wal8.com/img42/434369_20140909170142/14164911969.png)    


网络协议:

- 初始化iGaze眼镜, 广播视线给周围相邻设备
- 相邻iGaze眼镜捕获请求, 若在指定时间内没有事件发生,则丢弃请求, 否则进行向量对比,  成功后开始使用麦克风捕获声音信号.
- 初始化的iGaze等待相应, 相应同时双方眼镜发出立体信号
- 基于相应初始iGaze映射视线向量目标的网络ID


![网络](http://byson.img42.wal8.com/img42/434369_20140909170142/141649119746.png)


#3. 视线方向获取

视线方向获取:
iGaze追踪虹膜并检测实现方式，论文中使用了在 眼部相机中安装螺旋仪(检测头部状态)

![视线](http://byson.img42.wal8.com/img42/434369_20140909170142/141649119806.png)

通过眼部相机， 获取虹膜图像层面投影。通过相机坐标系获取实现向量， 然后传送到HU坐标系与设备坐标比对

![坐标](http://byson.img42.wal8.com/img42/434369_20140909170142/141649119857.png)

视线检测:

- 通过设置一个头部姿势, 如点头, 减少不相关视线的检测, 也能用于检测设备的方向
- 将眼部状态分为两种: 凝视和扫视
- 对眼球移动速率设置阈值, 低于一定阈值的为凝视状态, 高于阈值的则为扫视状态.


#4. 设备方向获取

针对存现方法难以利用到智能眼睛上, 论文中基于锁相环路( `Phase Locked Loop`)技术, 提出了追踪两个头戴式扬声器微妙的相对位移.
当一个出事设备发出高频信号被接手后, 信号通过多普勒效应频移. 通过PPL, 接收器可以追踪信号准确的相位, 相位相对位移的一部分.


#5. 系统实现

> 硬件

- 眼部相机追踪眼球运动
- 螺旋仪确定设备位置和坐标转换
- 麦克风和两个分开的扬声器
- Raspberry Pi平台用于数据计算处理
> 软件设计

- 实现双向模式, 连接两个设备用户,
- 实现单向模式, 连接无相机设备和安卓设备

6. 实验与评估
基本指标
|衡量指标|正确率|错误率|
|---|---|---|
|视线方向准确度| 91% | 8%|
| 设备方向准确度| 90%  |10%|
| 能量消耗|||


![测试1](http://byson.img42.wal8.com/img42/434369_20140909170142/14164911996.png)
![测试2](http://byson.img42.wal8.com/img42/434369_20140909170142/141649120061.png)


#6. 结  论

论文展现了iGaze(第一种低功耗智能眼镜)支持通过追踪视线建立网络, 并能够在视线交互时进行正确配对.
通过评估结果显示 : iGaze支持通过视线进行实时精确网络连接.


#7. 参考链接
[原文](http://www.cs.iit.edu/~xli/paper/Conf/iGaze-mobi14.pdf)