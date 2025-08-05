---
lab:
  title: 练习 4 - 使用数据连接器将 Defender XDR 连接到 Microsoft Sentinel
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# 学习路径 8 - 实验室 1 - 练习 4 - 使用数据连接器将 Defender XDR 连接到 Microsoft Sentinel

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex4.png)

你是一家公司的安全运营分析师，你所在公司同时部署了 Microsoft Defender XDR 和 Microsoft Sentinel。 你需要做好统一安全操作平台的准备工作，该平台用于将 Microsoft Sentinel 连接到 Defender XDR。 你下一步将安装 Defender XDR 内容中心解决方案，并将 Defender XDR 数据连接器部署到 Microsoft Sentinel。

>**备注：** 本练习的环境是由产品生成的模拟。 由于是有限的模拟，因此页面上的链接可能未启用，并且不支持超出指定脚本范围的文本输入。 将显示弹出消息，指出“此功能在模拟中不可用。” 发生这种情况时，请选择“确定”并继续执行练习步骤。

![弹出错误消息](../Media/simulation-pop-up-error.png)

### 任务 1：连接 Defender XDR

在此任务中，你将部署 Microsoft Defender XDR 连接器。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，选择以下链接打开模拟环境：[Azure 门户]( https://app.highlights.guide/start/1c894b46-4b0a-40cb-b0f0-1e1c86c615f3?token=16d48b6c-eace-4a1f-8050-098d29d23a89)。

1. 在 Azure 门户主页** 上，选择 Microsoft Sentinel**** 图标。

1. 在 Microsoft Sentinel** 页上，选择 Woodgrove-LogAnalyiticWorkspace**** 工作区。

1. 在 Microsoft Sentinel 左侧菜单中，向下滚动到“内容管理”部分，然后选择“内容中心”。

1. 在“内容中心”，搜索“Microsoft Defender XDR”解决方案，并从列表中选择它。******

1. 在“Microsoft Defender XDR”** 解决方案详细信息页上，选择“安装”****。

1. 安装完成后，搜索 Microsoft Defender XDR**** 解决方案并选择它。

1. 在“Microsoft Defender XDR”** 解决方案详细信息页上，选择“管理”****

1. 选中“Microsoft Defender XDR 数据连接器”复选框，然后选择“打开连接器页面”。******

1. 应会看到一条指示连接成功的消息。

### 任务 2：连接 Microsoft Sentinel 和 Microsoft Defender XDR

在此任务中，你将继续进行模拟，并将 Microsoft Sentinel 工作区连接到 Microsoft Defender XDR。

1. 导航回 Microsoft Sentinel“内容中心”**（使用页面顶部的“痕迹导航”菜单链接），然后从导航菜单的“常规”部分选择“概述(预览版)”****。

1. 在“在一个位置获取 SIEM 和 XDR”消息中选择“了解详细信息”按钮******。

1. 选择“了解详细信息”按钮后，浏览器中随即打开一个新标签页，展示 Microsoft Defender XDR 门户。******

1. 在 Defender 门户主页屏幕上，应会看到顶部横幅中有一条消息：“在一个位置获取 SIEM 和 XDR”。********** 选择“连接工作区”**** 按钮。

1. 在“选择工作区”页上，选择“woodgrove-loganalyiticsworkspace”这个 Microsoft Sentinel 工作区。******

1. 选择“**下一步**”按钮。

1. 在“设置主工作区”页上，下拉菜单中应会显示“woodgrove-loganalyiticsworkspace”这一 Microsoft Sentinel 工作区。******** 选择“**下一步**”按钮。

1. 在“查看并完成”页上，确认“工作区”选择正确无误，并查看“连接工作区后的预期结果”部分的项目符号项。****** 选择**连接**按钮。

1. 应会看到“即将连接工作区”** 消息。 选择**连接**按钮。

1. 你现在应位于“工作区已成功连接”** 页上。

1. 选择“关闭”**** 按钮。

1. 在“Defender XDR”**** 门户的“主页”**** 屏幕上，应该会在顶部看到一个横幅，其中显示消息“你的统一 SIEM 和 XDR 已准备就绪”**。 选择“开始搜寻”按钮****。

1. 在“高级搜寻”中，应会看到一条消息：“从 Microsoft Sentinel 浏览内容”。** 在“高级搜寻”导航菜单中，可以在相应选项卡下找到 Microsoft Sentinel 表、函数和查询。****

1. 在“架构”选项卡下，向下滚动到“Microsoft Sentinel”标题，然后双击 ThreatIntelligenceIndicator 表。************

1. 在“查询”窗格中，应会看到返回威胁情报指示器的 (KQL) 查询。** 选择“运行查询”按钮。****

1. 此时“结果”窗格中应会显示返回的结果。**

1. 展开左侧主菜单窗格（如果已折叠）并展开新的 Microsoft Sentinel**** 菜单项。 你应会看到“搜索”、“威胁管理”、“内容管理”和“配置”等选项。********

    >**注意：** 请注意，Azure Microsoft Sentinel 门户和 Microsoft Defender XDR Sentinel 门户之间存在功能差异 **[门户功能差异](https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-defender-portal#capability-differences-between-portals)**。

1. 从 Microsoft Defender XDR 的“Microsoft Sentinel”菜单项中，依次选择“配置”和“数据连接器”。************

1. 在“数据连接器”页中，应会看到已列出的“Azure 活动”和其他数据连接器，并显示为“已连接”状态。**********

>**注意：** 欢迎你自由探索并比较 Microsoft Sentinel 的其他功能，但由于这是一个模拟环境，你在 Microsoft Defender 门户中对 Microsoft Sentinel 的探索是受限的。 在实际环境中，你可以在 Microsoft Defender 门户中浏览 Microsoft Sentinel 的所有功能。

## 你已完成本实验室 - 请继续进入学习路径 9 - 实验室 1 - 练习 1 - 修改 Microsoft 安全规则
