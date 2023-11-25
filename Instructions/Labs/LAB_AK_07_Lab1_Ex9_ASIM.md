---
lab:
  title: 练习 9 - 创建 ASIM 分析程序
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 7 - 实验室 1 - 练习 9 - 部署 ASIM 分析程序

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 需要为特定 Windows 注册表事件建模 ASIM 分析程序。 这些简化分析程序将在稍后按照[高级安全信息模型 (ASIM) 注册表事件规范化架构参考](https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema)来完成。


>**注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20Advanced%20Security%20Information%20Model%20Parsers)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。 


### 任务 1：部署注册表架构 ASIM 分析程序。 

在此任务中，你将从 Microsoft Sentinel GitHub 存储库部署注册表架构分析程序。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在页面左侧的“内容管理”区域下，选择“社区”页。

1. 在右窗格中，选择“加入社区内容”链接。 这会在 Microsoft Edge 浏览器中打开一个新选项卡展示 Microsoft Sentinel GitHub 内容。 提示：可能需要向右滚动才能看到链接。 或者，请改为单击以下链接：[GitHub 上的 Microsoft Sentinel](https://github.com/Azure/Azure-Sentinel)。

1. 选择 ASIM 文件夹。 在这里，你可以部署包含所有 ASIM 分析程序的模板，但我们仅重点介绍注册表架构。

1. 向下滚动，在“注册表”旁边，选择“部署到 Azure ”按钮 。

1. 对于“资源组”，请选择 Sentinel 工作区所在的 RG-Defender。

1. 对于“工作区”，请键入 Sentinel 工作区名称，例如 uniquenameDefender 。

1. 保留其他默认值，然后选择“查看 + 创建”。

1. 选择“创建”以部署模板。 注意不同资源的名称。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在“常规”左侧菜单下选择“日志”。

1. 根据需要选择 >>，打开“架构和筛选器”边栏选项卡。

1. 选择“函数”选项卡（在“表”和“查询”选项卡旁边）。 提示：可能需要选择省略号图标 (...) 才能选择该选项卡 。

1. 展开“工作区函数”。 注意，名称对应于你刚刚部署的模板。

1. 将鼠标悬停在 vimRegistryEventMicrosoftSecurityEvents 工作区分析程序上，然后选择“加载函数代码”。

1. 查看正在分析事件 ID 4657 的 KQL，以简化对 Microsoft Sentinel 工作区中的数据的分析。

1. 运行查询。 不应获得任何结果或错误，它仅用于验证目的。

1. 返回到“架构和筛选器”边栏选项卡，现在将鼠标悬停到 inRegistry 统一分析程序上，然后选择“加载函数代码”。

1. 注意，统一分析程序使用 union 运算符一次运行所有工作区分析程序。 如果为注册表架构开发分析程序，则需要在此处添加它。

1. 运行查询。 不应获得任何结果或错误，它仅用于验证目的。

1. 此统一分析程序现在可用于 Analytics 规则或搜寻查询。


## 继续完成练习 10

