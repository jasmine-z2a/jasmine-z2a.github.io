---
title: ros学习
category: ros
order: 1
---
ros1和ros2 的区别：？
RPC：
ros1的最高版本是noetic （支持python3）
## ros的通信机制
1.启动ros core
### 话题通讯（发布和订阅模式）
 1. talker注册   publisher
 2. listenser注册  subscriber
 3. ros master 信息的匹配和管理，
 4. talker 确认请求
 5. listener 与 takler 建立连接
 6. talker 和 listener 通讯 （TCP/IP协议） 
  可以有多个 talker 和 listenser ，没有先后顺序   

### 服务通讯（请求响应模式）
 1. server注册  service  
 2. client注册  serviceProxy 
 3. ros master 信息的匹配和管理， 
 4. server 发送响应  
 server端要先启动  



