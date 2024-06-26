---
lab:
  title: 练习 2 - 创建 Playbook
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 7 - 实验室 1 - 练习 2 - 创建 Playbook

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何使用 Microsoft Sentinel 检测和缓解威胁。 现在，你想要响应和修正可以从 Microsoft Sentinel 作为例程运行的操作。

使用 playbook，可以帮助自动执行和协调威胁响应，与其他内部系统和外部系统集成，并可以设置为自动运行以响应特定警报或事件（分别由分析规则或自动化规则触发时）。 

>**注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20a%20playbook)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。

### 任务 1：在 Microsoft Teams 中创建安全运营中心团队

在此任务中，你将创建 Microsoft Teams 团队以便在实验室中使用。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，打开新标签页，然后导航到 Microsoft Teams 门户 (https://teams.microsoft.com) )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 关闭任何可能出现的 Teams 弹出窗口。

    >**注意：** 如果系统提示使用“新 Teams”，请接受并继续练习****。

1. 如果尚未选择，请在左侧菜单中选择“团队”，然后在顶部选择加号图标。****![](../Media/plus-sign-icon-lab.png)

1. 选择“创建团队”选项。****

1. 选择“从头开始”按钮。

1. 选择“专用”按钮。

1. 为团队指定名称：键入“SOC”并选择“创建”按钮 。

1. 在“向 SOC 添加成员”屏幕中，选择“跳过”按钮。 

1. 向下滚动“团队”边栏选项卡以找到新创建的 SOC 团队，选择名称右侧的省略号“...”，然后选择“添加频道” 。

1. 输入频道名称“新建警报”，然后选择“添加”按钮。


### 任务 2：在 Microsoft Sentinel 创建 Playbook

在此任务中，你将创建在 Microsoft Sentinel 用作 Playbook 的逻辑应用。

1. 在 Microsoft Edge 浏览器中，导航到 [GitHub 上的 Microsoft Sentinel](https://github.com/Azure/Azure-Sentinel)。

<!--- the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace you created earlier.

1. Select the **Community** page under the *Content management* area on the left side of the page.

1. On the right pane, select the **Onboard community content** link. This opens a new tab in the Microsoft Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

1. 向下滚动并选择“解决方案”文件夹。

1. 接下来，选择“SentinelSOARessentials”文件夹，然后选择“Playbooks”文件夹。

1. 选择“Post-Message-Teams”文件夹。

1. 在 readme.md 框中，向下滚动到“快速部署”部分的“使用事件触发器进行部署(推荐)”，然后选择“部署到 Azure”按钮 。  

1. 确保已选择 Azure 订阅。

1. 对于资源组，选择“新建”并输入“RG-Playbooks”，然后选择“确定”。

1. 将“区域”的默认值保留为“(US) 美国东部”。

1. 将“playbook 名称”重命名为“PostMessageTeams-OnIncident”，然后选择“查看 + 创建”。

1. 现在选择“创建”。 

    >**注意：** 请等待部署完成后再继续下一个任务。

### 任务 3：在 Microsoft Sentinel 中更新 Playbook

在此任务中，你将使用适当的连接信息更新创建的新 playbook。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 在“配置”区域下选择“自动化”，然后选择“可用的 Playbook”选项卡。

1. 如果看不到任何 playbook，请在命令栏中选择“刷新”。 应会显示在上一步中创建的 Playbook。

1. 选择“PostMessageTeams”playbook 名称。

1. 在 PostMessageTeams 的逻辑应用页的命令菜单中，选择“编辑”。

    >**注意：** 可能需要刷新页面。

1. 选择第一个块“Microsoft Sentinel 事件”******。

1. 选择“更改连接”链接。

1. 选择“添加新项”，然后选择“登录” 。 当系统提示时，在新窗口中，选择 Azure 订阅管理员凭据。 现在，块的最后一行应显示“已连接到 your-admin-username”。

1. 现在，选择第二个块“发布消息(V3)”******。

1. 在“Prameters”选项卡中，向下滚动并选择“更改连接”链接，然后选择“添加新连接”和“登录”************。 出现提示时选择你的 Azure 管理员凭据。 “Prameters”选项卡现在应显示“已连接到 <your-admin-username>”。

1. 在“团队”字段的末尾，选择 X 以清除内容******。 该字段将改为列出 Microsoft Teams 中各个可用团队的下拉列表。 选择“SOC”。

1. 对“频道”字段进行相同的选择，选择字段末尾的“X”以清除内容。 字段将更改为一个下拉列表，其中列出了 SOC 团队的频道。 选择“新建警报”。

1. 在命令栏上选择“保存”。 将来的实验室中将使用逻辑应用。

## 继续完成练习 3
