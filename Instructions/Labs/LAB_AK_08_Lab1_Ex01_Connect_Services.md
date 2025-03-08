---
lab:
  title: 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# 学习路径 8 - 实验室 1 - 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何连接来自组织中多个数据源的日志数据。 组织的数据来自 Microsoft 365、Microsoft 365 Defender、Azure 资源、非 Azure 虚拟机等。首先开始连接 Microsoft 源。

>**重要说明：** 学习路径 #8 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

### 完成本实验室的预计时间：20 分钟

### 任务 1：访问 Microsoft Sentinel 工作区

在此任务中，你将访问 Microsoft Sentinel 工作区。

>**备注：** 已在名称为 **defenderWorkspace** 的 Azure 订阅中预先部署了 Microsoft Sentinel，并且已安装所需的*内容中心*解决方案。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 打开 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com> )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择 Microsoft Sentinel **defenderWorkspace**。

1. 继续执行下一个任务。

### 任务 2：连接 Microsoft Defender for Cloud 数据连接器

在此任务中，你将连接 Microsoft Defender for Cloud 数据连接器。

   <!--- >>**Important:** To *Enable* Bi-directional sync, please rerun  **[Lab 05 Exercise 1](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_05_Lab1_Ex01_Enable_MDC.html)**, Task 2, and select **Setup** from the *Microsoft Defender for Cloud* navigation menu to verify all eligible Azure subscriptions are onboarded. --->

1. 在 Microsoft Sentinel 导航菜单中，向下滚动到“**内容管理**”部分，然后选择“**内容中心**”。

1. 在“内容中心”，搜索“Microsoft Defender for Cloud”解决方案，并从列表中选择它。

1. 在 *Microsoft Defender for Cloud* 解决方案详细信息页上，选择“**管理**”。

    >**备注：** Microsoft Defender for Cloud** 解决方案安装基于订阅的 Microsoft Defender for Cloud（旧版）** 数据连接器、基于租户的 Microsoft Defender for Cloud（预览版）** 数据连接器和分析规则。 当租户具有多个订阅时，将使用 *基于租户的 Microsoft Defender for Cloud（预览版）* 数据连接器。

1. 选择“基于订阅的 Microsoft Defender for Cloud（旧版）** 数据连接器”复选框，然后选择“打开连接器页”****。

1. 在 *“配置*”部分中，**选中** *MOC Subscription-XXXXXXXXXXXXXXXXX* 的复选框，然后选择“**连接**”链接，或向右滑动“**状态**”选项。

1. 若要启用双向同步，请选择“**为所有订阅启用 Microsoft Defender**”链接。

    >**备注：** 可能需要滚动到右侧才能看到链接。

1. 在“*Microsoft Defender for Cloud - 入门*”页上，应选中 *MOC Subscription-XXXXXXXXXXX* 的复选框，并且 *Microsoft Defender 计划*应显示“*启用 - 部分（剩余 30 个试用日）*”。

1. 选择右上方的“**X（关闭）**”按钮，关闭“*入门*”页。 在 *Microsoft Defender for Cloud* 配置页上，执行以下操作：

1. *MOC Subscription-XXXXXXXXX* 的“*状态*”现在应为“**已连接**”，并且“*双向同步*”应该是“*已启用*”。

    >**注意：** 可能需要刷新页面。

### 任务 3：连接 Azure 活动数据连接器

在此任务中，你将连接“Azure 活动”数据连接器。

1. 在 Microsoft Sentinel 导航菜单中，向下滚动到“*内容管理*”部分，然后选择“**内容中心**”。

1. 在“内容中心”，搜索“Azure 活动”解决方案并从列表中选择它。

1. 在“*Azure 活动*”解决方案页上，选择“**管理**”。

    >**备注：**“*Azure 活动*”解决方案会安装“*Azure 活动*”数据连接器、13 个分析规则、14 个搜寻查询和 1 个工作簿。

1. 选择“Azure 活动”数据连接器，然后选择“打开连接器页面”。

1. 在“说明”选项卡下的“配置”区域中，向下滚动到“2. 连接订阅...”，并选择“启动 Azure Policy 分配向导>”。

1. 在“**基本信息**”选项卡中，选择“**范围**”下的省略号按钮 (...)，从下拉列表中选择“*MOC Subscription-lodxxxxxxxx*”订阅，然后单击“**选择**”。

    >**备注：***请勿*选择可选资源组。

1. 选择“参数”选项卡，从“主要 Log Analytics 工作区”下拉列表中选择“uniquenameDefender”工作区。 此操作将应用订阅配置，以将信息发送到 Log Analytics 工作区。

1. 选择“修正”选项卡，然后选择“创建修正任务”复选框 。 此操作会将策略分配应用于现有的 Azure 资源。

1. 选择“查看 + 创建”按钮，检查配置。

1. 选择“创建”以完成操作。

## 继续进行练习 2
