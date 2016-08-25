# 引言

## 产品版本

目前与本文档相对应的产品版本为Mevoco 1.5。

## 读者对象

本文档详述了Mevoco云系统部署的安装、使用教程。本文档主要适用于以下读者：

* 技术支持工程师
* 部署运维工程师
* 产品咨询工程师
* 对Mevoco有兴趣研究的相关人员

## 术语定义

| 术语 | 概念 |
| --- | --- |
| 管理节点 | 安装Mevoco系统的物理主机，提供UI管理、云系统部署功能 |
| 计算节点 | 也称之为物理机，为云主机实例提供计算、内存、网络、存储的物理主机。虽然可以添加管理节点为一个计算节点，但不建议在生产环境中这么部署 |
| 集群 | 一个集群是类似主机（Host）组成的逻辑组. 在同一个集群中的主机必须安装相同的操作系统（虚拟机管理程序,hypervisor）, 拥有相同的二层网络连接, 可以访问相同的主存储. 在实际的数据中心, 一个集群通常对应一个机架（rack） |
| 云主机 | Mevoco 特制虚拟机，即运行在物理机上的虚拟机实例，具有独立的IP地址，可以安装部署应用服务 |
| 主存储 | 用于存储云主机的磁盘文件的存储服务器。支持本地存储、NFS、Ceph、Shared Mount Point等类型 |
| 镜像 | 云主机所使用的镜像模板文件，包含了云主机的操作系统，也可以定制安装相应的软件 |
| 镜像服务器 | 也称之为备份存储服务器，存储云主机镜像文件的物理主机。建议单独部署镜像服务器 |
| 云盘 | 云主机的数据盘，给云主机提供额外的存储空间，一块云盘在同一时刻只能挂载到一个云主机。一个云主机最多可以挂载24块云盘 |
| 计算规格 | 启动云主机涉及到的CPU数量、内存、网络设置等规格定义 |
| 云盘规格 | 创建云盘容量大小的规格定义 |
| 安全组 | 针对云主机进行第三层网络的防火墙控制，对IP地址、网络包类型或网络包流向等可以设置不同的安全规则 |
| L2NoVlanNetwork | 物理主机的网络连接不采用Vlan设置 |
| L2VlanNetwork | 物理主机节点的网络连接采用Vlan设置，Vlan需要在交换机端提前进行设置 |
| 二层网络 | 计算节点的物理网卡设备名称，例如eth0 |
| 三层网络 | 云主机使用的网络配置，包括IP地址范围，网关，DNS等 |
| 公有网络 | 由因特网信息中心分配的公有IP地址或者可以连接到外部互联网的IP地址 |
| 私有网络 | 云主机连接和使用的内部网络 |
| 弹性IP | 公有网络接入到私有网络的IP地址 |

## 中英文对照

| 中文 | 英文 |
| --- | --- |
| 管理节点 | Management Node |
| 集群 | Cluster|
| 物理机 | Host |
| 云主机 | VM Instance |
| 镜像服务器（备份服务器） | Backup Storage |
| 主存储 | Primary Storage |
| 镜像 | Image |
| 云盘 | Volume |
| 集群 | Cluster |
| 区域 | Zone |
| 二层网络 | L2 Network |
| 三层网络 | L3 Network |
| 安全组 | Security Group |
| 计算规格 | Instance Offering |
| 云盘规格 | Disk Offering |
| 扁平网络模式 | Flat Network Mode |
| 本地存储 | Local Storage |
| 弹性IP | EIP |
| 无域间路由 | CIDR |

## 版本更新

### 1.0

2016\/03\/01第一次正式发布。

### 1.1

2016\/04\/01 主要更新：

1. 新增用户管理

2. 新增多网络管理

3. 更新Windows Virtio驱动安装

4. 修改章节显示方式


### 1.2

2016\/04\/27 主要更新：

1. 初始化界面新增主存储

2. 新增NFS、Ceph、Shared Mount Point等存储类型支持

3. 新增弹性IP

4. 新增云主机缓存模式

5. 新增云主机高可用

6. 修改SSH key注入方式为Amazon AWS方式。

7. 新增控制台代理菜单


### 1.3

2016\/05\/27 主要更新：

1. 初始化界面新增普通用户和SSH指定端口的支持

2. 新增计算规格上行下行网络带宽限制

3. 新增CPU、内存、云盘等计费功能

4. 新增CPU超分

5. 新增云主机操作:更改所有者、指定物理机启动

6. 新增镜像、云盘资源实际占用空间和虚拟占用空间

7. 新增日志收集工具

8. 修改云主机可用与已删除显示列表


### 1.4

2016\/06\/29 主要更新：

1. Java版本从1.7升级到1.8版本

2. 新增性能监控与日志信息

3. 新增FusionStor存储支持

4. 删除本地yum源配置

5. 新增数据库恢复

6. 新增Cassandra数据库备份与恢复

7. 新增ZStack定制版ISO升级yum源

8. 新增在线快照


### 1.5
 
2016\/07\/30 主要更新：

1. 新增镜像仓库

2. 新增删除计费规则功能

3. 支持在线创建镜像

4. 优化性能监控信息

5. 新增日志语言切换

### 1.6

2016/08/31 主要更新：

1. 新增集群功能（[9](/Cluster/cluster-introduction.md)）

2. 新增操作助手（[6.4](/Main/help-box.md)）

3. 新增定时任务功能([7.2](/VM/single-vm.md))

4. 新增云主机克隆功能([7.2](/VM/single-vm.md))

5. 新增设置云主机控制台密码功能([7.2](/VM/single-vm.md))

6. 新增镜像仓库镜像导出功能([10.1](/Image/single-image.md))

7. 已创建云主机支持添加/删除SSH key([7.2](/VM/single-vm.md))

8. 支持为账户分配EIP的配额([18.1](/User-MN/account.md))

9. ceph存储支持指定池名

10. 支持UI界面查看DHCP Server IP

11. 优化Wizard用户体验

12. 优化部分操作顺序

