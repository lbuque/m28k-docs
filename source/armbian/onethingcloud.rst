网心云【容器魔方】
==================

.. include:: ../refs/armbian.onethingcloud.ref

环境要求
--------

网络要求
^^^^^^^^^^^^^

a. (pppoe拨号或者静态公网IP的可以忽略跳过)局域网网络的环境,必须要支持dhcp自动获取IP,容器魔
方会从路由器申请多个IP(MAC地址前缀是c0:e7:3e),请不要禁用这些IP,并开启upnp,DMZ只能映射到其中一个申请的IP。

b. 挂有旁路由的设备,请将容器魔方申请的IP网关指向主路由,减少旁路由的影响,提高跑量。

c. 容器魔方仅支持docker的host(推荐)和macvlan网络模式。


磁盘要求
^^^^^^^^^

a. 分配最小磁盘空间>50G,分配的空间越大越有助于提升跑量,可参考容器魔方的配置推荐。

b. 容器魔方会尽量使用完挂载的分区，建议同一块分区上不要存放其他数据。

c. 容器魔方不会主动格式化磁盘,使用前请自行格式化,推荐ext4、xfs、btrfs等主流文件系统,不支持裸盘、vfat、exfat、ntfs。

d. app显示磁盘空间比物理磁盘空间小时,请检查文件系统是否有设置预留空间。


安装docker
-----------

请参考 :ref:`Docker 安装 <docker-installation>`

切换root用户
^^^^^^^^^^^^

安装需要在root用户下进行，切换root用户命令如下：

.. code-block:: shell

    su root


挂载硬盘
^^^^^^^^^

请参考 :ref:`开机自动挂载硬盘 <automatically-mount-hard-drive>`

运行docker容器
^^^^^^^^^^^^^^^

运行容器命令：

.. code-block:: shell

    docker run \
    --name=wxedge \
    --restart=always \
    --privileged \
    --net=host \
    --tmpfs /run \
    --tmpfs /tmp \
    -v /media/wxedge_storage:/storage:rw \
    -d \
    registry.hub.docker.com/onething1/wxedge


docker升级命令：

    .. note::

        首次安装不需要执行此命令

.. code-block:: shell

    docker stop wxedge
    docker rm wxedge
    docker rmi registry.hub.docker.com/onething1/wxedge

    docker run \
    --name=wxedge \
    --restart=always \
    --privileged \
    --net=host \
    --tmpfs /run \
    --tmpfs /tmp \
    -v /media/wxedge_storage:/storage:rw \
    -d \
    registry.hub.docker.com/onething1/wxedge

换盘迁移：

容器启动成功后，会在挂载目录/media/wxedge_storage生成一个wxnode的文件，该文件是设备的唯一标识与账号绑定，请务必做好备份，换盘或者更换挂载目录时，要将wxnode迁移至新的挂载目录下。

其他操作：

- 换盘操作（挂载目录/media/wxedge_storage不变）：

    .. code-block:: shell

        docker  restart  wxedge

- 换盘操作（挂载目录/media/wxedge_storage改变）：

    1. 停止容器 docker   stop   wxedge
    2. 删除容器 docker  rm  wxedge
    3. 重新执行运行容器命令


绑定设备
---------

设备初始化
^^^^^^^^^^^^^^

打开浏览器（推荐谷歌浏览器），输入局域网ip:18888（ip可以通过路由器管理终端页面查看到M28K的ip），比如192.168.10.179:18888（一般30秒内都能初始化成功，失败即点击“重试”按钮，多次失败请反馈错误码联系客服反馈）。
初始化成功后，就会自动进入下图的设置页面：

|设置页面.png|

绑定设备
^^^^^^^^^^^^^^

将设备绑定到网心云APP，可时时看收益，周周提现金。

1. 下载APP：扫描下方二维码，下载网心云APP;
2. 绑定设备： 打开网心云APP【右上角“+”-扫一扫】，扫描下方二维码，即可将设备绑定到网心云APP。

注意：设备绑定后才会计算收益哦！请一定要绑定设备！

|二维码.png|

至此，绑定成功，可通过网心云APP时时看收益，周周提现金。