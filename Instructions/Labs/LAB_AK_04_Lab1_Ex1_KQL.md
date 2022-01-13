---
lab:
    title: '练习 1 - 使用 Kusto 查询语言 (KQL) 为 Microsoft Sentinel 创建查询'
    module: '模块 4 - 使用 Kusto 查询语言 (KQL) 为 Microsoft Sentinel 创建查询'
---

# 模块 4 - 实验室 1 - 练习 1 - 使用 Kusto 查询语言 (KQL) 为 Microsoft Sentinel 创建查询

## 实验室场景
你是一位安全运营分析师，你所在公司正在实现 Microsoft Sentinel。你负责执行日志数据分析，以便搜索恶意活动、显示可视化效果并执行威胁搜寻。为了查询日志数据，你使用 Kusto 查询语言 (KQL)。

>**提示**：此实验室需要将大量 KQL 脚本输入到 Microsoft Sentinel 中。这些脚本是在本实验室开始时以文件形式提供的。也可在以下位置下载它们：  https://github.com/MicrosoftLearning/SC-200T00CN-Microsoft-Security-Operations-Analyst/tree/master/Allfiles


### 任务 1：访问 KQL 测试区域。

在此任务中，你将访问 Log Analytics 环境，可在其中练习编写 KQL 语句。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 在浏览器中转到 https://aka.ms/lademo。 使用 MOD 管理员凭据登录。 

3. 浏览屏幕左侧选项卡中列出的可用表。

4. 在查询编辑器中，输入以下查询，然后选择“**运行**”按钮。  你应该会在底部窗口中看到查询结果。

```KQL
SecurityEvent
```

5. 在第一条记录旁边，选择 **“>”** 以展开该行的信息。


### 任务 2：运行基本的 KQL 语句

在此任务中，你将生成基本的 KQL 语句。

>**重要提示：** 对于每个查询，都应先从查询窗口中清除之前的语句，或是在最后打开的选项卡之后选择“**+**”打开一个新的查询窗口（最多 25 个）。

1. 下面的语句演示了将 let 语句用于声明变量的用法。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

2. 以下语句演示了将 let 语句用于声明动态列表的用法。在查询窗口中，输入以下语句，然后选择 **“运行”**： 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

3. 以下语句演示了将 let 语句用于声明动态表的用法。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
let LowActivityAccounts =
    SecurityEvent 
    | summarize cnt = count() by Account 
    | where cnt < 10;
LowActivityAccounts | where Account contains "sql"
```

4. 以下语句演示了查询窗口中显示的在所有表和列中搜索查询时间范围内的记录。运行此脚本前，在查询窗口中将“时间范围”更改为“**过去 1 小时**”。输入以下语句并选择“**运行**”： 

```KQL
search "err"
```

>**警告：** 请务必在后续脚本中将时间范围改回“过去 24 小时”。

5. 以下语句演示了查询窗口中显示的在所有通过“in”子句中列出的表中搜索查询时间范围内的记录。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
search in (SecurityEvent,SecurityAlert,A*) "err"
```

6. 以下语句演示了使用 where 运算符的筛选器。在查询窗口中，输入以下语句并选择 **“运行”**： 

    >**备注：** 在下面的每个代码块中输入查询后，你应该“运行”。

```KQL
SecurityEvent
| where TimeGenerated > ago(1d)
```

```KQL
SecurityEvent
| where TimeGenerated > ago(1h) and EventID == "4624"
```

```KQL
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4624
| where AccountType =~ "user"
```

```KQL
SecurityEvent | where EventID in (4624, 4625)
```

7. 以下语句演示了在查询窗口中使用 extend 运算符创建字段的方法。输入以下语句并选择 **“运行”**： 

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
```

8. 以下语句演示了如何使用 order by 运算符对结果进行排序。在查询窗口中，输入以下语句并选择“**运行**”： 

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
| order by severityOrder desc
```

9. 以下语句演示了使用项目运算符为结果集指定字段。

    >**备注：** 在下面的每个代码块中输入查询后，你应该“运行”。

在查询窗口中，输入以下语句并选择“**运行**”： 

```KQL
SecurityEvent
| project Computer, Account
```

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
| order by severityOrder
| project-away severityOrder
```


### 任务 3： 使用 Summarize 运算符分析 KQL 中的结果

在此任务中，你将生成 KQL 语句来准备数据。

1. 以下语句演示了 count 函数。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent
| where EventID == "4688"
| summarize count() by Process, Computer
```

2. 以下语句演示了 count 函数。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4624
| summarize cnt=count() by AccountType, Computer
```

3. 以下语句演示了 dcount 函数。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent
| summarize dcount(IpAddress)
```

4. 以下语句演示了 arg_max 函数。

以下语句将返回计算机 SQL12.NA.contosohotels.com 的 SecurityEvent 表中的最新行。  arg_max 函数中的 * 请求该行的所有列。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent 
| where Computer == "SQL12.na.contosohotels.com"
| summarize arg_max(TimeGenerated,*) by Computer
```

5. 以下语句演示了 arg_min 函数。

在此语句中，计算机 SQL12.NA.contosohotels.com 的最早 SecurityEvent 将作为结果集返回。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent 
| where Computer == "SQL12.na.contosohotels.com"
| summarize arg_min(TimeGenerated,*) by Computer
```

6. 以下语句演示了根据竖线“|”顺序理解结果的重要性。在查询窗口中，输入以下查询并分别运行： 

“**查询 1**”将提供最后一次活动为“登录”的帐户。首先汇总 SecurityEvent 表并返回每个帐户的最新行。  然后，将只返回 EventID 等于 4624（登录）的行。

```KQL
SecurityEvent
| summarize arg_max(TimeGenerated, *) by Account
| where EventID == "4624"
```

“**查询 2**”将提供已登录帐户的最新登录信息。将对 SecurityEvent 表进行筛选，使其仅包含 EventID = 4624。然后，将按帐户为最新登录行汇总这些结果。

```KQL
SecurityEvent
| where EventID == "4624"
| summarize arg_max(TimeGenerated, *) by Account
```

>**备注：** 也可以通过选择“已完成”栏来查看“总 CPU”和“用于已处理查询的数据”，并对两种语句之间的数据进行比较。

7. 以下语句演示了 make_list 函数。

make_list 函数返回一个动态 (JSON) 数组，该数组由组中表达式的所有值组成。此 KQL 查询将首先使用 where 运算符筛选 EventID。  接下来，对于每台计算机，结果都是帐户的 JSON 数组。生成的 JSON 数组将包含重复的帐户。

在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent
| where EventID == "4624"
| summarize make_list(Account) by Computer
```

8. 以下语句演示了 make_set 函数。

make_set 函数返回一个动态 (JSON) 数组，该数组中包含表达式在组中采用的不同值。此 KQL 查询将首先使用 where 运算符筛选 EventID。  接下来，对于每台计算机，结果都是唯一帐户的 JSON 数组。在查询窗口中，输入以下语句并选择“**运行**”： 

```KQL
SecurityEvent
| where EventID == "4624"
| summarize make_set(Account) by Computer
```


### 任务 4： 使用 Render 运算符以 KQL 创建可视化效果

在此任务中，你将使用 KQL 语句生成可视化效果。

1. 以下语句演示了使用条形图直观呈现结果的 render 函数。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 以下语句演示了使用时序直观呈现结果的 render 函数。

bin() 函数将值向下舍入为给定装箱大小的整数倍数。  经常与汇总依据一起使用…如果你有一组分散的值，则这些值将分组为更小的一组特定值。  将生成的时序和 render 运算符的管道与一种时间图表类型结合，可以提供时序可视化效果。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1h) 
| render timechart
```


### 任务 5： 使用 KQL 生成多表语句

在此任务中，你将生成多表 KQL 语句。

1. 以下语句演示了 union 运算符，该运算符采用两个或多个表，并返回所有表的行。有必要了解结果是如何通过竖线字符传递的，又是如何受到该字符影响的。在查询窗口中，输入以下语句，并分别针对每个语句选择“**运行**”以查看结果： 

“**查询 1**”将返回 SecurityEvent 和 SecurityAlert 的所有行。

```KQL
SecurityEvent 
| union SecurityAlert  
```

“**查询 2**”将返回一行和一列，即 SecurityEvent 和 SecurityAlert 的所有行的计数。

```KQL
SecurityEvent 
| union SecurityAlert  
| summarize count() 
| project count_
```

“**查询 3**”将返回 SecurityEvent 的所有行和 SecurityAlert 的其中一行。  SecurityAlert 的行将具有 SecurityAlert 行的计数。

```KQL
SecurityEvent 
| union (SecurityAlert  | summarize count()) 
| project count_
```

2. 以下语句演示了 union 运算符对通配符的支持，以联合多个表。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
union Security* 
| summarize count() by Type
```

3. 以下语句演示了 join 运算符，该运算符通过匹配每个表中指定列的值来合并两个表的行以形成新表。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
SecurityEvent 
| where EventID == "4624" 
| summarize LogOnCount=count() by EventID, Account 
| project LogOnCount, Account 
| join kind = inner (
     SecurityEvent 
     | where EventID == "4634" 
     | summarize LogOffCount=count() by EventID, Account 
     | project LogOffCount, Account 
) on Account
```

联接中指定的第一个表被看作是左表。  联接关键字后面的表被看作是右表。  处理表中的列时，名称 $left.Column 和 $right.Column 用于区分正在引用哪个表的列。 


### 任务 6：使用 KQL 处理字符串数据

在此任务中，你将使用 KQL 语句处理结构化和非结构化的字符串字段。

1. 以下语句演示了 extract 函数。  extract 从文本字符串中获取正则表达式的匹配项。可以选择将提取的子字符串转换为指定的类型。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
print extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"
```

2. 以下语句使用 extract 函数从 SecurityEvent 表的“帐户”字段中提取“帐户名称”。在查询窗口中，输入以下语句并选择 **“运行”**： 

```KQL
let top3 = SecurityEvent
| where TimeGenerated > ago(1h)
| where AccountType == 'User'
| extend Account_Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
| summarize Attempts = count() by Account_Name
| where Account_Name != ""
| top 3 by Attempts 
| summarize make_list(Account_Name);
SecurityEvent
| where TimeGenerated > ago(1h)
| where AccountType == 'User'
| extend Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
| extend Account_Name = iff(Name in (top3), Name, "Other")
| where Account_Name != ""
| summarize Attempts = count() by Account_Name
| sort by Attempts
```

3. 以下语句演示了 parse 函数。计算字符串表达式并将其值分析为一个或多个计算列。对于未成功分析的字符串，计算列的值将为 null。

```KQL
let Traces = datatable(EventText:string)
[
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=23, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=15, lockTime=02/17/2016 08:40:00, releaseTime=02/17/2016 08:40:00, previousLockTime=02/17/2016 08:39:00)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=20, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=22, lockTime=02/17/2016 08:41:01, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 08:41:00, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:00)"
];
Traces  
| parse EventText with * "resourceName=" resourceName ", totalSlices=" totalSlices:long * "sliceNumber=" sliceNumber:long * "lockTime=" lockTime ", releaseTime=" releaseTime:date "," * "previousLockTime=" previousLockTime:date ")" *  
| project resourceName, totalSlices, sliceNumber, lockTime, releaseTime, previousLockTime
```

4. 以下语句演示了如何使用动态字段：

Log Analytics 表中有一个定义为“动态”的字段类型。动态字段包含键值对。

若要访问动态字段中的字符串，请使用点表示法。AppAvailabilityResults 表中的“属性”字段属于动态类型。在此示例中，可以使用 Properties.SyntheticMonitorId 字段名称访问 SyntheticMonitorId。

在查询窗口中，输入以下语句并**运行**： 

```KQL
AppAvailabilityResults
| project Properties.SyntheticMonitorId
```

5. 以下语句演示了用于操作存储在字符串字段中的 JSON 的函数。许多日志以 JSON 格式提交数据，这要求了解如何将 JSON 数据转换为可查询字段。 

在查询窗口中，分别输入以下语句并选择 **“运行”**： 

```KQL
SecurityAlert
| extend ExtendedProperties = todynamic(ExtendedProperties) 
| extend ActionTaken = ExtendedProperties.ActionTaken
| extend AttackerIP = ExtendedProperties["Attacker IP"]
```
mv-expand 运算符将多值动态数组或属性包扩展为多个记录。

```KQL
SecurityAlert
| mv-expand entity = todynamic(Entities)
```
mv-apply 运算符对每个记录应用一个子查询，并返回所有子查询结果的并集。

```KQL
SecurityAlert
| where TimeGenerated >= ago(7d)
| mv-apply entity = todynamic(Entities) on 
( where entity.Type == "account" | extend account = strcat (entity.NTDomain, "\\", entity.Name))
```

6. 若要创建函数：

    >**备注：** 在用于本实验室中数据的 lademo 环境中，你将无法执行此操作，但这是你的环境中要使用的重要概念。 

运行查询后，选择“**保存**”按钮，然后从下拉列表中选择“**另存为函数**”。输入所需的名称，例如：在“**函数名称**”框中输入“*MailboxForward*”，然后输入一个旧类别（例如“*常规*”），再选择“**保存**”。

通过使用函数别名，该功能将以 KQL 提供：

```KQL
MailboxForward
```

## 你已完成本实验室。
