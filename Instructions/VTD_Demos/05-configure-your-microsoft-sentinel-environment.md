# <a name="module-5-configure-your-microsoft-sentinel-environment"></a>模块 5 配置 Microsoft Sentinel 环境

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="explore-the-microsoft-sentinel-interface"></a>浏览 Microsoft Sentinel 界面

1. 完成[先决条件部分](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4)后，返回到之前创建的 Microsoft Sentinel 实例。

1. 浏览新建的 Microsoft Sentinel 工作区以熟悉用户界面选项。

## <a name="create-a-watchlist"></a>创建 Watchlist。

在此任务中，你将创建一个 Watchlist。

1. In the search box at the bottom of the screen, enter <ph id="ph1">`Notepad`</ph>.  Select <bpt id="p1">**</bpt>Notepad<ept id="p1">**</ept> from the results.

1. 键入 `Hostname`，然后输入新行。

1. 在第 2 行到第 6 行中，添加以下主机名：
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, <bpt id="p1">**</bpt>File - Save As<ept id="p1">**</ept>, Name the file <ph id="ph1">`HighValue.csv`</ph>.  Then change the file type to <bpt id="p1">**</bpt>All files(<bpt id="p2">*</bpt>.<ept id="p2">*</ept>)<ept id="p1">**</ept>.  Then select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.

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

1. Select your new watchlist.  On the right tab, select <bpt id="p1">**</bpt>View in Log Analytics<ept id="p1">**</ept>.

1. 以下 KQL 语句将自动执行，并显示结果。

```KQL
_GetWatchlist('HighValueHosts')
```
备注：这可能需要一分钟时间才能完成。

You can now use the _GetWatchlist('HighValueHosts') in your own KQL statements to access the list. The column to reference would be <bpt id="p1">*</bpt>Hostname<ept id="p1">*</ept>.

## <a name="create-a-threat-indicator"></a>创建威胁指标。

在此任务中，你将创建一个指标。

1. 在 Microsoft Sentinel 中的“威胁管理”区域中，选择“威胁智能”选项 。

1. 从命令栏选择“新增”。

1. Review the different indicator types available in the Types dropdown.  Then select <bpt id="p1">**</bpt>domain-name<ept id="p1">**</ept>. Enter your initials in the Domain box. An example would be fmg.com.

1. 对于威胁类型，请选择“+ 添加”，然后复制“恶意活动”并将其粘贴到字段中。

1. For the name, enter the same value used for the Domain. An example would be fmg.com.

1. 将“有效期开始时间”字段设置为当天日期。

1. 选择“应用”。

备注：设置可能需要一分钟时间才能显示。

1. Select <bpt id="p1">**</bpt>Logs<ept id="p1">**</ept> option in the General area.  You may have to disable the "Always show queries" option to get to the query window.

1. 运行以下 KQL 语句。

```KQL
ThreatIntelligenceIndicator 
```
Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column.  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>你已完成本演示。