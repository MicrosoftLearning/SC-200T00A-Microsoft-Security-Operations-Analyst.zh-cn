---
ms.openlocfilehash: 5558e8d3b103524ec27eb44b0b8531c7ae06720a
ms.sourcegitcommit: 6934bbcd5d9774aa44dd949cf9523e8a43a505d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2022
ms.locfileid: "147168435"
---
# <a name="module-1---mitigate-threats-using-microsoft-365-defender"></a>模块 1 - 使用 Microsoft 365 Defender 缓解威胁

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="use-the-microsoft-365-defender-portal"></a>使用 Microsoft 365 Defender 门户

在此任务中，你将熟悉 Microsoft 365 Defender 门户功能。

- （主页）仪表板
- 事件和警报
- 搜寻
- 操作中心
- 威胁分析
- 安全评分
- 终结点
- 漏洞管理
- 电子邮件和协作
- 云应用
- 报表
- 设置
- 权限

1. 如果你还未在浏览器中打开 Microsoft Defender 安全中心，请转到 Microsoft Defender 安全中心 (https://security.microsoft.com) )，并以租户管理员的身份登录。

1. 在“主页”仪表板中，可以全面查看安全状态。 可以通过添加卡片或删除卡片来自定义视图。 若要删除卡片，请选择卡片上的省略号 (...)。
1. 接下来，选择“事件和警报”。 此操作将展开下面的菜单选项。 在这里可以执行调查。
1. 使用“搜寻”执行相同的操作，以显示“高级搜寻”查询页面。 
    1. 可以在此处运行 KQL 查询。
1. 选择“操作和提交”将显示“操作中心”和“提交”
1. 选择“威胁分析”。 本页提供有关需要跟踪的常见漏洞和风险 (CVE) 的见解
1. 选择“安全功能分数”并浏览选项卡。 在此处查看“建议”。
1. 可以选择“终结点”和“设备库存”选项。 可以在此处加入设备，或者使用现有库存。
1. 此外，“终结点”部分还包括“漏洞管理”。 漏洞管理有一个仪表板，你可在其中查看风险评分。
1. “终结点”中的另一项功能是“评估和模拟”。 使用评估实验室，可以设置独立设备来了解恶意软件。
1. “电子邮件和协作”部分提供了 Defender for Office 365 功能。 你可从“调查”中看到自动调查和响应 (AIR) 威胁调查的结果。
1. “电子邮件和协作”中还包含“策略和规则”。 你将在此处配置“威胁和警报”策略。
1. 向下滚动到“云应用”。 这是“Microsoft Defender for Cloud Apps”服务部分。 在“应用治理”下，可以设置应用策略。
1. 在下一部分中，你可以找到 Microsoft 365 Defender 服务的报表“AUdit”，可在其中启用管理员操作跟踪，另外还有“权限”和“设置”   。
1. 在“权限”中，可以配置 Azure AD 和终结点角色。
1. 在“设置”中，可以输入常规配置（如时区和电子邮件通知），还包含终结点、标识和设备发现的精确设置。
1. 选择“设置”，然后选择“终结点”。 可在此处查看和添加“许可证”。 接下来，选择“高级功能”。 滚动浏览功能列表，但现在不要做任何改动。
1. 最后，离开“设置”，在左侧主菜单列表上，选择“更多资源”。 应会看到卡片或磁贴，其中包含 Microsoft Purview 合规性、Azure Active Directory 和其他功能的链接，这些功能不直接属于 Microsoft 365 Defender。 选择 Microsoft Purview 合规性的“打开”按钮。 此操作将打开合规性门户。

## <a name="you-have-completed-the-lab"></a>你已完成本实验室。