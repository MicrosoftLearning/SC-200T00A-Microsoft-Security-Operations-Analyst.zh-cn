---
lab:
  title: 练习 2 - 使用数据连接器将 Windows 设备连接到 Microsoft Sentinel
  module: Module 6 - Connect logs to Microsoft Sentinel
ms.openlocfilehash: 91e038a226219fbd411855158f1449d92995ff5f
ms.sourcegitcommit: 320cb9d3ce20c75731418e03eb86916841cecc69
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2022
ms.locfileid: "140742095"
---
# <a name="module-6---lab-1---exercise-2---connect-windows-devices-to-microsoft-sentinel-using-data-connectors"></a>模块 6 - 实验室 1 - 练习 2 - 使用数据连接器将 Windows 设备连接到 Microsoft Sentinel

## <a name="lab-scenario"></a>实验室方案

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何连接来自组织中多个数据源的日志数据。 下一个数据源是 Azure 内部和外部的 Windows 虚拟机，例如本地环境或其他公共云。


### <a name="task-1-create-a-windows-virtual-machine-in-azure"></a>任务 1：在 Azure 中创建 Windows 虚拟机

在本任务中，你将在 Azure 中创建 Windows 虚拟机。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 选择“+ 创建资源”。 提示：如果已在 Azure 门户中，则可能需要从顶部栏中选择 Microsoft Azure 以返回主页。

1. 在“搜索服务和市场”框中，输入“Windows 10”并从下拉列表中选择“Microsoft Window 10”。

1. 打开“计划”下拉列表，然后选择“Windows 10 企业版，版本 20H2”。 选择“开始使用预设置配置”以继续。

1. 选择“开发/测试”，然后选择“继续创建 VM” 。

1. 为“资源组”选择“新建”，输入 RG-AZWIN01 作为名称，然后选择“确定”。

    >**注意：** 该资源组将是用于跟踪的新资源组。 

1. 在“虚拟机名称”处输入 AZWIN01。

1. 将“区域”设置为所在地区的相应区域。 相应区域将为默认区域。

1. 向下滚动并查看虚拟机的“大小”。 如果显示为空，请选择“查看所有大小”，然后选择“B2ms”并单击“选择”  。

1. 输入你选择的用户名。 提示：避免使用保留字，如 admin 或 root。

1. 输入你选择的密码。 提示：重新使用你的租户密码可能更简单。 可以在“资源”选项卡中找到它。

1. 向下滚动到页面底部，选中“许可”下面的复选框，以确认你具有符合条件的许可证。

1. 选择“查看 + 创建”，然后等待验证通过。

1. 选择“创建”。 等待创建资源，这可能需要几分钟的时间。


### <a name="task-2-connect-an-azure-windows-virtual-machine"></a>任务 2：连接 Azure Windows 虚拟机

在此任务中，需要将 Azure Windows 虚拟机连接到 Microsoft Sentinel。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在“数据连接器”选项卡中，搜索“通过旧版代理程序的安全事件”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”部分中的“1. 下载并安装代理”下，选择“在 Azure Windows 虚拟机上安装代理”选项。

1. 选择“为 Azure Windows 虚拟机下载和安装代理”。 此时会显示 Azure 订阅中的可用虚拟机。

1. 选择刚才在上一个任务中创建的 AZWIN01 虚拟机，然后选择“连接” 。 等待直到“状态”显示“此工作区”。

1. 选择“x”关闭窗口。 在“配置”部分中的“2. 选择要流式传输的事件”下，选择“所有事件”，然后选择“应用更改” 。


### <a name="task-3-connect-a-non-azure-windows-machine"></a>任务 3：连接非 Azure Windows 计算机

在此任务中，需要将非 Azure Windows 虚拟机连接到 Microsoft Sentinel。

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 查找虚拟机名称引用。

1. 以管理员身份使用密码登录到 WIN2 虚拟机：**Pa55w.rd**。  

1. 打开 Microsoft Edge 浏览器。

1. 打开浏览器，并使用在先前的实验室中使用的凭据登录 Azure 门户 (https://portal.azure.com )。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择 Microsoft Sentinel 工作区。

1. 选择“数据连接器”，然后搜索“通过旧版代理程序的安全事件”连接器，并从列表中选择它 。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”部分中的“1. 下载并安装代理”下，现在，请选择“在非 Azure Windows 计算机上安装代理”选项。

1. 选择“为 Azure Windows 计算机下载和安装代理”。 

    >**注意：** Log Analytics 工作区会显示 2 台 Windows 计算机已连接。 分别对应于之前连接的 WINServer 和 AZWIN01 虚拟机。

1. 选择“下载 Windows 代理(64 位)”的链接。

1. 选择已下载的 MMASetup-AMD64.exe 文件下的“打开文件”，然后选择“是”，以允许可执行文件在显示的“用户帐户控制”窗口中运行。

1. 在欢迎对话框中选择“下一步”，在“Microsoft 软件许可条款”页面上选择“我同意”，然后在目标提示中选择“下一步”，以接受默认路径  。

1. 在“代理安装选项”提示上，选择“将代理连接到 Azure Log Analytics (OMS)”选项，然后选择“下一步”。 

1. 在打开了 Microsoft Sentinel 的浏览器中，从“代理管理”页复制工作区 ID，然后粘贴到对话框的“工作区 ID”中。 

1. 在打开了 Microsoft Sentinel 的浏览器中，从“代理管理”页复制主键，然后粘贴到对话框的“工作区密钥”中。 

1. 选择“下一步”以保存配置。

1. 在“Microsoft 更新”页上选择“下一步”。

1. 然后选择“安装”。 等待 Microsoft Monitoring Agent 安装完成。

1. 完成后，选择“完成”。


### <a name="task-4-install-and-collect-sysmon-logs"></a>任务 4：安装并收集 Sysmon 日志

在此任务中，你将安装并收集 Sysmon 日志。

>**注意：** 以下说明将使用默认配置安装 Sysmon。 应研究基于社区的配置，以便在生产计算机上使用 Sysmon。

1. 在浏览器中打开新选项卡，转到 https://docs.microsoft.com/sysinternals/downloads/sysmon

1. 从页面上选择“下载 Sysmon”以下载 Sysmon。

1. 将鼠标悬停在 Sysmon.zip 上，然后选择文件夹图标。 右键单击下载的文件并选择“全部提取...”；在“文件将被提取到此文件夹”下输入 C:\Sysmon，然后选择“提取” 。 

1. 在适用于 WIN2 的 Windows 任务栏搜索框中，输入“命令”。 搜索结果将显示命令提示符应用。 右键单击命令提示符应用，并选择“以管理员身份运行”。 选择“是”，允许应用在显示的“用户帐户控制”窗口中运行。

1. 键入 cd \sysmon

1. 键入“notepad sysmon.xml”以创建新文件。 选择“是”，以确认文件创建。

1. 在浏览器中打开新选项卡，转到： https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

1. 选择“原始”按钮。 选择全文，然后从 GitHub 复制该文件的内容，并将其粘贴回刚刚创建的 sysmon.xml 记事本文件中。

1. 在记事本中，选择“文件”，然后选择“保存”以保存文件 。

1. 返回命令提示符，键入以下命令，然后按 Enter：sysmon.exe -accepteula -i sysmon.xml

    >**重要提示：** 验证输出中是否出现“已验证配置文件”和“已启动 Sysmon”消息。 如果不是这种情况，请验证数据是否正确复制，以及 sysmon.xml 文件是否已保存。

1. 在浏览器中，导航回打开 Azure 门户的选项卡 (https://portal.azure.com ) 

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel，并选择之前创建的 Microsoft Sentinel 工作区。

1. 在 Microsoft Sentinel 中，从“配置”区域中选择“设置”，然后选择“工作区设置 >”选项卡 。

1. 在“设置”区域中，选择“代理配置”。 默认情况下应选择“Windows 事件日志”选项卡。

1. 选择“+ 添加 Windows 事件日志”按钮。

1. 在“日志名称”字段中键入“Microsoft-Windows-Sysmon/Operational”。

1. 选择“应用”。 这样，我们将可以从事件查看器收集 Sysmon 生成的所有事件。


### <a name="task-5-onboard-microsoft-defender-for-endpoint-device"></a>任务 5：加入 Microsoft Defender for Endpoint 设备

在此任务中，你需要将设备加入 Microsoft Defender for Endpoint。

>重要提示：如果已完成本课程的“模块 2 - 练习 1”实验室，并且到目前为止一直在保存虚拟机，可以跳过此任务。 否则，需要再次将 WIN1 计算机加入 Defender for Endpoint。

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 查找虚拟机名称引用。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 如果当前不在门户中，请通过 Microsoft Edge 浏览器转到 Microsoft 365 Defender 门户 (https://security.microsoft.com) )，并使用租户电子邮件凭据登录。

1. 从左侧菜单栏中选择“设置”，然后从“设置”页面中选择“终结点” 。

1. 在“设备管理”部分选择“加入”。

1. 选择“下载载入包”。

1. 提取下载的 .zip 文件。

1. 以管理员身份运行 Windows 命令提示符，并同意显示的用户帐户控制提示。

1. 运行你刚才以管理员身份提取的 WindowsDefenderATPLocalOnboardingScript.cmd 文件。 **注意：** 默认情况下，该文件应位于 c:\users\admin\downloads 目录中。 对于脚本呈现的问题回答 Y。 

1. 从门户的“加入”页面中，复制检测测试脚本，并在一个打开的命令窗口中运行该脚本。 你可能需要通过在 Windows 搜索栏中键入 **CMD，然后选择“以管理员身份运行”，来打开新的“管理员: 命令提示符”窗口**。

1. 在 Microsoft 365 Defender 门户的“终结点”区域中，选择“设备清单”。 该列表中现在应列出了你的设备。

## <a name="proceed-to-exercise-3"></a>继续完成练习 3
