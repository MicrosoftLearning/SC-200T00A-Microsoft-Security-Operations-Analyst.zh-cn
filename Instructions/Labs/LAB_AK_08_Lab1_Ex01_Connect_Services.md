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

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 打开 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com> )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择你在上一个实验室中创建的 Microsoft Sentinel 工作区。

1. 继续执行下一个任务。

### 任务 2：连接 Microsoft Defender for Cloud 数据连接器

在此任务中，你将连接 Microsoft Defender for Cloud 数据连接器。

1. 在 Microsoft Sentinel 左侧菜单中，向下滚动到“内容管理”部分，然后选择“内容中心”。

1. 在“内容中心”，搜索“Microsoft Defender for Cloud”解决方案，并从列表中选择它。

1. 在“Microsoft Defender for Cloud”解决方案详细信息页面上，选择“安装”******。

1. 安装完成后，搜索 Microsoft Defender for Cloud**** 解决方案并选择它。

1. 在“Microsoft Defender for Cloud”解决方案详细信息页面上，选择“管理”******

    >**备注：** Microsoft Defender for Cloud** 解决方案安装基于订阅的 Microsoft Defender for Cloud（旧版）** 数据连接器、基于租户的 Microsoft Defender for Cloud（预览版）** 数据连接器和分析规则。 当租户具有多个订阅时，将使用 *基于租户的 Microsoft Defender for Cloud（预览版）* 数据连接器。

1. 选择“基于订阅的 Microsoft Defender for Cloud（旧版）** 数据连接器”复选框，然后选择“打开连接器页”****。

1. 在“说明”选项卡下的“配置”部分，选中“Azure Pass - 赞助”订阅的复选框，并将“状态”选项滑动到右侧  。

    >注意：如果切换回断开连接，请查看学习路径 3 练习 1 任务 1，为帐户分配适当的权限。

1. 现在，“状态”应该是“已连接”，并且“双向同步”应该是“已启用”。

    <!--- 1. Scroll down and under the *Create incidents - Recommended!* area, verify that *Create incidents automatically from all alerts generated in this connected service* is **Enabled**. --->

### 任务 3：连接 Azure 活动数据连接器

在此任务中，你将连接“Azure 活动”数据连接器。

1. 在 Microsoft Sentinel 左侧菜单中，向下滚动到“内容管理”部分，然后选择“内容中心”。

1. 在“内容中心”，搜索“Azure 活动”解决方案并从列表中选择它。

1. 在“Azure 活动”解决方案页中，选择“安装”。

1. 安装完成后，选择“管理”

    >注意：“Azure 活动”解决方案会安装“Azure 活动”数据连接器、12 个分析规则、14 个搜寻查询和 1 个工作簿。

1. 选择“Azure 活动”数据连接器，然后选择“打开连接器页面”。

1. 在“说明”选项卡下的“配置”区域中，向下滚动到“2. 连接订阅...”，并选择“启动 Azure Policy 分配向导>”。

1. 在“基本信息”选项卡中，选择“范围”下的省略号按钮 (...)，然后从下拉列表中选择你的“Azure Pass - 赞助”订阅，然后单击“选择”  。

1. 选择“参数”选项卡，从“主要 Log Analytics 工作区”下拉列表中选择“uniquenameDefender”工作区。 此操作将应用订阅配置，以将信息发送到 Log Analytics 工作区。

1. 选择“修正”选项卡，然后选择“创建修正任务”复选框 。 此操作会将策略分配应用于现有的 Azure 资源。

1. 选择“查看 + 创建”按钮，检查配置。

1. 选择“创建”以完成操作。

## 继续进行练习 2
