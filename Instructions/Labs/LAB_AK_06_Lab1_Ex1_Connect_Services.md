---
lab:
  title: 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel
  module: Module 6 - Connect logs to Microsoft Sentinel
ms.openlocfilehash: ba1ab1fbfbc322357395fc6d78ba124eda9d00cc
ms.sourcegitcommit: 190d5d493301a8c8d98c86772d2500128637ad2d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "146650236"
---
# <a name="module-6---lab-1---exercise-1---connect-data-to-microsoft-sentinel-using-data-connectors"></a>模块 6 - 实验室 1 - 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何连接来自组织中多个数据源的日志数据。 组织的数据来自 Microsoft 365、Microsoft 365 Defender、Azure 资源、非 Azure 虚拟机等。首先开始连接 Microsoft 源。


### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>任务 1：访问 Microsoft Sentinel 工作区

在此任务中，你将访问 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 打开 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择你在上一个实验室中创建的 Microsoft Sentinel 工作区。


### <a name="task-2-connect-the-azure-active-directory-connector"></a>任务 2：连接 Azure Active Directory 连接器

在此任务中，你要将 Azure Active Directory 连接器连接到 Microsoft Sentinel。

1. 在“配置”区域下，选择“数据连接器”。 在“数据连接器”页面中，搜索“Azure Active Directory”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 从“配置”区域中选择“登录日志”和“审核日志”选项，然后选择“应用更改”。


### <a name="task-3-connect-the-azure-active-directory-identity-protection-connector"></a>任务 3：连接 Azure Active Directory 标识保护连接器

在此任务中，你要将 Azure Active Directory 标识保护连接器连接到 Microsoft Sentinel。

1. 在“数据连接器”选项卡中，搜索“Azure Active Directory 标识保护”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 从“配置”区域，选择“连接”按钮。


### <a name="task-4-connect-the-microsoft-defender-for-cloud-connector"></a>任务 4：连接 Microsoft Defender for Cloud 连接器

在此任务中，你将连接 Microsoft Defender for Cloud 连接器。

1. 在“数据连接器”选项卡中，搜索“Microsoft Defender for Cloud”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”区域的“订阅”下，选中“Azure Pass - 赞助”订阅的复选框，并将“状态”选项滑动到右侧以指示“已连接” 。

1. 现在，“状态”应该是“已连接”，并且“双向同步”应该是“已启用” 。

1. 向下滚动，在“创建事件 - 推荐!” 区域下，选择“启用”。 此选项会自动为此服务创建“分析”规则。 如果此处未启用，可稍后手动添加它，或者在“分析”边栏选项卡中更改其配置。


### <a name="task-5-connect-the-microsoft-365-defender-connector"></a>任务 5：连接 Microsoft 365 Defender 连接器

在此任务中，你将连接 Microsoft 365 Defender 连接器。

1. 在“数据连接器”选项卡中，搜索“Microsoft 365 Defender(预览版)”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”区域中，选择“连接事件和警报”。 

1. 在“连接事件”下，选中“名称”复选框，从而选中“Microsoft Defender for Endpoint”的所有复选框。

1. 针对“Microsoft Defender for Office 365”执行相同的操作

1. 滚动到页面底部，并选择“应用更改”。


### <a name="task-6-connect-the-azure-activity-connector"></a>任务 6：连接 Azure 活动连接器

在此任务中，你将连接 Azure 活动连接器。

1. 在“数据连接器”选项卡中，搜索“Azure 活动”连接器，并从列表中选择它。

1. 在连接器信息边栏选项卡上选择“打开连接器页面”。

1. 在“配置”区域中，向下滚动，在“2. 连接订阅...”下选择“启动 Azure Policy 分配向导>”。

1. 在“基本信息”选项卡中，选择“范围”下的省略号按钮 (...)，然后从下拉列表中选择你的“Azure Pass - 赞助”订阅，然后单击“选择”  。

1. 选择“参数”选项卡，从“主要 Log Analytics 工作区”下拉列表中选择“uniquenameDefender”工作区。

1. 选择“修正”选项卡，然后选择“创建修正任务”复选框 。

1. 选择“查看 + 创建”按钮，检查配置。

1. 选择“创建”以完成操作。

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
