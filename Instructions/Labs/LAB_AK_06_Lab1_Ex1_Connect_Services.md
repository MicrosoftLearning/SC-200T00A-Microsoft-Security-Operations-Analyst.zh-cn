---
lab:
  title: 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# 学习路径 6 - 实验室 1 - 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何连接来自组织中多个数据源的日志数据。 组织的数据来自 Microsoft 365、Microsoft 365 Defender、Azure 资源、非 Azure 虚拟机等。首先开始连接 Microsoft 源。

>                **注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Connect%20data%20to%20Microsoft%20Sentinel%20using%20data%20connectors)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。 


### 任务 1：访问 Microsoft Sentinel 工作区

在此任务中，你将访问 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 打开 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择你在上一个实验室中创建的 Microsoft Sentinel 工作区。


### 任务 2：连接 Microsoft Defender for Cloud 连接器

在此任务中，你将连接 Microsoft Defender for Cloud 连接器。

1. 在“数据连接器”选项卡中，搜索“Microsoft Defender for Cloud”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”区域的“订阅”下，选中“Azure Pass - 赞助”订阅的复选框，并将“状态”选项滑动到右侧” 。

    >注意：如果切换回断开连接，请查看学习路径 3 练习 1 任务 1，为帐户分配适当的权限。

1. 现在，“状态”应该是“已连接”，并且“双向同步”应该是“已启用”。

1. 向下滚动，在“创建事件 - 推荐!” 区域下，选择“启用”。 

    >注意：此选项会自动为此连接器创建 Analytics 规则。 如果此处未启用，可稍后手动添加它，或者在“分析”边栏选项卡中更改其配置。


### 任务 3：连接 Azure 活动连接器

在此任务中，你将连接 Azure 活动连接器。

1. 在“数据连接器”选项卡中，搜索“Azure 活动”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”区域中，向下滚动，在“2. 连接订阅...”下选择“启动 Azure Policy 分配向导>”。

1. 在“基本信息”选项卡中，选择“范围”下的省略号按钮 (...)，然后从下拉列表中选择你的“Azure Pass - 赞助”订阅，然后单击“选择”  。

1. 选择“参数”选项卡，从“主要 Log Analytics 工作区”下拉列表中选择“uniquenameDefender”工作区。

1. 选择“修正”选项卡，然后选择“创建修正任务”复选框 。 此操作将应用订阅配置，以将信息发送到 Log Analytics 工作区。

1. 选择“查看 + 创建”按钮，检查配置。

1. 选择“创建”以完成操作。

## 继续进行练习 2
