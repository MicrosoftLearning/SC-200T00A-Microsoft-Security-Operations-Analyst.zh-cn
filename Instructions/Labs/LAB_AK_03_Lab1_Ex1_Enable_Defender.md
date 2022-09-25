---
lab:
  title: 练习 1 - 启用 Microsoft Defender for Cloud
  module: Module 3 - Mitigate threats using Microsoft Defender for Cloud
---

# <a name="module-3---lab-1---exercise-1---enable-microsoft-defender-for-cloud"></a>模块 3 - 实验室 1 - 练习 1 - 启用 Microsoft Defender for Cloud

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing cloud workload protection with Microsoft Defender for Cloud.  In this lab you will enable Microsoft Defender for Cloud.


### <a name="task-1-access-the-azure-portal-and-set-up-a-subscription"></a>任务 1：访问 Azure 门户，然后设置订阅

在此任务中，你将设置完成本实验室和以后的实验室所需的 Azure 订阅。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 打开 Microsoft Edge 浏览器，如果已打开浏览器，则打开新选项卡。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com) )。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

1. 在 Azure 门户的搜索栏中，键入“订阅”，然后选择“订阅”。 

1. If the <bpt id="p1">*</bpt>"Azure Pass - Sponsorship"<ept id="p1">*</ept> subscription is shown (or equivalent name in your selected language), proceed to Task #2. Otherwise, ask your instructor on how to create the Azure subscription with your tenant admin user credentials. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The subscription creation process could take up to 10 minutes. 

    >**重要提示：** 这些实验室已设计为在上课期间使用低于 10 美元的 Azure 服务。


### <a name="task-2-create-a-log-analytics-workspace"></a>任务 2：创建 Log Analytics 工作区

在此任务中，你将创建一个 Log Analytics 工作区，以与 Microsoft Defender for Cloud 配合使用。

1. 在 Azure 门户的搜索栏中，键入“Log Analytics 工作区”，然后选择相同的服务名称。

1. 从命令栏中选择“+ 创建”。

1. 为资源组选择“新建”。

1. 输入 RG-Defender，然后选择“确定”。

1. 对于“名称”，请输入唯一的名称，例如：uniquenameDefender。

1. 选择“查看 + 创建”  。

1. Once the workspace validation has passed, select <bpt id="p1">**</bpt>Create<ept id="p1">**</ept>. Wait for the new workspace to be provisioned, this may take a few minutes.


### <a name="task-3-enable-microsoft-defender-for-cloud"></a>任务 3：启用 Microsoft Defender for Cloud

在此任务中，你将启用和配置 Microsoft Defender for Cloud。

1. 在 Azure 门户的搜索栏中，输入 Defender，然后选择“Microsoft Defender for Cloud”。

1. On the <bpt id="p1">**</bpt>Getting started<ept id="p1">**</ept> page, under the <bpt id="p2">**</bpt>Upgrade<ept id="p2">**</ept> tab, make sure your subscription is selected, and then select the <bpt id="p3">**</bpt>Upgrade<ept id="p3">**</ept> button at the bottom of the page. Wait for the <bpt id="p1">*</bpt>Trial started<ept id="p1">*</ept> notification to appear, it takes about 2 minutes. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You can click the bell button on the top bar to review your Azure portal notifications.

1. The next page shows the option to install the agent on virtual machines already in the subscription. Select <bpt id="p1">**</bpt>Continue without installing agents<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Do nothing here<ept id="p2">**</ept>.

1. 在门户菜单的管理区域下，选择“环境设置”。

1. 选择“Azure Pass - 赞助”订阅（或所选语言的等效名称）。 

1. 查看在“启用所有 Microsoft Defender for Cloud 计划”下启用的功能，以及在“Microsoft Defender for”列下受保护的 Azure 资源 。

1. 从“设置”区域中选择“自动设置”。

1. 你是一名安全运营分析师，你所在公司正在使用 Microsoft Defender for Cloud 实现云工作负载保护。

1. 选择页面右上角的“x”关闭设置页面，再次返回“环境设置”，然后选择订阅左侧的“>”。

1. 在此实验室中，你将启用 Microsoft Defender for Cloud。

    >**注意：** 如果页面未显示，请刷新 Microsoft Edge 浏览器，然后重试。


### <a name="task-4-install-azure-arc-on-an-on-premises-server"></a>任务 4：在本地服务器上安装 Azure Arc

在此任务中，你将在本地服务器上安装 Azure Arc，以便更轻松地加入。

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. Log in to <bpt id="p1">**</bpt>WINServer<ept id="p1">**</ept> virtual machine as Administrator with the password: <bpt id="p2">**</bpt>Passw0rd!<ept id="p2">**</ept> if required.  

1. 打开 Microsoft Edge 浏览器并导航到 Azure 门户 (https://portal.azure.com )。

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

1. 在“1. 注册订阅”步骤下 *，选择“注册”* 。

    >**注意：** 等待处理完成，至少需要三 (3) 分钟。

1. Scroll down and select the <bpt id="p1">**</bpt>Download<ept id="p1">**</ept> button. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select <bpt id="p1">**</bpt>Keep<ept id="p1">**</ept>. 

1. 右键单击 Windows 的“开始”按钮，然后选择“Windows PowerShell (管理员)”。

1. Enter <bpt id="p1">*</bpt>Administrator<ept id="p1">*</ept> for "Username" and <bpt id="p2">*</bpt>Passw0rd!<ept id="p2">*</ept> for "Password" if you get a UAC prompt.

1. 输入：cd C:\Users\Administrator\Downloads

1. 键入“Set-ExecutionPolicy -ExecutionPolicy Unrestricted”，然后按 Enter。

1. 输入“A”，表示全部接受，然后按 Enter。

1. 键入“.\OnboardingScript.ps1”，然后按 Enter。  

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you get the error <bpt id="p2">*</bpt>"The term .\OnboardingScript.ps1 is not recognized..."<ept id="p2">*</ept>, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for <bpt id="p1">*</bpt>".\OnboardingScript (1).ps1"<ept id="p1">*</ept> or other file numbers in the running directory.

1. 输入 R 以运行一次，然后按 Enter（这可能需要几分钟时间）。

1. 返回到 Microsoft Edge 浏览器，打开一个新选项卡，并在地址栏中输入 https://microsoft.com/devicelogin 。

1. 返回到 Windows PowerShell 窗口，复制在脚本最后一行“...enter the code”之后显示的代码，以对代理进行身份验证。

1. Go back to the Edge browser and paste it in the <bpt id="p1">**</bpt>Code<ept id="p1">**</ept> box and select <bpt id="p2">**</bpt>Next<ept id="p2">**</ept>. Select your tenant admin account and select <bpt id="p1">**</bpt>Continue<ept id="p1">**</ept> in the <bpt id="p2">*</bpt>Are you trying to sign in to Azure Connected Machine Agent?<ept id="p2">*</ept> window. 

1. Go back to the Windows PowerShell window and wait for the message <bpt id="p1">*</bpt>"Successfully Onboarded Resource to Azure"<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you see a message line with a new authentication code, you need to repeat the last 3 steps again.

1. 如果显示“Azure Pass - 赞助”订阅（或所选语言的等效名称），请继续执行任务 #2。

1. 选择“刷新”，直到显示 WINServer 服务器名称。

    >**注意：** 这可能需要几分钟时间。


### <a name="task-5-protect-an-on-premises-server"></a>任务 5：保护本地服务器

在此任务中，你将在 WINServer 虚拟机上手动安装所需代理。

1. 转到“Microsoft Defender for Cloud”，然后选择“入门”页面 。

1. 选择“入门”选项卡。

1. 向下滚动并选择“添加非 Azure 服务器”部分下的“配置”。

1. 否则，请向讲师咨询如何创建包含租户管理员用户凭据的 Azure 订阅。

1. 选择之前创建的工作区旁边的“+ 添加服务器”。

1. 选择“下载 Windows 代理(64 位)”。

1. 选择“打开文件”，运行下载的 MMASetup-AMD64.exe 文件。

1. 选择“下一步”，直到显示“代理安装选项”向导页，选择“将代理连接到 Azure Log Analytics (OMS)”，然后选择“下一步”   。

1. 从 Azure 门户的“工作区密钥”文本框中，将“工作区 ID”和“主键”值复制并粘贴到相应的向导页面字段中，然后选择“下一步”   。

1. **注意：** 订阅创建过程可能需要长达 10 分钟的时间。

1. 转到“Microsoft Defender for Cloud”门户并选择“清单”。

1. The <bpt id="p1">**</bpt>WINServer<ept id="p1">**</ept> virtual machine will appear after at least 5 minutes. You may have to select <bpt id="p1">**</bpt>Refresh<ept id="p1">**</ept> to see it. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you see the number 1 under <bpt id="p2">*</bpt>Total resources<ept id="p2">*</ept> remove the filter to show the <bpt id="p3">*</bpt>WINServer<ept id="p3">*</ept> virtual machine.

1. 可以继续下一个实验室，稍后再返回查看 Microsoft Defender for Cloud 的“清单”部分 。

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
