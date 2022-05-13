---
lab:
  title: 练习 1 - 配置 Microsoft Sentinel 环境
  module: Module 5 - Configure your Microsoft Sentinel environment
ms.openlocfilehash: 3dc3670a58758c2d7de37878ba5b9413804596c4
ms.sourcegitcommit: a90325f86a3497319b3dc15ccf49e0396c4bf749
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2022
ms.locfileid: "141493963"
---
# <a name="module-5---lab-1---exercise-1---configure-your-microsoft-sentinel-environment"></a>模块 5 - 实验室 1 - 练习 1 - 配置 Microsoft Sentinel 环境

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod5_L1_Ex1.png)

你是一位安全运营分析师，你所在公司正在实现 Microsoft Sentinel。 你负责设置满足公司要求的 Microsoft Sentinel 环境，并最大程度降低成本、符合法规要求，同时为安全团队提供最易于管理的环境，以便其履行日常工作职责。


### <a name="task-1-initialize-the-microsoft-sentinel-workspace"></a>任务 1：初始化 Microsoft Sentinel 工作区

在此任务中，你将创建 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 打开 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择“+ 新建”。 

1. 接下来，选择之前创建的 Log Analytics 工作区（例如 uniquenameDefender），然后选择“添加”。 激活可能需要几分钟的时间。

    >**注意：** 如果在此处未看到 Log Analytics 工作区，请参阅模块 3 练习 1 任务 2 以创建一个工作区。

1. 浏览新建的 Microsoft Sentinel 工作区以熟悉用户界面选项。


### <a name="task-2-create-a-watchlist"></a>任务 2：创建监视列表

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

1. 从命令栏中选择“+ 添加新增”。

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

1. 选择“HighValueHosts”监视列表，然后在右侧选项卡上，选择“在日志中查看”。

    >**重要提示：** 可能需要一些时间才能显示监视列表。 请继续执行以下任务，并在下一个实验室上运行此命令。
    
    >**注意：** 现在，可以在自己的 KQL 语句中使用 _GetWatchlist('HighValueHosts') 来访问列表。 要引用的列将是主机名。

1. 通过选择右上方的“x”关闭“日志”窗口，然后选择“确定”以放弃未保存的编辑。


### <a name="task-3-create-a-threat-indicator"></a>任务 3：创建威胁指标

在此任务中，你将在 Microsoft Sentinel 中创建指标。

1. 在 Microsoft Sentinel 中，在“威胁管理”区域中选择“威胁智能”选项。

1. 从命令栏中选择“+ 新增”。

1. 查看“类型”下拉列表中的各种指标类型。 选择“domain-name”。 在“域”框中输入姓名首字母缩写。 例如 fmg.com。

1. 对于威胁类型，请选择“恶意活动”。

1. 对于“名称”，输入用于域的同一个值。 例如 fmg.com。

1. 将“有效期开始时间”字段设置为当天日期。

1. 选择“应用”。

1. 在“常规”区域下选择“日志”选项。 你可能希望禁用“始终显示查询”选项，并关闭“查询”窗口以运行 KQL 语句。

1. 运行以下 KQL 语句。

    ```KQL
    ThreatIntelligenceIndicator
    ```

    >**注意：** 设置可能需要几分钟时间才能显示。

1. 向右滚动结果以查看“DomainName”列。 还可以运行以下 KQL 语句，这样就可以仅查看“DomainName”列。 

    ```KQL
    ThreatIntelligenceIndicator | project DomainName
    ```

## <a name="you-have-completed-the-lab"></a>你已完成本实验室。
