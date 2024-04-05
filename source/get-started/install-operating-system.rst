安装操作系统
===========

.. include:: ../refs/install-operating-system.ref

准备工作
--------

- 1x microSD 卡(容量 >=8GB)

- 1x microSD 读卡器

- TYPE-C 电源适配器

镜像下载
--------

请到 :ref:`资源下载汇总 <resource-download-summary>` 下载对应的镜像文件

安装系统
--------

Balena Etcher 是一个跨平台且，用户界面友好的镜像文件烧写工具，我们推荐你使用它。 如果你使用 Windows，并且对 Win32DiskImager 或 Rufus 更熟悉，你也可以使用它们。

1. 下载 Etcher 并安装。

|rock5a-step1.webp|

2. 打开 Etcher，单击 `Flash from file` 以选择需要写入的镜像。

|rock5a-step2.webp|

1. 点击 `Select target` 以选择设备，请注意小心选择。

|rock5a-step3.webp|

4. 点击 `Flash!` 开始写入，然后等待写入进度条完成。

|rock5a-step4.webp|

5. 当写入镜像成功时，Etcher 将会显示 `Flash Complete!`。

|rock5a-step5.webp|

**如果刷写操作系统镜像错误, 请手动再试一次。**

启动系统
--------

按照上述步骤成功烧录 microSD 卡后，将 microSD 卡插入 芒果派 M28K 的 MicroSD 插槽内。

芒果派 M28K 的供电接口为 USB Type C port，请使用 Type-C 线缆连接供电口和适配器。
