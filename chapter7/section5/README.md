### RBD Mirror

#### **概述**

简单了说就是通过日志进行回放（replay）。

rbd-mirror服务负责不同Ceph集群的数据同步，当用户执行IO write操作时（必须写入primary image），首先会尝试写入journal，一旦写入完成会向client发起ACK确认，此时开始执行底层的image写入操作，与此同时rbd-mirror开始根据journal执行回放操作，同步到远端的ceph集群中。

#### **操作实例**

两个集群，都没有更改集群的名称，名称都是ceph，通过配置文件来识别集群。

分别在两个集群中的一台机器上进行操作：ansible-0（主），ceph0（备）

将ansible-0所在集群中的image备份到ceph0所在的集群上（当然，也可以将pool备份）

步骤如下：

[**相关配置**](7-5-1.md)

- 配置image属性
- 配置文件和密钥文件

[**安装rbd_mirror服务**](7-5-2.md)

- 安装rbd mirror服务

[**增加peer**](7-5-3.md)

- 增加peer

[**开启mirror模式**](7-5-4.md)

- 开启mirror模式