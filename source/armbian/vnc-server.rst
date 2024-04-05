VNC Server
==========

Installing VNC
--------------

.. code-block:: shell

    apt install tigervnc-standalone-server


Configuring the VNC Server
--------------------------

如果你希望用某个用户比如 demo登录，就用su切换到这个用户。

如果想用root登录就直接使用root账号进行操作。

.. code-block:: shell

    # su - demo
    demo@demoserver:~$ vncpasswd
    Password:
    Verify:
    Would you like to enter a view-only password (y/n)? n
    A view-only password is not used


Starting the VNC Server
-----------------------

.. code-block:: shell

    vncserver


即可启动vnc server ,但是连不上，因为只监听了127.0.0.1，所以需要以下命令

.. code-block:: shell

    vncserver -localhost no


查看全部的vnc会话

.. code-block:: shell

    $ vncserver -list
    TigerVNC server sessions:

    X DISPLAY #	PROCESS ID
    :1		1607
    :2		4726

关闭某个会话可以用下面的命令

.. code-block:: shell

    vncserver -kill :1


客户端选择
-----------

- https://www.realvnc.com/en/connect/download/viewer/windows/

- https://vnc-viewer.en.softonic.com/

具体使用不讲了，默认端口是5901
