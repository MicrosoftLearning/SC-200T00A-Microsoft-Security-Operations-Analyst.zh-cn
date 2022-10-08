---
lab:
  title: 练习 3 - 使用数据连接器将 Linux 主机连接到 Microsoft Sentinel
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-3---connect-linux-hosts-to-microsoft-sentinel-using-data-connectors"></a>模块 6 - 实验室 1 - 练习 3 - 使用数据连接器将 Linux 主机连接到 Microsoft Sentinel

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex3.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data are Linux virtual machines using the Common Event Formatting (CEF) and Syslog connectors.


><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> There are steps within the next Tasks that are done in different virtual machines. Look for the Virtual Machine name references.

### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>任务 1：访问 Microsoft Sentinel 工作区

在此任务中，你将访问 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 启动 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择你在之前的实验室中创建的 Microsoft Sentinel 工作区。


### <a name="task-2-connect-a-linux-host-using-the-common-event-format-connector"></a>任务 2：使用通用事件格式连接器连接 Linux 主机

在此任务中，你将通过通用事件格式 (CEF) 连接器将 Linux 主机连接到 Microsoft Sentinel。

1. Select <bpt id="p1">**</bpt>Data connectors<ept id="p1">**</ept> from the Configuration area in Microsoft Sentinel. From the Data Connectors tab, search for the <bpt id="p1">**</bpt>Common Event Format (CEF)<ept id="p1">**</ept> connector and select it from the list.

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”下，将“1.2 在 Linux 计算机上安装 CEF 收集器”中显示的命令复制到剪贴板 。

1. Launch your <bpt id="p1">**</bpt>LIN1<ept id="p1">**</ept> virtual machine. Login with the username and password provided by your lab hoster. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might need to press the Enter key to see the login prompt. 

1. Note the IP address for your LIN1 server. See the screenshot below as an example:

    ![linux 登录](../Media/LinuxLoginExample.png)

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 输入以下 PowerShell 命令，根据你的具体 Linux 服务器信息进行调整，然后按 Enter：

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. 你需要了解如何连接来自组织中多个数据源的日志数据。

    ![linux 登录](../Media/PSconnectLinux.png)

1. 下一个数据源是使用通用事件格式化 (CEF) 和 Syslog 连接器的 Linux 虚拟机。 

1. 粘贴后，在按 Enter 键之前，将字符 3 添加到单词 python，如下所示：

    ![连接器脚本](../Media/ConnectorScript.png)


1. Once the script is adjusted press Enter. The script will run against your Linux server remotely. When the script processes properly it should look like this screen:

    ![连接器脚本](../Media/LinuxConnected.png)

1. 键入“exit”以关闭与 LIN1 的远程 Shell 连接。


### <a name="task-3-connect-a-linux-host-using-the-syslog-connector"></a>任务 3：使用 Syslog 连接器连接 Linux 主机

在此任务中，你将通过 Syslog 连接器将 Linux 主机连接到 Microsoft Sentinel。

1. 返回到打开 Microsoft Sentinel 门户的 Microsoft Edge 浏览器，并通过选择右上角的“x”关闭“通用事件格式 (CEF)”数据连接器页。 

1. 在“数据连接器”选项卡中，搜索“Syslog”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”下，打开“在非 Azure Linux 计算机上安装代理”部分。

1. 选择“为非 Azure Linux 计算机下载和安装代理”的链接。 

    >**重要提示：** 下一个任务中有一些步骤是在不同的虚拟机中完成的。

1. 选择“Linux 服务器”的选项卡。

    >查找虚拟机名称引用。

1. 将“下载和加入适用于 Linux 的代理”区域中的命令复制到剪贴板。

1. Launch your LIN2 virtual machine. Login with the username as password provided by your lab hoster. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might need to press the Enter key to see the login prompt.

1. Note the IP address for your LIN2 server. See the screenshot below as an example:

    ![linux 登录](../Media/LinuxLoginExample.png)

1. Go back to the <bpt id="p1">**</bpt>WIN1<ept id="p1">**</ept> virtual machine. Select the Windows PowerShell used in the previous task.

1. 输入以下 PowerShell 命令，根据你的具体 Linux 服务器信息进行调整，然后按 Enter：

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. Enter <bpt id="p1">*</bpt>yes<ept id="p1">*</ept> to confirm the connection and then type the user's password and press enter. Your screen should look something like this:

    ![linux 登录](../Media/PSconnectLinux.png)

1. You are now ready to paste the <bpt id="p1">*</bpt>Download and onboard agent for Linux<ept id="p1">*</ept> command from the earlier step. Make sure that script is in the clipboard. In PowerShell right-click the top bar and choose <bpt id="p1">**</bpt>Edit<ept id="p1">**</ept> and then <bpt id="p2">**</bpt>Paste<ept id="p2">**</ept>.

1. Once the script is pasted, press Enter. The script will run against your Linux server remotely. Wait

1. 完成后，键入“exit”以关闭与 LIN2 的远程 Shell 连接。


### <a name="task-4-configure-the-facilities-you-want-to-collect-and-their-severities-for-the-syslog-connector"></a>任务 4：为 Syslog 连接器配置你想收集的设备及其严重性

在此任务中，你将配置 Syslog 收集设备。

1. 返回到打开 Microsoft Sentinel 门户的 Microsoft Edge 浏览器，并通过选择两次右上角的“x”关闭“Log Analytics 工作区”页和“Syslog”数据连接器页。

1. 在 Microsoft Sentinel 门户中，选择“配置”下的“设置”，然后选择“工作区设置”选项卡。

1. 选择“设置”区域下的“旧代理管理” 。

1. 选择“Syslog”选项卡。

1. 选择“+ 添加设备”按钮。

1. 从“设备名称”下拉菜单中选择“auth”。

1. 再次选择“+ 添加设备”按钮。

1. 从“设备名称”下拉菜单中选择“authpriv”。

1. 选择“应用”以保存所做的更改。

## <a name="proceed-to-exercise-4"></a>继续完成练习 4
