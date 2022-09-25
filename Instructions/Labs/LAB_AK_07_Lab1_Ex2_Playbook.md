---
lab:
  title: 练习 2 - 创建 Playbook
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-2---create-a-playbook"></a>模块 7 - 实验室 1 - 练习 2 - 创建 Playbook

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. Now, you want to respond and reMediate actions that can be run from Microsoft Sentinel as a routine.

使用 playbook，可以帮助自动执行和协调威胁响应，与其他内部系统和外部系统集成，并可以设置为自动运行以响应特定警报或事件（分别由分析规则或自动化规则触发时）。 


### <a name="task-1-create-a-security-operations-center-team-in-microsoft-teams"></a>任务 1：在 Microsoft Teams 中创建安全运营中心团队

在此任务中，你将创建 Microsoft Teams 团队以便在实验室中使用。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，打开新选项卡，然后导航到 Microsoft Teams 门户 (https://teams.microsoft.com) )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 关闭任何可能出现的 Teams 弹出窗口。

1. 如果尚未选择，请在左侧菜单上选择“团队”，然后在底部选择“加入或创建团队” 。

1. 在主窗口中选择“创建团队”按钮。

1. 选择“从头开始”按钮。

1. 选择“专用”按钮。

1. 为团队指定名称：键入“SOC”并选择“创建”按钮 。

1. 在“向 SOC 添加成员”屏幕中，选择“跳过”按钮。 

1. 向下滚动“团队”边栏选项卡以找到新创建的 SOC 团队，选择名称右侧的省略号“...”，然后选择“添加频道” 。

1. 输入频道名称“新建警报”，然后选择“添加”按钮。


### <a name="task-2-create-a-playbook-in-microsoft-sentinel"></a>任务 2：在 Microsoft Sentinel 创建 Playbook

在此任务中，你将创建在 Microsoft Sentinel 用作 Playbook 的逻辑应用。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在页面左侧的“内容管理”区域下，选择“社区”页。

1. On the right pane, select the <bpt id="p1">**</bpt>Onboard community content<ept id="p1">**</ept> link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content.

1. 选择“Solutions”文件夹。

1. 接下来，选择“Teams”文件夹，然后选择“Playbooks”文件夹。

1. 选择“Post-Message-Teams”文件夹。

1. 在“readme.md”框中，向下滚动到第二个“快速部署”选项“使用警报触发器进行部署”，并选择“部署到 Azure”按钮 。  

    ><bpt id="p1">**</bpt>VERY IMPORTANT<ept id="p1">**</ept>: Be aware that they are two different Microsoft Sentinel triggers to use, Incident and Alert. Make sure you are selecting the Alert (second) one.

1. 确保已选择 Azure 订阅。

1. 对于资源组，选择“新建”并输入“RG-Playbooks”，然后选择“确定”。

1. 将“区域”的默认值保留为“(US) 美国东部”。

1. Make sure the <bpt id="p1">*</bpt>Playbook Name<ept id="p1">*</ept> is "PostMessageTeams-OnAlert" and select <bpt id="p2">**</bpt>Review + create<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If the name is different, go back to GitHub and select the <bpt id="p2">**</bpt>Deploy with alert trigger<ept id="p2">**</ept> playbook.

1. 现在选择“创建”。 

    >**注意：** 请等待部署完成后再继续下一个任务。


### <a name="task-3-update-a-playbook-in-microsoft-sentinel"></a>任务 3：在 Microsoft Sentinel 中更新 Playbook

在此任务中，你将使用适当的连接信息更新创建的新 playbook。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 在“配置”区域下选择“自动化”，然后选择“可用的 Playbook”选项卡。

1. Select the <bpt id="p1">**</bpt>PostMessageTeams-OnAlert<ept id="p1">**</ept> playbook. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the playbook, refresh the Azure portal page by pressing Ctrl+F5.

1. 在 PostMessageTeams-OnAlert 的逻辑应用页的命令菜单中，选择“编辑”。

1. 选择第一个块，Microsoft Sentinel 警报。

1. 选择“更改连接”链接。

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 现在，选择第二个块“警报 - 获取事件”。

1. 选择“更改连接”链接。

1. 你需要了解如何使用 Microsoft Sentinel 检测和缓解威胁。

1. 现在，选择第三个块“连接”。

1. 现在，你想要响应和修正可以从 Microsoft Sentinel 作为例程运行的操作。

1. The block has now been renamed to <bpt id="p1">**</bpt>Post a message (V3)<ept id="p1">**</ept>, at the end of the <bpt id="p2">*</bpt>Team<ept id="p2">*</ept> field, select the <bpt id="p3">**</bpt>X<ept id="p3">**</ept> to clear the contents. The field will be changed to a drop-down with a listing of the available Teams from Microsoft Teams. Select <bpt id="p1">**</bpt>SOC<ept id="p1">**</ept>.

1. Do the same for the <bpt id="p1">*</bpt>Channel<ept id="p1">*</ept> field, select the <bpt id="p2">**</bpt>X<ept id="p2">**</ept> at the end of the field to clear the contents. The field will be changed to a drop-down with a listing of the Channels of the SOC Teams. Select <bpt id="p1">**</bpt>New Alerts<ept id="p1">**</ept>.

1. 在命令栏上选择“保存”。

将来的实验室中将使用逻辑应用。

## <a name="proceed-to-exercise-3"></a>继续完成练习 3
