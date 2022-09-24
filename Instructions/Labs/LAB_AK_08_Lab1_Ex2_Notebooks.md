---
lab:
  title: 练习 2 - 使用 Notebook 通过 Microsoft Sentinel 进行威胁搜寻
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-2---threat-hunting-using-notebooks-with-microsoft-sentinel"></a>模块 8 - 实验室 1 - 练习 2 - 使用 Microsoft Sentinel 的 Notebook 进行威胁搜寻

## <a name="lab-scenario"></a>实验室方案



You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You need to explore the benefits of threat hunting with Microsoft Sentinel Notebooks. You can use notebooks to:

- 执行 Microsoft Sentinel 中未直接提供的分析，例如一些 Python 机器学习功能。
- 创建 Microsoft Sentinel 中未直接提供的数据可视化，例如自定义时间线和流程树。
- 集成 Microsoft Sentinel 外部的数据源（例如，本地数据集）。


### <a name="task-1-explore-notebooks"></a>任务 1：探索笔记本

在此任务中，你将探索在 Microsoft Sentinel 中使用笔记本。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 在 Microsoft Sentinel 工作区中，选择“笔记本”。

1. Next, you need to create an AzureML Workspace. Select <bpt id="p1">**</bpt>Configure Azure Machine Learning<ept id="p1">**</ept> and then select <bpt id="p2">**</bpt>Create new Azure ML workspace<ept id="p2">**</ept> button in the command bar.

1. 在“订阅”框中，选择自己的订阅。

1. 为资源组选择“新建”，输入“RG-MachineLearning”作为名称，然后选择“确定”。 

1. 在“工作区详细信息”部分中，执行以下任务：

     - 为工作区指定唯一的名称。
     - 将“区域”的默认值保留为“美国东部”。
     - 保存默认的“存储帐户”、“密钥保管库”和“应用程序见解”信息。
     - “容器注册表”选项可以保留为“无”。

1. At the bottom of the page, select <bpt id="p1">**</bpt>Review + create<ept id="p1">**</ept>. When you see the <bpt id="p1">*</bpt>"Validation passed"<ept id="p1">*</ept> message, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>. 

     >**注意：** 部署机器学习工作区可能需要几分钟时间。

1. 显示“部署已完成”消息后，返回 Microsoft Sentinel 门户。

1. 选择“笔记本”，然后从中间命令栏中选择“模板”选项卡 。 

1. 选择“Microsoft Sentinel ML Notebooks 入门指南”。 

1. On the right pane, scroll down and select <bpt id="p1">**</bpt>Create from template<ept id="p1">**</ept> button. Review the default option and select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 如果 Microsoft Azure 机器学习工作室中显示信息窗口，请选择“关闭”。

1. 在命令栏中的“计算: 实例选择器”的右侧，选择“+”符号，创建新的计算实例 。

1. 你需要探索通过 Microsoft Sentinel 笔记本进行威胁搜寻的好处。

1. 可以使用笔记本来：

1. Select the <bpt id="p1">**</bpt>Create<ept id="p1">**</ept> button at the bottom of the screen. Close any feedback window that may appear. This will take a few minutes, you will see a notification (bell icon) when it is done.

1. Once the Compute has been created and running, verify that the kernel to use is <bpt id="p1">*</bpt>Python 3.8 - AzureML<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> This is shown in the right of the command bar. You can also increase your screen size by selecting <bpt id="p1">**</bpt><ph id="ph1">&lt;&lt;</ph><ept id="p1">**</ept> under the <bpt id="p2">*</bpt>Notebooks<ept id="p2">*</ept> menu.

1. 通过从命令栏中选择“橡皮擦”图标，清除笔记本中的所有结果，然后按照“入门”教程进行操作。

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you cannot complete the steps above to access the Notebook, you can follow it on its GitHub page instead. See the notebook file here: <bpt id="p1">[</bpt>Microsoft Sentinel Notebooks on GitHub<ept id="p1">](https://github.com/Azure/Azure-Sentinel-Notebooks/blob/8122bca32387d60a8ee9c058ead9d3ab8f4d61e6/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb)</ept> 

## <a name="you-have-completed-the-lab"></a>你已完成本实验室。
