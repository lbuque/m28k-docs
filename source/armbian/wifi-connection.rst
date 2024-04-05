Wi-Fi连接
==========

nmcli
-------

`nmcli` 是一个命令行工具，用于控制 NetworkManager；还可以用来显示网络设备状态；创建、编辑、开启/关闭和删除网络连接 。Armbian 系统默认自带 `nmcli`， 这里不介绍安装方法。

通过 `nmcli` 直接连上 WIFI 后，系统会记录已保存的 AP。下面是具体的连接方法：

1. 查看设备状态：

    .. code-block:: shell

        nmcli device status


2. 检查 radio

    .. code-block:: shell

        nmcli radio


3. 查看附近无线网络信号：

    .. code-block:: shell

        nmcli dev wifi list


第5列表示信号情况，信号越好的 AP，会越靠前。

4. 连上 AP 热点：

    1. 如果是无密码的 WIFI， 执行以下连接命令，SSID 就是我们所说的 WIFI 名:

        .. code-block:: shell

            nmcli device wifi connect <SSID/BSSID>


    2. 加密的 AP, 使用以下命令：

        .. code-block:: shell

            nmcli device wifi connect <SSID/BSSID> password <password>


执行命令没有报错后，再 Ping 下百度是否可达，能 Ping 通就表明已经连上 AP，可以正常上网。
