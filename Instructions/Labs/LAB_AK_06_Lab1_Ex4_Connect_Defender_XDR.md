---
lab:
  title: 练习 4 - 使用数据连接器将 Defender XDR 连接到 Microsoft Sentinel
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# 学习路径 6 - 实验室 1 - 练习 4 - 使用数据连接器将 Defender XDR 连接到 Microsoft Sentinel

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

你是一家公司的安全运营分析师，你所在公司同时部署了 Microsoft Defender XDR 和 Microsoft Sentinel。 你需要做好统一安全操作平台的准备工作，该平台用于将 Microsoft Sentinel 连接到 Defender XDR。 你下一步将安装 Defender XDR 内容中心解决方案，并将 Defender XDR 数据连接器部署到 Microsoft Sentinel。

>**重要提示：** 请注意，Azure Microsoft Sentinel 门户和 Microsoft Defender XDR Sentinel 门户之间存在功能差异 **[门户功能差异](https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-defender-portal#capability-differences-between-portals)**。

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

1. 在“Microsoft Defender XDR”** 解决方案详细信息页上，选择“安装”****。

1. 安装完成后，搜索 Microsoft Defender XDR**** 解决方案并选择它。

1. 在“Microsoft Defender XDR”** 解决方案详细信息页上，选择“管理”****

>**注意：***Microsoft Defender XDR* 解决方案安装 *Microsoft Defender XDR* 数据连接器、搜寻查询、工作簿和分析规则。

1. 选中“Microsoft Defender XDR 数据连接器”复选框，然后选择“打开连接器页面”。******

1. ******** 在“配置”部分的“说明”选项卡下，取消选中复选框“关闭这些产品的所有 Microsoft 事件创建规则”。**“建议”，然后选择“连接事件和警报”按钮。****

1. 应会看到一条指示连接成功的消息。

### 任务 2：连接 Microsoft Sentinel 和 Microsoft Defender XDR

在此任务中，你要将 Microsoft Sentinel 工作区连接到 Microsoft Defender XDR。

>**注意：** Microsoft Defender XDR 门户中的 Microsoft Sentinel 以公共预览版提供，用户界面体验和步骤可能与实验说明有所不同。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：********Pa55w.rd**。  

1. 启动 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，转到 Microsoft Defender XDR 门户 (https://security.microsoft.com)。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

    >提示：可以在“资源”选项卡上找到管理员的租户电子邮件帐户和密码。

1. 在“Defender XDR”**** 门户的“主页”**** 屏幕上，应该会在顶部看到一个横幅，其中显示消息“在一个位置获取 SIEM 和 XDR”**。 选择“连接工作区”**** 按钮。

1. 在“选择工作区”页上，选择之前创建的 Microsoft Sentinel 工作区。******

    >提示****：它的名称应类似于 uniquenameDefender**。

1. 选择“**下一步**”按钮。

    >注意：**** 如果“下一步”** 按钮禁用或灰显，则会看到一条错误消息，指出 Microsoft Sentinel 工作区** 未载入到 Defender XDR，请尝试刷新 Defender XDR 门户页面，因为同步可能需要 5 到 10 分钟。

1. 在“查看更改”** 页上，验证工作区** 选择是否正确，并查看“连接工作区后的预期结果”** 部分的项目符号项。 选择**连接**按钮。

1. 你应该会看到消息“正在连接工作区”**，然后看到消息“工作区已成功连接”**。

1. 选择“关闭”**** 按钮。 

1. 在“Defender XDR”**** 门户的“主页”**** 屏幕上，应该会在顶部看到一个横幅，其中显示消息“你的统一 SIEM 和 XDR 已准备就绪”**。 选择“开始搜寻”按钮****。

1. 在“高级搜寻”** 中，应该会看到一条消息“浏览 Sentinel 中的内容”。 在左侧菜单窗格中，记下相应选项卡下的 Microsoft Sentinel** 表、函数和查询。

1. 展开左侧主菜单窗格（如果已折叠）并展开新的 Microsoft Sentinel**** 菜单项。 应该会看到“威胁管理”**、“内容管理”** 和“配置”** 选择。

 >**注意：** 某些功能在公共预览版中可能不可用，用户界面可能与实验说明有所不同。 此外，Microsoft Sentinel 和 Microsoft Defender XDR 之间的同步可能需要几分钟才能完成，因此你可能看不到所有已安装的数据连接器**。

## 你已完成本实验
