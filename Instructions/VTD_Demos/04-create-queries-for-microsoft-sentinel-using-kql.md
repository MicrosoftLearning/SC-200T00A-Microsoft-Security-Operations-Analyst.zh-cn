# 模块 4 使用 Kusto 查询语言 (KQL) 为 Microsoft Sentinel 创建查询

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## 访问 KQL 测试区域

在此任务中，你将访问 Log Analytics 环境，可在其中练习编写 KQL 语句。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在浏览器中转到 https://aka.ms/lademo。 使用 MOD 管理员凭据登录。 

1. 浏览屏幕左侧选项卡中列出的可用表。

1. 在查询编辑器中，输入以下查询，然后选择“运行”按钮。  你应该会在底部窗口中看到查询结果。

    ```KQL
    SecurityEvent
    ```

1. 在第一条记录旁边，选择“>”以展开该行的信息。

### 任务 2：运行基本的 KQL 语句

在此任务中，你将生成基本的 KQL 语句。

1. `search` 运算符提供了多表/多列搜索体验。 下面的查询演示了 `search` 运算符的用法。

```KQL
search "err" 

search in (SecurityEvent,SecurityAlert,A*) "err"
```

1. `where` 运算符可筛选表来获取满足谓词的行子集。 下面的查询演示了 `where` 运算符的用法。

```KQL
SecurityEvent | where EventID in (4624, 4625)

SecurityEvent 
| where TimeGenerated > ago(1d) 

SecurityEvent 
| where TimeGenerated > ago(1h) and EventID == "4624" 

SecurityEvent 
| where TimeGenerated > ago(1h) 
| where EventID == 4624 
| where AccountType =~ "user" 
```

1. 下面的语句演示了如何使用 `let` 语句来声明变量。 在“查询”窗口中，输入以下语句，然后选择“运行”： 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. 以下语句演示了如何使用 `let` 语句来声明动态列表。 在查询窗口中，输入以下语句，然后选择“运行”： 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. 以下语句演示了查询窗口中显示的在所有表和列中搜索查询时间范围内的记录。 在运行此脚本之前，在查询窗口中，将时间范围更改为“过去一小时”。 输入以下语句并选择“运行”：

```KQL
search "err"
```

**警告：** 请务必在后续脚本中将时间范围改回“过去 24 小时”。

### 使用 Render 运算符以 KQL 创建可视化效果

在此任务中，你将使用 KQL 语句生成可视化效果。

1. 以下语句演示了使用条形图直观呈现结果的 render 函数。 在查询窗口中， 输入以下语句并选择“运行”： 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

1. 以下语句演示了使用时序直观呈现结果的 render 函数。

bin() 函数将值向下舍入为给定装箱大小的整数倍数。  经常与汇总依据一起使用…如果你有一组分散的值，则这些值将分组为更小的一组特定值。  将生成的时序和 render 运算符的管道与一种时间图表类型结合，可以提供时序可视化效果。 在查询窗口中， 输入以下语句并选择“运行”： 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## 你已完成本演示
