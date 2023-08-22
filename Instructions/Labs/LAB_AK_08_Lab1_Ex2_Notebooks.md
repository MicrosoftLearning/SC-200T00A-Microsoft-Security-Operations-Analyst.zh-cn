---
lab:
  title: 练习 2 - 使用 Notebook 通过 Microsoft Sentinel 进行威胁搜寻
  module: Learning Path 8 - Perform threat hunting in Microsoft Sentinel
---

# 学习路径 8 - 实验室 1 - 练习 2 - 通过 Microsoft Sentinel 使用 Notebook 进行威胁搜寻

## 实验室方案

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要探索通过 Microsoft Sentinel 笔记本进行威胁搜寻的好处。 可以使用笔记本来：

- 执行 Microsoft Sentinel 中未直接提供的分析，例如一些 Python 机器学习功能。
- 创建 Microsoft Sentinel 中未直接提供的数据可视化，例如自定义时间线和流程树。
- 集成 Microsoft Sentinel 外部的数据源（例如，本地数据集）。

>                **注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Hunt%20for%20threats%20using%20notebooks%20in%20Microsoft%20Sentinel)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。 

### 任务 1：探索笔记本

在此任务中，你将探索在 Microsoft Sentinel 中使用笔记本。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 在 Microsoft Sentinel 工作区的“威胁管理”区域下，选择 Notebooks。

1. 接下来，需要创建 AzureML 工作区。 选择“配置 Azure 机器学习”，然后在命令栏中选择“创建新的 Azure ML 工作区”按钮 。

1. 在“订阅”框中，选择自己的订阅。

1. 为资源组选择“新建”，输入“RG-MachineLearning”作为名称，然后选择“确定”。 

1. 在“工作区详细信息”部分中，执行以下任务：

     - 为工作区指定唯一的名称。
     - 将“区域”的默认值保留为“美国东部”。
     - 保存默认的“存储帐户”、“密钥保管库”和“应用程序见解”信息。
     - “容器注册表”选项可以保留为“无”。

1. 在页面底部，选择“查看 + 创建”。 当看到“验证通过”消息时，选择“创建”。 

     >**注意：** 部署机器学习工作区可能需要几分钟时间。

1. 显示“部署已完成”消息后，返回 Microsoft Sentinel 门户。

1. 再次选择 Notebooks，然后在中间命令栏中选择“模板”选项卡 。 

1. 选择“Microsoft Sentinel ML Notebooks 入门指南”。 

1. 在右侧窗格中，向下滚动并选择“从模板创建”按钮。 查看默认选项，然后选择“保存”。

1. 保存完成后，选择“启动笔记本”按钮。 这会将你带至 Microsoft Azure 机器学习工作室。

1. 如果 Microsoft Azure 机器学习工作室中显示信息窗口，请选择“关闭”。

1. 在命令栏中的“计算实例:”选择器的右侧，选择 + 符号，创建新的计算实例 。 提示：它可能隐藏在省略号图标 (...) 中 。

     >注意：可以通过选择左上角的 3 条线来隐藏 Azure ML Studio 左侧边栏选项卡，选择 << 图标来隐藏 Notebooks 文件，以此获得更多屏幕空间 。

1. 在“计算名称”字段中输入唯一名称。 这将标识你的计算实例。

1. 向下滚动并选择第一个可用选项。 提示：工作负载类型：笔记本开发和轻型测试。

1. 选择屏幕底部的“创建”按钮。 关闭可能显示的任何反馈窗口。 这将需要几分钟时间，完成后你将看到一条通知（铃铛图标），计算实例左侧图标从蓝色变为绿色。

1. 创建并运行计算后，请验证要使用的内核是否为 Python 3.8 - AzureML。 提示：这显示在命令栏的右侧。

1. 选择“身份验证”按钮并等待身份验证完成。

1. 通过从命令栏中选择“清除所有输出”图标，清除笔记本中的所有结果，然后按照“入门”教程进行操作。 提示：这可通过从命令栏中选择省略号 (...) 来找到。

>注意：如果无法完成上述步骤来访问 Notebooks，可以改为根据其 GitHub 查看者页面进行操作。 [Azure ML Notebooks 和 Microsoft Sentinel 入门](https://nbviewer.org/github/Azure/Azure-Sentinel-Notebooks/blob/master/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## 你已完成本实验室。
