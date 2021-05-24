# 安装SAS大学版

***

[参考文章](https://www.sas.com/zh_cn/software/university-edition/download-software.html#windows)

## 获取虚拟化软件

首先，在您的计算机上下载并安装虚拟化软件。我们建议您使用适用于 Windows 系统的免费 Oracle VirtualBox。

[网站戳这里](https://www.virtualbox.org/wiki/Downloads)

## 为您的 SAS 文件创建一个文件夹

在等待 VirtualBox 安装时：

1. 在您的本地计算机上创建一个名为 SASUniversityEdition（无空格）的文件夹，并记住这个位置。
2. 然后在 SASUniversityEdition 文件夹中创建一个名为 myfolders（无空格）的子文件夹。这是您保存所有SAS 大学版文件的地方。

***

## 下载 SAS University Edition vApp

1. 单击下方的 获取 SAS 大学版按钮。系统将提示您创建 SAS 个人帐户，或者登录您已创建的帐户。
[下载戳这里](https://support.sas.com/edownload/software/DPUNVE001_VirtualBox)

2. 登录到您的 SAS 个人帐户后，请接受许可协议条款和条件。

3. 在“汇总页”上单击“下载”链接，将开始下载。（如果浏览器提示您保存或运行文件，请选择“保存”，将文件保存在“下载”目录中。）

***

## 将 SAS 大学版导入 VirtualBox

1. 启动 VirtualBox，并选择 File > Import Appliance（文件>导入设备）。
2. 在“Import Virtual Appliance”（导入虚拟设备） 窗口中，单击字段右侧的文件夹图标。
3. 在文件浏览器窗口中，选择 SAS University Edition .ova 文件，然后单击“Open”（打开）。
4. 单击“Next”（下一步），然后在“Appliance Settings”（设备设置）窗口中单击“Import”（导入）。

## 与 VirtualBox 共享您的 myfolders 文件夹

1. 在 VirtualBox 中选择 SAS University Edition vApp，然后选择“Machine > Settings”（机器>设置）。
2. 在导航窗格中，选择“Shared Folders”（共享文件夹），然后单击“Settings”（设置）窗口右上方的“Add Folder”（添加文件夹）图标（+）。
3. 在“Add Share”（添加共享）窗口中，选择“Other”（其他）作为文件夹路径。
4. 在“Select Folder”（选择文件夹）窗口中，打开 SASUniversityEdition 文件夹，然后选择在步骤 1 中创建的 myfolders 子文件夹。单击“Select Folder”（选择文件夹）。
5. 在“Add Share”（添加共享）窗口中，确认未选择“Read-only”（只读）。
6. 选择“Auto-mount”（自动安装）和“Make Permanent”（设为永久）（如可用）选项，然后单击“OK”（确定）。
7. 再次单击“OK”（确定），关闭“Settings”（设置）窗口。

***

## 启动 SAS 大学版

1. 在 VirtualBox 中，选择 SAS University Edition vApp，然后选择“Machine > Start”（机器>开始）。虚拟机可能需要几分钟才能启动。
注意：虚拟机运行时，带有 SAS 徽标的界面将被替换为黑色的控制台界面（即“欢迎”窗口）。您可以最小化此窗口，但是在准备好结束 SAS 会话之前，请不要关闭“欢迎”窗口。

2. 在本地计算机上的 Web 浏览器中，输入 [这个网站](http://localhost:10080)。

3. 在 SAS 大学版：信息中心中，单击“启动 SAS Studio”.

### 一些常见问题

问题描述：
    http访问非80端口时，Firefox提示

        此地址访问受限
        此地址使用了一个通常应该用于其他网页浏览的端口。由于安全原因，Firefox 取消了该请求。

解决方法：
    在Firefox地址栏输入about:config，然后在右键新建一个字符串键：

        network.security.ports.banned.override，

    将需访问网站的端口号添加到，值就是那个端口号即可。
    多个端口要添加的话，就半角逗号隔开，如：807,808,8080

    在能保证安全的前提下，还能简化成这样写 0-65535
    这是没有任务端口限制的，就要看你是否需要了！ 
