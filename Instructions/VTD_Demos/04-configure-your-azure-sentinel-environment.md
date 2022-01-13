# 模块 4 使用 Kusto 查询语言 (KQL) 为 Azure Sentinel 创建查询

**备注**： 能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## 探索 Azure Sentinel 界面

1. 完成[先决条件部分](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4)后，返回到之前创建的 Azure Sentinel 实例。

1. 浏览新建的 Azure Sentinel 工作区以熟悉用户界面选项。

## 创建监视列表。

在此任务中，你将创建一个 watchlist。

1. 在屏幕底部的搜索框中，输入 `Notepad`。  从结果中选择 **“记事本”**。

2. 键入 `Hostname`，然后输入新行。

3. 在第 2 行到第 6 行中，添加以下主机名：
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

4. 从菜单中依次选择 **“文件”、“另存为”**，将文件命名为 `HighValue.csv`。  然后将文件类型更改为 **“所有文件”(*.*)**。  然后选择 **“保存”**。

5. 关闭记事本。

6. 在 Azure Sentinel 中的 **“配置”** 区域，选择 **“Watchlist”** 选项。

7. 从命令栏选择 **“新增”**。

8. 在 Watchlist 向导中，输入以下内容：
    名称： HighValueHosts
    说明：高价值主机
    Watchlist 别名：HighValueHosts

9. 选择 **“下一步: 源 >”**。

10. 浏览刚刚创建的 `HighValue.csv` 文件。 

1. 加载 CSV 文件后，从 **“SearchKey 字段”** 下拉框中选择 **“主机名”**。

11. 选择 **“下一步: 查看并创建 >”**。

12. 选择 **“创建”**。

13. 屏幕返回到 watchlist 列表。

14. 选择新 watchlist。  在右侧选项卡上，选择 **“在 Log Analytics 查看”**。

15. 以下 KQL 语句将自动执行，并显示结果。

```KQL
_GetWatchlist('HighValueHosts')
```
**备注**：这可能需要一分钟时间才能完成。

现在，可以在自己的 KQL 语句中使用 _GetWatchlist('HighValueHosts') 来访问列表。要引用的列将是*主机名*。

## 创建威胁指标。

在此任务中，你将创建一个指标。

1. 在 Azure Sentinel 中的 **“威胁管理”** 区域，选择 **“威胁情报”** 选项。

2. 从命令栏选择 **“新增”**。

3. 在“类型”下拉列表中查看可用的不同指标类型。  然后选择 **“域名”**。在“域”框中输入姓名缩写。例如 fmg.com。

4. 对于威胁类型，请选择 **“恶意活动”**。

5. 对于名称，输入用于域的同一个值。例如 fmg.com。

6. 将 **“有效期开始时间”** 字段设置为当天日期。

7. 选择 **“应用”**。

**备注**：设置可能需要一分钟时间才能显示。

8. 从“常规”区域选择 **“日志”** 选项。  可能必须禁用“始终显示查询”选项才能进入查询窗口。

9. 运行以下 KQL 语句。

```KQL
ThreatIntelligenceIndicator 
```
向右滚动结果以查看“DomainName”列。还可以运行以下 KQL 语句，这样就可以仅查看“DomainName”列。  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## 你已完成本演示。