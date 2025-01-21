---
lab:
  title: 练习 1 - 修改 Microsoft 安全规则
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 9 - 实验室 1 - 练习 1 - 修改 Microsoft 安全规则

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何使用 Microsoft Sentinel 检测和缓解威胁。 首先，需要按严重性将来自 Defender for Cloud 的警报筛选到 Microsoft Sentinel 中。

>**重要说明：** 学习路径 #9 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

### 完成本实验的预计时间：10 分钟

### 任务 1：激活 Microsoft 安全规则

在此任务中，你将激活 Microsoft 安全规则。

>**备注：** Microsoft Sentinel 已在 Azure 订阅中预先部署了名称 **defenderWorkspace**，并且已安装所需的“*内容中心*”解决方案。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com>)。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择 Microsoft Sentinel **defenderWorkspace**。

1. 从“配置”区域选择“分析”。

1. 选择命令栏中的“+ 创建”按钮，然后选择“Microsoft 事件创建规则” 。

1. 在“*名称*”下，输入“**基于 Defender for Cloud 创建事件**”。

1. 向下滚动，在“*Microsoft 安全服务*”下选择“**Microsoft Defender for Cloud**”。

1. 在“按严重性筛选”下，选择“自定义”选项，为严重级别选择“低”、“中”和“高”，然后返回到规则   。

1. 选择“下一步: 自动响应”按钮，然后选择“下一步: 查看和创建”按钮。

1. 查看所做的更改并选择“保存”按钮****。 如果 Defender for Cloud 中存在警报，则会保存分析规则并创建事件。

1. 现在，你将拥有一种“*融合*”和一种“*Microsoft 安全*”警报类型。

## 继续进行练习 2
