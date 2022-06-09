---
lab:
  title: 练习 1 - 探索 Microsoft 365 Defender
  module: Module 1 - Mitigate threats using Microsoft 365 Defender
ms.openlocfilehash: 675aa05339ee8b5f24e45aa17d737d2155d2a164
ms.sourcegitcommit: ac5992dcbc64a608d24a33e084c71f456327b07d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2022
ms.locfileid: "145892523"
---
# <a name="module-1---lab-1---exercise-1---explore-microsoft-365-defender"></a>模块 1 - 实验室 1 - 练习 1 - 探索 Microsoft 365 Defender 

## <a name="lab-scenario"></a>实验室方案

![M365 Defender](../Media/SC-200-Lab_M1_L1_Ex1.png)

你是一家公司的安全运营分析师，你所在公司正在实现 Microsoft 365 Defender。 首先，在 EOP 和 Microsoft Defender for Office 365 中分配预设的安全策略。


### <a name="task-1-obtain-your-microsoft-365-credentials"></a>任务 1：获取 Microsoft 365 凭据

启动实验室后，你将获得一个免费试用版租户，可在 Microsoft 虚拟实验室环境中访问。 系统会自动向该租户分配一个唯一用户名和密码。 你需要检索此用户名和密码，以便在 Microsoft 虚拟实验室环境中登录 Azure 和 Microsoft 365。 

由于学习合作伙伴可以通过多家授权实验室托管 (ALH) 提供商中的任何一家来提供本课程，因此检索与租户关联的租户 ID 所涉及的实际步骤可能因实验室托管提供商而异。 因此，讲师需要向你提供必要的指导，介绍如何检索课程的此类信息。 你应该记录以供稍后使用的信息包括：

- 租户后缀 ID。 此 ID 适用于将在所有实验室中用来登录 Microsoft 365 的 onmicrosoft.com 帐户。 其格式为 {username}@ZZZZZZ.onmicrosoft.com，其中 ZZZZZZ 是实验室托管提供者提供的唯一租户后缀 ID。 记录此 ZZZZZZ 值以供稍后使用。 当有任何实验室步骤指示你登录 Microsoft 365 门户时，都必须输入在此处获取的 ZZZZZZ 值。
- 租户密码。 这是由实验室托管提供者提供的管理员帐户的密码。


### <a name="task-2-apply-microsoft-defender-for-office-365-preset-security-policies"></a>任务 2：应用 Microsoft Defender for Office 365 预设的安全策略

在此任务中，将在 Microsoft 365 安全门户中为 EOP 和 Microsoft Defender for Office 365 分配预设策略。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 启动 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，转到 Microsoft 365 Defender 门户 (https://security.microsoft.com) )。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

    >注意：如果收到消息“无法访问此部分。” 请等待 5 分钟，再重试。 有时访问规则需传播租户，这可能需要几分钟时间。  

1. 如果显示，请关闭 Microsoft 365 Defender 快速导览。

1. 在导航菜单中的“电子邮件与协作”区域下，选择“策略与规则”。

1. 在“策略与规则”仪表板上，选择“威胁策略”。

1. 在“威胁策略”仪表板上，选择“预设安全策略”。

    >**注意：** 如果收到消息“客户端错误 - 收到 bip 规则时出错”，请选择“确定”以继续。 此错误是由于 Office 365 在默认情况下未启用租户的冻结状态。

1. 在 *“标准保护*”下，选择 **“应用标准策略**”。

1. 在“EOP 保护适用范围”部分，在“域”下，写入租户的域名，选中它，然后选择“下一步” 。 提示：租户的域名与管理员帐户的域名相同，可能与 WWLx####.onmicrosoft.com 类似。 请注意，此配置适用于防垃圾邮件、出站垃圾邮件筛选器、防恶意软件和防钓鱼的策略。 

1. 在“Defender for Office 365 保护适用范围”部分，应用与上一步相同的配置，然后选择“下一步”。 请注意，此配置适用于防钓鱼、安全附件、安全链接的策略。

1. 在 *“策略模式”* 部分中，确保选中“完成单选按钮 **后启用策略** ”，然后选择“ **下一步**”。

1. 阅读“查看并确认更改”下的内容，选择“确认”以应用更改，然后选择“完成”以完成 。

1. 在 *“严格保护*”下，选择 **“应用标准策略**”。 提示：在“电子邮件与协作 - 策略与规则 - 威胁策略 - 预设安全策略”下找到“严格保护”。

1. 在“EOP 保护适用范围”中，在“组”下写入“领导层”，选择它，然后选择“下一步”  。 请注意，此配置适用于防垃圾邮件、出站垃圾邮件筛选器、防恶意软件和防钓鱼的策略。

1. 在“Defender for Office 365 保护适用范围”部分，应用与上一步相同的配置，然后选择“下一步”。 请注意，此配置适用于防钓鱼、安全附件、安全链接的策略。

1. 在 *“策略模式”* 部分中，确保选中“完成单选按钮 **后启用策略** ”，然后选择“ **下一步**”。

1. 阅读“查看并确认更改”下的内容，选择“确认”以应用更改，然后选择“完成”以完成 。

1. 在顶部中间菜单中，选择“威胁策略”以返回，在“策略”下，选择“安全附件”。 请注意，这两个预设策略都显示在此处，状态为“开启”。

1. 在菜单中，选择“全局设置”的“齿轮”图标 。

1. 通读可用的集成选项，然后选择“取消”以返回。

1. 在 Microsoft 365 Defender 门户中，从左侧“导航”菜单中选择“设置” 。

1. 在“设置”页面上，选择“Microsoft 365 Defender” 。 你将看到一张咖啡杯图像和一条信息，消息的内容是:“稍等一下！ 我们正在为数据准备新空间并连接它们”。 需要几分钟才能完成，因此请让页面保持打开状态，直到下一个实验室。 

    >**注意：** 如果收到错误消息“我们未计划到它会失败，但出现了问题。” 请稍后重试此步骤，或在下一实验室之前重试。

1. 当新空间成功完成时，你将看到 Microsoft 365 Defender 的帐户、电子邮件通知、预览功能和流式处理 API 的设置。

## <a name="you-have-completed-the-lab"></a>你已完成本实验室。
