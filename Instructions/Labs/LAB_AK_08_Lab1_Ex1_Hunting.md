---
lab:
  title: 练习 1 - 在 Microsoft Sentinel 中执行威胁搜寻
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-1---perform-threat-hunting-in-microsoft-sentinel"></a>模块 8 - 实验室 1 - 练习 1 - 在 Azure Sentinel 中执行威胁搜寻

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You have received threat intelligence about a Command and Control (C2 or C&amp;C) technique. You need to perform a hunt and watch for the threat.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The log data used in the lab was created in the previous module. See <bpt id="p1">**</bpt>Attack 3<ept id="p1">**</ept> on WIN1 server in Exercise 5.

>**注意：** 你已在上一模块中体验过探索数据的过程，因此本实验室提供 KQL 语句供你开始操作。 


### <a name="task-1-create-a-hunting-query"></a>任务 1：创建搜寻查询

在此任务中，你将创建搜寻查询、为结果添加书签并创建 Livestream。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 选择“日志” 

1. 在“新查询 1”空间输入以下 KQL 语句：

   >**重要提示：** 请首先将任意 KQL 查询粘贴到记事本，然后从此处复制到“新建查询 1 日志”窗口以避免任何错误。

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize count() by bin(TimeGenerated, 3m), c2
    | where count_ > 5
    | render timechart 
    ```

    ![屏幕快照](../Media/SC200_hunting1.png)

1. The goal of the previous KQL query is to provide a visualization for a C2 beaconing on a consistent basis. Adjust grouping of values by changing the <bpt id="p1">*</bpt>3m<ept id="p1">*</ept> setting to <bpt id="p2">**</bpt>30s<ept id="p2">**</ept> within bin() and <bpt id="p3">**</bpt>Run<ept id="p3">**</ept> the query again.

1. Change it back to <bpt id="p1">*</bpt>3m<ept id="p1">*</ept>. Now change the <bpt id="p1">*</bpt>count_<ept id="p1">*</ept> threshold to <bpt id="p2">**</bpt>10<ept id="p2">**</ept> and <bpt id="p3">**</bpt>Run<ept id="p3">**</ept> the query again to witness the impact.

1. You have now identified DNS requests that are beaconing to a C2 server. Next, determine which devices are beaconing. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL Statement:

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

    ![屏幕快照](../Media/SC200_hunting2.png)

    >**注意：** 生成的日志数据仅来自 WIN1 设备。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 再次选择 Microsoft Sentinel 工作区，并选择“威胁管理”区域下的“搜寻”页。

1. 从命令栏中选择“+ 新建查询”。

1. 在“创建自定义查询”窗口中，为“名称”输入“C2 Hunt” 

1. 对于“自定义查询”，输入以下 KQL 语句：

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

1. 向下滚动，在“实体映射（预览）”下，选择：

    - 对于“实体类型”下拉列表，请选择“Host”。
    - 对于“标识符”下拉列表，选择“HostName”。
    - 对于“值”下拉列表，选择“DeviceName”。

1. 向下滚动，然后在“策略与技术”下选择“命令和控制”，然后选择“创建”以创建搜寻查询 。

1. 在“Microsoft Sentinel - 搜寻”边栏选项卡中，在列表中搜索刚刚创建的查询“C2 Hunt” 。

1. 从列表中选择“C2 Hunt”。

1. 在右窗格中，向下滚动并选择“运行查询”按钮。

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 你收到了关于命令和控制（C2 或 C&C）技术的威胁情报。

1. 选中结果中第一行的复选框。 

1. 在中间的命令栏中，选择“添加书签”按钮。

1. 查看默认填充的值，在“添加书签”边栏选项卡中，选择“创建”。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 返回到 Microsoft Sentinel 门户的“搜寻”页，选择中间窗格中的“书签”选项卡。

1. 从结果列表中选择刚刚创建的“C2 Hunt”书签。

1. 你需要执行搜寻并监视威胁。

1. 像在上一模块中一样浏览调查图。

1. 通过选择窗口右上方的“X”关闭“调查图”窗口，然后选择“确定”以放弃更改 。 

1. 选择“查询”选项卡。

1. 再次搜索并选择“C2 Hunt”查询。

1. Right-click your query and select <bpt id="p1">**</bpt>Add to livestream<ept id="p1">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> This also can be done by sliding right and selecting the ellipsis <bpt id="p2">**</bpt>(...)<ept id="p2">**</ept> at the end of the row to open a context menu.

1. **重要提示：** 本实验室使用的日志数据是在上一个模块中创建的。


### <a name="task-2-create-a-nrt-query-rule"></a>任务 2：创建 NRT 查询规则

请参阅练习 5 中 WIN1 服务器上的攻击 3。


1. 在 Microsoft Sentinel 中选择“分析”页面。 

1. 选择“创建”选项卡，然后选择“NRT 查询规则”
1. This starts the "Analytics rule wizard". For the <bpt id="p1">*</bpt>General<ept id="p1">*</ept> tab type:

    |设置|值|
    |---|---|
    |名称|**NRT C2 搜寻**|
    |说明|**NRT C2 搜寻**|
    |策略|**命令和控制**|
    |Severity|**高**|

1. 选择“下一页:**设置规则逻辑 >”按钮**。 


1. 对于“规则查询”，输入以下 KQL 语句：

    ```KQL
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. 对于“事件设置”选项卡，保留默认值并选择“下一页: “下一步: 自动响应 >”按钮。

1. 对于“自动响应”选项卡，选择“警报自动化”下的“PostMessageTeams-OnAlert”，然后选择“下一页: 审阅”按钮。

1. 在“查看”选项卡上，选择“创建”按钮以新建计划分析规则。



### <a name="task-3-create-a-search"></a>任务 3：创建搜索

在此任务中，你将使用搜索作业查找 C2。 


1. 在 Microsoft Sentinel 中选择“搜索”页。 

1. 选择“还原”选项卡。

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The lab will not have Archived tables to restore from.  The normal process would restore archived tables to include in the Search job.
1. 选择“取消”。
1. 选择“搜索”选项卡。
1. 选择表并更改为“DeviceRegistryEvents”
1. 在搜索框中输入“reg.exe”  
1. 选择“保存的搜索”。 
1. 搜索作业将创建名为“DeviceRegistryEvents_####_SRCH”的新表。 
1. Wait for the search job to complete.  The status will display <bpt id="p1">*</bpt>Updating<ept id="p1">*</ept>. Then <bpt id="p1">*</bpt>In progress<ept id="p1">*</ept>. Then <bpt id="p1">*</bpt>Search completed<ept id="p1">*</ept>. 
1. 选择“查看搜索结果”
1. 在“日志”中打开一个新选项卡。
1. 输入新的表名称“DeviceRegistryEvents_####_SRCH”并运行。

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
