---
lab:
  title: 练习 1 - 配置 Microsoft Sentinel 环境
  module: Learning Path 5 - Configure your Microsoft Sentinel environment
---

# 学习路径 5 - 实验室 1 - 练习 1 - 配置 Microsoft Sentinel 环境

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod5_L1_Ex1.png)

你是一位安全运营分析师，你所在公司正在实现 Microsoft Sentinel。 你负责设置满足公司要求的 Microsoft Sentinel 环境，并最大程度降低成本、符合法规要求，同时为安全团队提供最易于管理的环境，以便其履行日常工作职责。

>**注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Configure%20your%20Microsoft%20Sentinel%20environment)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。 


### 任务 1：初始化 Microsoft Sentinel 工作区

在此任务中，你将创建 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。  

1. 打开 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择“+ 新建”。

1. 接下来，选择之前创建的 Log Analytics 工作区（例如 uniquenameDefender），然后选择“添加”。 激活可能需要几分钟的时间。

    >**注意：** 如果在此处未看到 Log Analytics 工作区，请参阅模块 3 练习 1 任务 2 以创建一个工作区。

1. 在 Microsoft Sentinel 中，你应处于“常规”部分的“资讯与指南”中，并看到一个声明“Microsoft Sentinel 免费试用版已激活”的通知************。 按 **“确认”** 按钮。

1. 浏览新建的 Microsoft Sentinel 工作区以熟悉用户界面选项。

### 任务 2：创建监视列表

在此任务中，你将在 Microsoft Sentinel 中创建监视列表。

1. 在 Windows 10 屏幕底部的搜索框中，输入“记事本”。 从结果中选择“记事本”。

1. 键入“主机名”，然后输入新行。

1. 从记事本的第 2 行复制以下主机名，每个主机名位于不同的行中：

    ```Notepad
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. 从菜单中选择“文件”-“另存为”，将文件命名为“HighValue.csv”，将文件类型更改为“所有文件”(.)，然后选择“保存”。 提示：文件可保存在 Documents 文件夹中。

1. 关闭记事本。

1. 在 Microsoft Sentinel 中的“配置”区域下，选择“监视列表”选项。

1. 从命令栏中选择“+ 新建”。

1. 在 Watchlist 向导中，输入以下内容：

    |常规设置|值|
    |---|---|
    |名称|HighValueHosts|
    |说明|高价值主机|
    |监视列表别名|HighValueHosts|

1. 选择“下一步:源 >”。

1. 选择“上传文件”下的“浏览文件”，然后浏览刚创建的 HighValue.csv 文件 。

1. 在“SearchKey”字段中，选择“主机名”。

1. 选择“下一页:查看和创建 >”。

1. 检查输入的设置，然后选择“创建”。

1. 屏幕返回到“监视列表”页。

1. 选择“HighValueHosts”监视列表，然后在右窗格上，选择“在日志中查看”。

    >重要提示：监视列表可能需要长达十分钟才能显示。 请继续执行以下任务，并在下一个实验室上运行此命令。
    
    >**注意：** 现在，可以在自己的 KQL 语句中使用 _GetWatchlist('HighValueHosts') 来访问列表。 要引用的列将是主机名。

1. 通过选择右上方的“x”关闭“日志”窗口，然后选择“确定”以放弃未保存的编辑。


### 任务 3：创建威胁指标

在此任务中，你将在 Microsoft Sentinel 中创建指标。

1. 在 Microsoft Sentinel 中，在“威胁管理”区域中选择“威胁智能”选项。

1. 从命令栏中选择“+ 新增”。

1. 查看“类型”下拉列表中的各种指标类型。 选择“domain-name”。 

1. 对于“域”，请输入域名，例如键入 contoso.com。

1. 对于“威胁类型”，请选择“+ 添加”，然后键入“恶意活动”。 选择“应用”。

1. 输入“说明”

1. 对于“名称”，输入用于域的同一个值。

1. 将“有效期开始时间”字段设置为当天日期。

1. 选择“应用”。

1. 在“常规”区域下选择“日志”选项。 你可能希望禁用“始终显示查询”选项，并关闭“查询”窗口以运行 KQL 语句。

1. 运行以下 KQL 语句。

    ```KQL
    ThreatIntelligenceIndicator
    ```

    >注意：指标可能需要长达五分钟的时间才能显示。

1. 向右滚动结果以查看“DomainName”列。 还可以运行以下 KQL 语句，这样就可以仅查看“DomainName”列。 

    ```KQL
    ThreatIntelligenceIndicator 
    | project DomainName
    ```


### 任务 4：配置日志保留期

在此任务中，将更改 SecurityEvent 表的保持期。

1. 在 Microsoft Sentinel 的“配置”区域下，选择“设置”选项。

1. 选择“工作区设置”。

1. 在 Log Analytics 工作区的“设置”区域下，选择“表”选项。

1. 搜索并选择 SecurityEvent 表，然后选择省略号按钮 (...)。

1. 选择“管理表”。

1. 为“总保持期”选择“180 天”。 请注意，“存档期”仅 150 天，因为它从（默认）“交互保留期”开始使用 30 天 。

1. 选择“保存”应用所做的更改。


## 你已完成本实验室。
