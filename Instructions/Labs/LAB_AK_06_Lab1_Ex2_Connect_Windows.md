---
lab:
  title: 练习 2 - 使用数据连接器将 Windows 设备连接到 Microsoft Sentinel
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-2---connect-windows-devices-to-microsoft-sentinel-using-data-connectors"></a>模块 6 - 实验室 1 - 练习 2 - 使用数据连接器将 Windows 设备连接到 Microsoft Sentinel

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data are Windows virtual machines inside and outside of Azure, like On-Premises environments or other Public Clouds.


### <a name="task-1-create-a-windows-virtual-machine-in-azure"></a>任务 1：在 Azure 中创建 Windows 虚拟机

在本任务中，你将在 Azure 中创建 Windows 虚拟机。

1. 使用密码 Pa55w.rd 以管理员身份登录到 WIN1 虚拟机 。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. Select <bpt id="p1">**</bpt>+ Create a Resource<ept id="p1">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you were already in the Azure Portal, you might need to select <bpt id="p2">*</bpt>Microsoft Azure<ept id="p2">*</ept> from the top bar to go Home.

1. 在“搜索服务和市场”框中，输入“Windows 10”并从下拉列表中选择“Microsoft Window 10”。

1. Open the <bpt id="p1">*</bpt>Plan<ept id="p1">*</ept> drop-down list and select <bpt id="p2">**</bpt>Windows 10 Enterprise, version 21H2<ept id="p2">**</ept>. Select <bpt id="p1">**</bpt>Start with a pre-set configuration<ept id="p1">**</ept> to continue.

1. 选择“开发/测试”，然后选择“继续创建 VM” 。

1. 为“资源组”选择“新建”，输入 RG-AZWIN01 作为名称，然后选择“确定”。

    >**注意：** 该资源组将是用于跟踪的新资源组。 

1. 在“虚拟机名称”处输入 AZWIN01。

1. 将“区域”的默认值保留为“(US) 美国东部”。

1. Scroll down and review the <bpt id="p1">*</bpt>Size<ept id="p1">*</ept> for the virtual machine. If it appears empty, select <bpt id="p1">**</bpt>See all sizes<ept id="p1">**</ept>, choose one of the VM sizes under <bpt id="p2">*</bpt>Most used by Azure users<ept id="p2">*</ept> and click <bpt id="p3">**</bpt>Select<ept id="p3">**</ept>.

1. Enter a <bpt id="p1">*</bpt>Username<ept id="p1">*</ept> of your choosing. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> Avoid reserved words like admin or root.

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 向下滚动到页面底部，选中“许可”下面的复选框，以确认你具有符合条件的许可证。

1. 选择“查看 + 创建”，然后等待验证通过。

1. 你需要了解如何连接来自组织中多个数据源的日志数据。


### <a name="task-2-connect-an-azure-windows-virtual-machine"></a>任务 2：连接 Azure Windows 虚拟机

在此任务中，需要将 Azure Windows 虚拟机连接到 Microsoft Sentinel。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在“数据连接器”选项卡中，搜索“通过 AMA 的 Windows 安全事件”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”部分，选择“创建数据收集规则”。
1. 为规则名称输入“AZWIN01DCR”，然后选择“下一步:**资源”** 。
1. 选择“+添加资源”
1. 展开“rg-azwin01”，然后选择“AZWIN01”。
1. 选择“应用”。
1. 选择“下一页:**收集”，然后选择“下一步:** **审阅并创建”**
1. 选择“创建”
1. 等待几分钟，然后选择“刷新”以查看列出的新数据收集规则。


### <a name="task-3-connect-a-non-azure-windows-machine"></a>任务 3：连接非 Azure Windows 计算机

在此任务中，需要安装 Azure Arc 并将非 Azure Windows 虚拟机连接到 Microsoft Sentinel。  

>下一个数据源是 Azure 内部和外部的 Windows 虚拟机，例如本地环境或其他公共云。

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

1. Select the Resource group you created earlier. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> <bpt id="p2">*</bpt>RG-Defender<ept id="p2">*</ept>

    >**注意：** 如果尚未创建资源组，请打开另一个选项卡并创建资源组，然后重新开始。

1. Review the <bpt id="p1">*</bpt>Server details<ept id="p1">*</ept> and <bpt id="p2">*</bpt>Connectivity method<ept id="p2">*</ept> options. Keep the default values and select <bpt id="p1">**</bpt>Next<ept id="p1">**</ept> to get to the Tags tab.

1. 选择“下一步”，转到“下载并运行脚本”选项卡。

1. 如果有“注册”选项，则选择以下位置中的“注册”，步骤 1.*选择“注册”* 。

    >**注意：** 等待处理完成，至少需要三 (3) 分钟。

1. Scroll down and select the <bpt id="p1">**</bpt>Download<ept id="p1">**</ept> button. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select <bpt id="p1">**</bpt>Keep<ept id="p1">**</ept>. 

1. 右键单击 Windows 的“开始”按钮，然后选择“Windows PowerShell (管理员)”。

1. In case you get a UAC prompt, enter <bpt id="p1">*</bpt>Administrator<ept id="p1">*</ept> for "Username" and <bpt id="p2">*</bpt>Passw0rd!<ept id="p2">*</ept> for "Password", else skip to next step.

1. 输入：cd C:\Users\Admin\Downloads

1. 键入“Set-ExecutionPolicy -ExecutionPolicy Unrestricted”，然后按 Enter。

1. 输入“A”，表示全部接受，然后按 Enter。

1. 键入“.\OnboardingScript.ps1”，然后按 Enter。  

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you get the error <bpt id="p2">*</bpt>"The term .\OnboardingScript.ps1 is not recognized..."<ept id="p2">*</ept>, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for <bpt id="p1">*</bpt>".\OnboardingScript (1).ps1"<ept id="p1">*</ept> or other file numbers in the running directory.

1. 输入 R 以运行一次，然后按 Enter（这可能需要几分钟时间）。

1. 返回到 Microsoft Edge 浏览器，打开一个新选项卡，并在地址栏中输入 https://microsoft.com/devicelogin 。

1. 返回到 Windows PowerShell 窗口，复制在脚本最后一行“...enter the code”之后显示的代码，以对代理进行身份验证。

1. Go back to the Edge browser and paste it in the <bpt id="p1">**</bpt>Code<ept id="p1">**</ept> box and select <bpt id="p2">**</bpt>Next<ept id="p2">**</ept>. Select your tenant admin account and select <bpt id="p1">**</bpt>Continue<ept id="p1">**</ept> in the <bpt id="p2">*</bpt>Are you trying to sign in to Azure Connected Machine Agent?<ept id="p2">*</ept> window. 

1. Go back to the Windows PowerShell window and wait for the message <bpt id="p1">*</bpt>"Successfully Onboarded Resource to Azure"<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you see a message line with a new authentication code, you need to repeat the last 3 steps again.

1. 选择“+ 创建资源”。

1. 选择“刷新”，直到 WIN2 名称出现 。

    >**注意：** 这可能需要几分钟时间。



1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在“数据连接器”选项卡中，搜索“通过 AMA 的 Windows 安全事件”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”部分，选择“创建数据收集规则”。
1. 为规则名称输入“WIN2”，然后选择“下一步:**资源”** 。
1. 选择“+添加资源”
1. 展开“rg-defender”（或创建的资源组），然后选择“WIN2”。
1. 选择“应用”。
1. 选择“下一页:**收集”，然后选择“下一步:** **审阅并创建”**
1. 选择“创建”
1. 等待几分钟，然后选择“刷新”以查看列出的新数据收集规则。



### <a name="task-4-onboard-microsoft-defender-for-endpoint-device"></a>任务 4：加入 Microsoft Defender for Endpoint 设备

在此任务中，你需要将设备加入 Microsoft Defender for Endpoint。

>提示：如果已在 Azure 门户中，则可能需要从顶部栏中选择 Microsoft Azure 以返回主页。

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 如果当前不在门户中，请通过 Microsoft Edge 浏览器转到 Microsoft 365 Defender 门户 (https://security.microsoft.com) )，并使用租户电子邮件凭据登录。

1. 从左侧菜单栏中选择“设置”，然后从“设置”页面中选择“终结点” 。

1. 在“设备管理”部分选择“加入”。

1. 选择“下载载入包”。

1. 提取下载的 .zip 文件。

1. 以管理员身份运行 Windows 命令提示符，并同意显示的用户帐户控制提示。

1. Run the WindowsDefenderATPLocalOnboardingScript.cmd file that you just extracted as administrator. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> By default the file should be in the c:\users\admin\downloads directory. Answer Y to questions presented by the script. 

1. 打开“计划”下拉列表，然后选择“Windows 10 企业版，版本 21H2”。

1. 选择“开始使用预设置配置”以继续。

## <a name="proceed-to-exercise-3"></a>继续完成练习 3
