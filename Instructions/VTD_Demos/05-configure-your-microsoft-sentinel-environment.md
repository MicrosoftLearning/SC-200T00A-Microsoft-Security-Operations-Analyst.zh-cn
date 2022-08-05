---
ms.openlocfilehash: 8b5dbb31b0de6f493d9eb51a4a2e998aa248ce46
ms.sourcegitcommit: c026d30237cf9a0efdc6e7bbc58a395ecbc9e250
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "147449885"
---
# <a name="module-5-configure-your-microsoft-sentinel-environment"></a>模块 5 配置 Microsoft Sentinel 环境

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="explore-the-microsoft-sentinel-interface"></a>浏览 Microsoft Sentinel 界面

1. 完成[先决条件部分](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4)后，返回到之前创建的 Microsoft Sentinel 实例。

1. 浏览新建的 Microsoft Sentinel 工作区以熟悉用户界面选项。

## <a name="create-a-watchlist"></a>创建 Watchlist。

在此任务中，你将创建一个 Watchlist。

1. 在屏幕底部的搜索框中，输入 `Notepad`。  从结果中选择“记事本”。

1. 键入 `Hostname`，然后输入新行。

1. 在第 2 行到第 6 行中，添加以下主机名：
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. 从菜单中依次选择“文件”、“另存为”，将文件命名为 `HighValue.csv`。  然后将文件类型更改为“所有文件”( *.* )。  再选择“保存”。

1. 关闭记事本。

1. 在 Microsoft Sentinel 中的“我的 Watchlist”区域中，选择“Watchlist”选项 。

1. 从命令栏选择“新增”。

1. 在 Watchlist 向导中，输入以下内容：名称：HighValueHosts  Description:High Value Hosts  Watchlist alias:HighValueHosts

1. 选择“下一步:源 >”。

1. 浏览刚刚创建的 `HighValue.csv` 文件。 

1. 加载 CSV 文件后，从“SearchKey 字段”下拉框中选择“主机名” 。

1. 选择“下一页:查看和创建 >”。

1. 选择“创建”。

1. 屏幕返回到 Watchlist 列表。

1. 选择新 watchlist。  在右侧选项卡上，选择“在 Log Analytics 查看”。

1. 以下 KQL 语句将自动执行，并显示结果。

```KQL
_GetWatchlist('HighValueHosts')
```
备注：这可能需要一分钟时间才能完成。

现在，可以在自己的 KQL 语句中使用 _GetWatchlist('HighValueHosts') 来访问列表。 要引用的列将是主机名。

## <a name="create-a-threat-indicator"></a>创建威胁指标。

在此任务中，你将创建一个指标。

1. 在 Microsoft Sentinel 中的“威胁管理”区域中，选择“威胁智能”选项 。

1. 从命令栏选择“新增”。

1. 查看“类型”下拉列表中的各种指标类型。  然后选择“域名”。 在“域”框中输入姓名首字母缩写。 例如 fmg.com。

1. 对于威胁类型，请选择“+ 添加”，然后复制“恶意活动”并将其粘贴到字段中。

1. 对于名称，输入用于域的同一个值。 例如 fmg.com。

1. 将“有效期开始时间”字段设置为当天日期。

1. 选择“应用”。

备注：设置可能需要一分钟时间才能显示。

1. 从“常规”区域选择“日志”选项。  可能必须禁用“始终显示查询”选项才能进入查询窗口。

1. 运行以下 KQL 语句。

```KQL
ThreatIntelligenceIndicator 
```
向右滚动结果以查看“DomainName”列。 还可以运行以下 KQL 语句，这样就可以仅查看“DomainName”列。  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>你已完成本演示。