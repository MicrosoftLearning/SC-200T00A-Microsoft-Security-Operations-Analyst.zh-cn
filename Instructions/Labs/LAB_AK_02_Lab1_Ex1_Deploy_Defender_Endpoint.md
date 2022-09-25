---
lab:
  title: 练习 1 - 部署 Microsoft Defender for Endpoint
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# <a name="module-2---lab-1---exercise-1---deploy-microsoft-defender-for-endpoint"></a>模块 2 - 实验室 1 - 练习 1 - 部署 Microsoft Defender for Endpoint

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Defender for Endpoint. Your manager plans to onboard a few devices to provide insight into required changes to the Security Operations (SecOps) team response procedures.

You start by initializing the Defender for Endpoint environment. Next, you onboard the initial devices for your deployment by running the onboarding script on the devices. You configure security for the environment. Lastly, you create Device groups and assign the appropriate devices.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept>  The lab Virtual Machines are used through different modules. SAVE your virtual machines. If you exit the lab without saving, you will be required to re-run some configurations again.

>**注意：** 请确保已成功完成前一模块的任务 3。


### <a name="task-1-initialize-microsoft-defender-for-endpoint"></a>任务 1：初始化 Microsoft Defender for Endpoint

在此任务中，你将执行 Microsoft Defender for Endpoint 门户的初始化。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 如果尚未处于 Microsoft 365 Defender 门户，请启动 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，转到 Microsoft 365 Defender 门户 (https://security.microsoft.com) )。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

1. 在 Microsoft 365 Defender 门户中，从左侧“导航”菜单中选择“设置” 。

1. 在“设置”页面上，选择“设备发现” 。 

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you do not see the <bpt id="p2">**</bpt>Device discovery<ept id="p2">**</ept> option under <bpt id="p3">**</bpt>Settings<ept id="p3">**</ept>, logout by selecting the top-right circle with your account initials and select <bpt id="p4">**</bpt>Sign out<ept id="p4">**</ept>. Other options that you might want to try is to refresh the page with Ctrl+F5 or open the page InPrivate. Login again with the <bpt id="p1">**</bpt>Tenant Email<ept id="p1">**</ept> credentials.

1. In Discovery setup make sure <bpt id="p1">**</bpt>Standard discovery (recommended)<ept id="p1">**</ept> is selected. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the option, refresh the page.


### <a name="task-2-onboard-a-device"></a>任务 2：加入设备。

在此任务中，你需要使用加入脚本将设备加入 Microsoft Defender for Endpoint。

1. 如果你在浏览器中尚未处于 Microsoft 365 Defender 门户上，请启动 Microsoft Edge 浏览器并转到 (https://security.microsoft.com) 并使用“租户电子邮件”凭据登录。

1. 从左侧菜单栏中选择“设置”，然后从“设置”页面中选择“终结点” 。

1. 在“设备管理”部分选择“加入”。

1. 你是一家公司的安全操作分析师，你的公司正在实施 Microsoft Defender for Endpoint。

1. 右键单击已下载的 zip 文件，然后选择“全部提取...”，确保选中“完成时显示提取的文件”，然后选择“提取”。

1. 你的主管计划加入一些设备，以深入了解安全运营 (SecOps) 团队响应程序所需的更改。

1. Right-click on the extracted file "WindowsDefenderATPLocalOnboardingScript.cmd" again and choose <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>.  <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you encounter the Windows SmartScreen window, select on <bpt id="p2">**</bpt>More info<ept id="p2">**</ept>, and choose <bpt id="p3">**</bpt>Run anyway<ept id="p3">**</ept>. 
    
1. 首先初始化 Defender for Endpoint 环境。

1. 接下来，通过对初始设备运行加入脚本，为你的部署加入这些设备。

1. 配置环境的安全性。  

1. 在 WIN1 虚拟机的 Windows 搜索栏中，键入“CMD”，然后在命令提示符应用的右窗格上，选择“以管理员身份运行” 。 

1. 显示“用户帐户控制”窗口时，选择“是”以允许应用运行。 

1. 最后，创建设备组并分配适当的设备。

1. In the Microsoft 365 Defender portal, in the left-hand menu, under the <bpt id="p1">**</bpt>Assets<ept id="p1">**</ept> area, select <bpt id="p2">**</bpt>Devices<ept id="p2">**</ept>. If the device is not shown, complete the next task and come back to check it back later. It can take up to 60 minutes for the first device to be displayed in the portal.

    >**注意：** 如果你已完成载入过程，但在一小时后未在“设备”列表中看到设备，这可能指示存在载入或连接问题。


### <a name="task-3-configure-roles"></a>任务 3：配置角色

在此任务中，你将配置用于设备组的角色。

1. 在 Microsoft 365 Defender 门户中，从左侧菜单栏中选择“设置”，然后选择“终结点” 。 

1. 在“权限”区域下选择“角色”。

1. 选择“启用角色”按钮。

1. 选择“+ 添加项”。

1. 在“添加角色”对话框中，输入以下内容：

    |常规设置|值|
    |---|---|
    |角色名称|**第 1 层支持**|
    |权限|实时响应功能 - 高级|

1. **重要提示：** 通过不同的模块使用实验室虚拟机。

1. 选择“保存”。


### <a name="task-4-configure-device-groups"></a>任务 4：配置设备组

在此任务中，你将配置允许访问控制和自动化配置的设备组。

1. 在 Microsoft 365 Defender 门户中，从左侧菜单栏中选择“设置”，然后选择“终结点” 。 

1. 在“权限”区域中，选择“设备组”。

1. 选择“+ 添加设备组”图标。

1. 在“常规”选项卡中输入以下信息：

    |常规设置|值|
    |---|---|
    |设备组名称|**常规**|
    |自动化级别|全面 - 自动修正威胁|

1. 选择“下一步”  。

1. 在“设备”选项卡中，对操作系统条件选择“Windows 10”，然后选择“下一步” 。

1. 请保存你的虚拟机。

1. 如果在不保存的情况下退出实验室，将需要再次重新运行某些配置。

1. 选择“完成”  。

1. Device group configuration has changed. Select <bpt id="p1">**</bpt>Apply changes<ept id="p1">**</ept> to check matches and recalculate groupings.

1. 现在，你将有两个设备组；刚创建的“常规”设备组和具有相同修正级别的“未分组的设备（默认）”设备组。

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
