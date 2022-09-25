# <a name="module-4-create-queries-for-microsoft-sentinel-using-kusto-query-language-kql"></a>模块 4 使用 Kusto 查询语言 (KQL) 为 Microsoft Sentinel 创建查询

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="access-the-kql-testing-area"></a>访问 KQL 测试区域。

在此任务中，你将访问 Log Analytics 环境，可在其中练习编写 KQL 语句。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. Go to <ph id="ph1">https://aka.ms/lademo</ph> in your browser. Login with the MOD Administrator credentials. 

3. 浏览屏幕左侧选项卡中列出的可用表。

4. In the query editor, enter the following query and select the Run button.  You should see the query results in the bottom window.

    ```KQL
    SecurityEvent
    ```

5. 在第一条记录旁边，选择“>”以展开该行的信息。

### <a name="task-2-run-basic-kql-statements"></a>任务 2：运行基本的 KQL 语句

在此任务中，你将生成基本的 KQL 语句。

1. The following statement demonstrates the use of the let statement to declare variables. In the Query Window, enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 


```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. The following statement demonstrates the use of the let statement to declare a dynamic list. In the Query Window enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 


```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. The following statement demonstrates searching across all tables and columns for records within the query time range display in the query window. In the Query Window before running this script change the Time range to "Last hour". Enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 

```KQL
search "err"
```

**警告：** 请务必在后续脚本中将时间范围改回“过去 24 小时”。

### <a name="create-visualizations-in-kql-with-the-render-operator"></a>使用 Render 运算符以 KQL 创建可视化效果

在此任务中，你将使用 KQL 语句生成可视化效果。

1. The following statement demonstrates the render function visualizing results with a barchart. In the Query Window. Enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 以下语句演示了使用时序直观呈现结果的 render 函数。

在浏览器中转到 https://aka.ms/lademo。 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## <a name="you-have-completed-the-demo"></a>你已完成本演示。

