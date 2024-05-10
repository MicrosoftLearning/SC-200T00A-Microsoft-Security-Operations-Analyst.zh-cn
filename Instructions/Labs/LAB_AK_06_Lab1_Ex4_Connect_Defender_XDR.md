---
lab:
  title: 练习 4 - 使用数据连接器将 Defender XDR 连接到 Microsoft Sentinel
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# 学习路径 6 - 实验室 1 - 练习 4 - 使用数据连接器将 Defender XDR 连接到 Microsoft Sentinel

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

你是一家公司的安全运营分析师，你所在公司同时部署了 Microsoft Defender XDR 和 Microsoft Sentinel。 你需要做好统一安全操作平台的准备工作，该平台用于将 Microsoft Sentinel 连接到 Defender XDR。 你下一步将安装 Defender XDR 内容中心解决方案，并将 Defender XDR 数据连接器部署到 Microsoft Sentinel。

### 任务 1：连接 Defender XDR

在此任务中，你将部署 Microsoft Defender XDR 连接器。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com>)。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在 Microsoft Sentinel 左侧菜单中，向下滚动到“内容管理”部分，然后选择“内容中心”。

1. 在“内容中心”，搜索“Microsoft Defender XDR”解决方案，并从列表中选择它。******

1. 在“Microsoft Defender XDR”解决方案详细信息页面上，选择“安装”******。

1. 安装完成后，搜索 Microsoft Defender XDR**** 解决方案并选择它。

1. 在“Microsoft Defender XDR”解决方案详细信息页面上，选择“管理”******

>**注意：***Microsoft Defender XDR* 解决方案安装 *Microsoft Defender XDR* 数据连接器、搜寻查询、工作簿和分析规则。

1. 选中“Microsoft Defender XDR 数据连接器”复选框，然后选择“打开连接器页面”。******

1. ******** 在“配置”部分的“说明”选项卡下，取消选中复选框“关闭这些产品的所有 Microsoft 事件创建规则”。**“建议”，然后选择“连接事件和警报”按钮。****

1. 应会看到一条指示连接成功的消息。

## 你已完成本实验室
