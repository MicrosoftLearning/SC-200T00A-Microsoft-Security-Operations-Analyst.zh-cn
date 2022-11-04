---
lab:
  title: 练习 1 - 启用 Microsoft Defender for Cloud
  module: Module 3 - Mitigate threats using Microsoft Defender for Cloud
---

# <a name="module-3---lab-1---exercise-1---enable-microsoft-defender-for-cloud"></a>模块 3 - 实验室 1 - 练习 1 - 启用 Microsoft Defender for Cloud

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex1.png)

你是一名安全运营分析师，你所在公司正在使用 Microsoft Defender for Cloud 实现云工作负载保护。  在此实验室中，你将启用 Microsoft Defender for Cloud。


### <a name="task-1-access-the-azure-portal-and-set-up-a-subscription"></a>任务 1：访问 Azure 门户，然后设置订阅

在此任务中，你将设置完成本实验室和以后的实验室所需的 Azure 订阅。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 打开 Microsoft Edge 浏览器，如果已打开浏览器，则打开新选项卡。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com) )。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

1. 在 Azure 门户的搜索栏中，键入“订阅”，然后选择“订阅”。 

1. 如果显示“Azure Pass - 赞助”订阅（或所选语言的等效名称），请继续执行任务 #2。 否则，请向讲师咨询如何创建包含租户管理员用户凭据的 Azure 订阅。 **注意：** 订阅创建过程可能需要长达 10 分钟的时间。 

    >**重要提示：** 这些实验室已设计为在上课期间使用低于 10 美元的 Azure 服务。


### <a name="task-2-create-a-log-analytics-workspace"></a>任务 2：创建 Log Analytics 工作区

在此任务中，你将创建一个 Log Analytics 工作区，以与 Microsoft Defender for Cloud 配合使用。

1. 在 Azure 门户的搜索栏中，键入“Log Analytics 工作区”，然后选择相同的服务名称。

1. 从命令栏中选择“+ 创建”。

1. 为资源组选择“新建”。

1. 输入 RG-Defender，然后选择“确定”。

1. 对于“名称”，请输入唯一的名称，例如：uniquenameDefender。

1. 选择“查看 + 创建”  。

1. 工作区验证通过后，选择“创建”。 等待新工作区进行预配，这可能需要几分钟时间。


### <a name="task-3-enable-microsoft-defender-for-cloud"></a>任务 3：启用 Microsoft Defender for Cloud

在此任务中，你将启用和配置 Microsoft Defender for Cloud。

1. 在 Azure 门户的搜索栏中，输入 Defender，然后选择“Microsoft Defender for Cloud”。

1. 在“开始”页面的“升级”选项卡下，确保订阅已选中，然后选择页面底部的“升级”按钮  。 等待显示“试用已启动”通知，大约需要 2 分钟。 提示：可以单击顶部栏中的铃声按钮，查看 Azure 门户通知。

1. 在 Microsoft Defender for Cloud 的左侧菜单中的“管理”下，选择“环境设置”。

1. 选择“Azure Pass - 赞助”订阅（或所选语言的等效名称）。 

1. 查看现在受 Defender for Cloud 计划保护的 Azure 资源。

1. 从“设置”区域中选择“自动设置”。

1. 查看自动设置 - 扩展。 确认“Log Analytics 代理/Azure Monitor 代理”为“关闭” 。

1. 选择页面右上角的“x”关闭设置页面，再次返回“环境设置”，然后选择订阅左侧的“>”。

1. 选择之前创建的 Log Analytics 工作区“uniquenameDefender”，查看可用选项和定价。 

1. 选择“启用所有 Microsoft Defender for Cloud 计划”，然后选择“保存” 。 等待显示“已成功保存工作区 uniquenameDefender 的 Microsoft Defender 计划！” 通知。

    >**注意：** 如果页面未显示，请刷新 Microsoft Edge 浏览器，然后重试。


### <a name="task-4-install-azure-arc-on-an-on-premises-server"></a>任务 4：在本地服务器上安装 Azure Arc

在此任务中，你将在本地服务器上安装 Azure Arc，以便更轻松地加入。

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 查找虚拟机名称引用。

1. 使用以下密码以管理员身份登录到 WINServer 虚拟机：Passw0rd!  （如果需要）。  

1. 打开 Microsoft Edge 浏览器并导航到 Azure 门户 (https://portal.azure.com )。

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

1. 在“用户名”中输入“Administrator”，在“密码”中输入“Passw0rd!”  （如果收到 UAC 提示）。

1. 输入：cd C:\Users\Administrator\Downloads

    >重要提示：如果没有此目录，最有可能意味着你使用的是错误的计算机。 返回任务 4 的开头，更改为 WINServer 并重新启动。

1. 键入“Set-ExecutionPolicy -ExecutionPolicy Unrestricted”，然后按 Enter。

1. 输入“A”，表示全部接受，然后按 Enter。

1. 键入“.\OnboardingScript.ps1”，然后按 Enter。  

    >**重要提示：** 如果收到错误“无法识别术语 .\OnboardingScript.ps1...”，请确保是在 WINServer 虚拟机中执行任务 4 的步骤。 其他问题可能是由于多次下载导致文件名称更改，请在运行目录中搜索“.\OnboardingScript (1).ps1”或其他文件编号。

1. 输入 R 以运行一次，然后按 Enter（这可能需要几分钟时间）。

1. 安装过程将打开新的 Edge 浏览器标签页，以对 Azure Arc 代理进行身份验证。 选择管理员帐户，等待消息“身份验证完成”，然后返回到 Windows PowerShell 窗口。

1. 安装完成后，返回到下载脚本的 Azure 门户页面，然后选择“关闭”。 关闭“使用 Azure Arc 添加服务器”，返回到 Azure Arc 服务器页面 。

1. 选择“刷新”，直到显示 WINServer 服务器名称，且状态为“已连接”。

    >注意：这可能需要几分钟。

### <a name="task-5-protect-an-on-premises-server"></a>任务 5：保护本地服务器

在此任务中，你将在 WINServer 虚拟机上手动安装所需代理。

1. 转到“Microsoft Defender for Cloud”，然后选择“入门”页面 。

1. 选择“入门”选项卡。

1. 向下滚动并选择“添加非 Azure 服务器”部分下的“配置”。

1. 选择之前创建的工作区旁边的“升级”。 可能需要几分钟，请等待，直到看到通知“工作区 uniquenameDefender 的 Azure Defender 计划已成功保存！”。

1. 选择之前创建的工作区旁边的“+ 添加服务器”。

1. 选择“Log Analytics 代理说明”。

1. 选择“下载 Windows 代理(64 位)”。

1. 选择“打开文件”，运行下载的 MMASetup-AMD64.exe 文件。

1. 选择“下一步”，直到显示“代理安装选项”向导页，选择“将代理连接到 Azure Log Analytics (OMS)”，然后选择“下一步”   。

1. 从 Azure 门户的“工作区密钥”文本框中，将“工作区 ID”和“主键”值复制并粘贴到相应的向导页面字段中，然后选择“下一步”   。

1. 继续安装。 完成后选择“完成”。

1. 转到“Microsoft Defender for Cloud”门户并选择“清单”。

1. 5 分多钟后将显示 WINServer 虚拟机。 可能需要选择“刷新”才能看到。 提示：如果在“资源总数”下看到数字 1，请删除筛选器，以显示 WINServer 虚拟机 。

1. 可以继续下一个实验室，稍后再返回查看 Microsoft Defender for Cloud 的“清单”部分 。

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
