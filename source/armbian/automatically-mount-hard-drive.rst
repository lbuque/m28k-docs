.. _automatically-mount-hard-drive:

开机自动挂载硬盘
=================

不同于热插拔的设备，对于硬盘可能需要长期挂载在系统下，所以如果每次开机都去手动mount是非常痛苦的。

fstab
-----

系统开机的时候会读取/etc/fstab这个文件中的内容，根据文件配置情况去挂载磁盘。vi /etc/fstab，打开fstab文件，具体如下图所示；

.. code-block:: shell

    root@mangopi-m28k:~# cat /etc/fstab 
    UUID=2fc3eceb-3b48-4c27-a73d-19d86e1fa23e / ext4 defaults,noatime,commit=600,errors=remount-ro 0 1
    UUID=1abbe161-eb7d-4409-9b1a-ca3c6ccad0a3 /boot ext4 defaults,commit=600,errors=remount-ro 0 2
    tmpfs /tmp tmpfs defaults,nosuid 0 0


参数含义
^^^^^^^^^

这里需要配置6个参数，`<file system>`，`<mount point>`，`<type>`，`<options>`，`<dump>`，`<pass>`；简单解释一下每个参数的含义，不能只见树木不见森林。

- file system

    文件系统，参考默认的`fstab`来看，这里只需要把硬盘的`UUID`正确配置即可；可以通过指令`blkid`，查看硬盘的`UUID`；

- mount point

    挂载路径，最终硬盘会被挂载到配置的这个路径下，但是这个路径必须先存在，提前创建好这个路径即可；

- type

    硬盘的文件系统类型，相应的有`ntfs`，`ext4`，`fat`，`vfat`等等，这里要根据实际情况设置，同样的也可以通过指令`blkid`，查看硬盘的`TYPE`；

- options

============== ============
option         description
-------------- ------------
defaults       use default options: rw, suid, dev, exec, auto, nouser, and async.
-------------- ------------
noauto         do not mount when “mount -a” is given (e.g., at boot time)
-------------- ------------
user           allow a user to mount
-------------- ------------
owner          allow device owner to mount
-------------- ------------
comment or x-  for use by fstab-maintaining programs
-------------- ------------
nofail         do not report errors for this device if it does not exist.
============== ============

- dump

    这个参数用来检查文件系统以多快频率进行备份，系统将认为其值为0，则不需要进行备份；设置成1暂时也没有实践过；

- pass

    这个参数用来决定在启动时需要被`fsck`扫描的文件系统的顺序，根文件系统"/"对应该字段的值应该为1，其他的应该逐渐递增，如果设置为0则表示不扫描。

实现步骤
--------

1. 格式化硬盘

.. code-block:: shell

    mkfs.ext4 /dev/sda1


1. 创建挂载目录

创建硬盘需要挂载的路径，这个路径可以根据自己的需要随意命名；

.. code-block:: shell

    mkdir /media/sda1


3. 查看UUID

.. code-block:: shell

    root@panther-x2:~# blkid /dev/sda1 
    /dev/sda1: UUID="7ff1f142-470c-4cbb-8155-5df4e1d41835" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="869ac3a5-01"


4. 配置/etc/fstab

.. code-block:: shell

    UUID=7ff1f142-470c-4cbb-8155-5df4e1d41835 /media/sda1 ext4 errors=remount-ro 0 0


最后，重启系统，看一下硬盘是不是已经挂载上去了；

.. code-block:: shell

    $ cat /proc/mounts | grep sda1
    $ /dev/sda1 /media/sda1 ext4 rw,relatime,errors=remount-ro,data=ordered 0
