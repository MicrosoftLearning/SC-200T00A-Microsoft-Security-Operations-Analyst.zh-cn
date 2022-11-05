---
lab:
  title: 练习 2 - 使用数据连接器将 Windows 设备连接到 Microsoft Sentinel
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-2---connect-windows-devices-to-microsoft-sentinel-using-data-connectors"></a>模块 6 - 实验室 1 - 练习 2 - 使用数据连接器将 Windows 设备连接到 Microsoft Sentinel

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何连接来自组织中多个数据源的日志数据。 下一个数据源是 Azure 内部和外部的 Windows 虚拟机，例如本地环境或其他公共云。


### <a name="task-1-create-a-windows-virtual-machine-in-azure"></a>任务 1：在 Azure 中创建 Windows 虚拟机

在本任务中，你将在 Azure 中创建 Windows 虚拟机。

1. 使用密码 Pa55w.rd 以管理员身份登录到 WIN1 虚拟机 。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 选择“+ 创建资源”。 提示：如果已在 Azure 门户中，则可能需要从顶部栏中选择 Microsoft Azure 以返回主页。

1. 在“搜索服务和市场”框中，输入“Windows 10”并从下拉列表中选择“Microsoft Window 10”。

1. 打开“计划”下拉列表，然后选择“Windows 10 企业版，版本 21H2”。 选择“开始使用预设置配置”以继续。

1. 选择“开发/测试”，然后选择“继续创建 VM” 。

1. 为“资源组”选择“新建”，输入 RG-AZWIN01 作为名称，然后选择“确定”。

    >**注意：** 该资源组将是用于跟踪的新资源组。 

1. 在“虚拟机名称”处输入 AZWIN01。

1. 将“区域”的默认值保留为“(US) 美国东部”。

1. 向下滚动并查看虚拟机的“大小”。 如果它显示为空，请选择“查看所有大小”，在“Azure 用户最常用的大小”下选择第一个 VM 大小，然后单击“选择”。

1. 输入你选择的用户名。 提示：避免使用保留字，如 admin 或 root。

1. 输入你选择的密码。 提示：重新使用你的租户密码可能更简单。 可以在“资源”选项卡中找到它。

1. 向下滚动到页面底部，选中“许可”下面的复选框，以确认你具有符合条件的许可证。

1. 选择“查看 + 创建”，然后等待验证通过。

1. 选择“创建”。 等待创建资源，这可能需要几分钟的时间。


### <a name="task-2-connect-an-azure-windows-virtual-machine"></a>任务 2：连接 Azure Windows 虚拟机

在此任务中，需要将 Azure Windows 虚拟机连接到 Microsoft Sentinel。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在“数据连接器”选项卡中，搜索“通过 AMA 的 Windows 安全事件”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”部分，选择“创建数据收集规则”。

1. 为规则名称输入“AZWIN01DCR”，然后选择“下一步:**资源”** 。

1. 选择“+添加资源”。

1. 展开“RG-AZWIN01”，然后选择“AZWIN01” 。

1. 选择“应用”。

1. 依次选择“下一步: 收集”、“下一步: 查看 + 创建” 。

1. 选择“创建” 。

1. 等待几分钟，然后选择“刷新”以查看列出的新数据收集规则。


### <a name="task-3-connect-a-non-azure-windows-machine"></a>任务 3：连接非 Azure Windows 计算机

在此任务中，需要安装 Azure Arc 并将非 Azure Windows 虚拟机连接到 Microsoft Sentinel。  

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 查找虚拟机名称引用。

>**重要提示：** “通过 AMA 的 Windows 安全中心事件”需要针对非 Azure 设备的 Azure Arc。 

1. 使用密码 Pa55w.rd 以管理员身份登录到 WIN2 虚拟机 。  

1. 打开 Microsoft Edge 浏览器。

1. 打开浏览器，并使用在先前的实验室中使用的凭据登录 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Arc”，然后选择“Azure Arc”。

1. 在“基础结构”下的导航窗格中，选择“服务器” 

1. 选择“+ 添加”。

1. 在“添加单个服务器”部分中选择“生成脚本”。

1. 选择“下一步”，转到“资源详细信息”选项卡。

1. 选择之前创建的资源组。 提示：RG-Defender

    >**注意：** 如果尚未创建资源组，请打开另一个选项卡并创建资源组，然后重新开始。

1. 查看“服务器详细信息”和“连接方法”选项 。 保留默认值并选择“下一步”，以转到“标记”选项卡。

1. 选择“下一步”，转到“下载并运行脚本”选项卡。

1. 向下滚动并选择“下载”按钮。 提示：如果浏览器阻止下载，请在浏览器中执行操作以允许下载。 在 Microsoft Edge 浏览器中，根据需要选择省略号按钮 (...)，然后选择“保留”。 

1. 右键单击 Windows 的“开始”按钮，然后选择“Windows PowerShell (管理员)”。

    >注意：可能需要搜索 Windows PowerShell。  在搜索框中，键入“PowerShell”。 此时会显示“Windows PowerShell 应用”。 选择“以管理员身份运行”选项。

1. 如果收到 UAC 提示，请在“用户名”中输入“Administrator”，在“密码”中输入“Passw0rd!” 。 如果未收到，请跳到下一步。

1. 输入：cd C:\Users\Admin\Downloads

1. 键入“Set-ExecutionPolicy -ExecutionPolicy Unrestricted”，然后按 Enter。

1. 输入“A”，表示全部接受，然后按 Enter。

1. 键入“.\OnboardingScript.ps1”，然后按 Enter。  

    >重要提示：如果收到错误“无法识别术语 .\OnboardingScript.ps1...”，请确保是在 WIN2 虚拟机中执行任务 3 的步骤。 其他问题可能是由于多次下载导致文件名称更改，请在运行目录中搜索“.\OnboardingScript (1).ps1”或其他文件编号。

1. 输入 R 以运行一次，然后按 Enter（这可能需要几分钟时间）。

1. 安装过程将打开新的 Edge 浏览器标签页，以对 Azure Arc 代理进行身份验证。 选择管理员帐户，等待消息“身份验证完成”，然后返回到 Windows PowerShell 窗口。

1. 安装完成后，返回到下载脚本的 Azure 门户页面，然后选择“关闭”。 关闭“使用 Azure Arc 添加服务器”，返回到 Azure Arc 服务器页面 。

1. 选择“刷新”，直到 WIN2 名称出现 。

    >**注意：** 这可能需要几分钟时间。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在“数据连接器”选项卡中，搜索“通过 AMA 的 Windows 安全事件”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”部分，选择“创建数据收集规则”。

1. 为规则名称输入“WIN2”，然后选择“下一步:**资源”** 。

1. 选择“+添加资源”。

1. 展开“rg-defender”（或创建的资源组），然后选择“WIN2”。

1. 选择“应用”。

1. 依次选择“下一步: 收集”、“下一步: 查看 + 创建” 。

1. 选择“创建” 。

1. 等待几分钟，然后选择“刷新”以查看列出的新数据收集规则。


### <a name="task-4-onboard-microsoft-defender-for-endpoint-device"></a>任务 4：加入 Microsoft Defender for Endpoint 设备

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
