---
lab:
  title: 练习 7 - 创建检测
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-7---create-detections"></a>模块 7 - 实验室 1 - 练习 7 - 创建检测

## <a name="lab-scenario"></a>实验室方案


You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You are going to work with Log Analytics KQL queries and from there, you will create custom analytics rules to help discover threats and anomalous behaviors in your environment.

分析规则将在你的整个环境中搜索特定事件或事件集，在达到特定事件阈值或条件时发出警报，生成故障事件以供 SOC 进行会审和调查，并通过自动化跟踪和修正流程来响应威胁。


### <a name="task-1-attack-1-detection-with-defender-for-endpoint"></a>任务 1：使用 Defender for Endpoint 检测攻击 1

在此任务中，你将在配置了 Microsoft Defender for Endpoint 的主机上创建针对攻击 1 的检测。

1. 如果你已离开此页面，在 Microsoft Sentinel 门户中，选择“常规”部分中的“日志”。

1. 再次运行以下 KQL 语句，以召回包含此数据的表：

    ```KQL
    search "temp\\startup.bat"
    ```

1. This detection will focus on data from Defender for Endpoint. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL Statement:

    ```KQL
    search in (Device*) "temp\\startup.bat"
    ```

1. The table <bpt id="p1">*</bpt>DeviceRegistryEvents<ept id="p1">*</ept> looks to have the data already normalized and easy for us to query. Expand the row to see all the columns related to the record.

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you do not see the <bpt id="p2">*</bpt>DeviceRegistryEvents<ept id="p2">*</ept> table in the results, an alternative for the following queries is to use the <bpt id="p3">*</bpt>DeviceProcessEvents<ept id="p3">*</ept> table as replacement. Being that said, use one of the two provided examples below.

1. 从结果中，我们现在知道了 Threat Actor 正在使用 reg.exe 向注册表项添加项，程序位于 C:\temp。运行以下语句，将查询中的搜索运算符替换为 where 运算符 :

    ```KQL
    DeviceRegistryEvents | where ActionType == "RegistryValueSet"
    | where InitiatingProcessFileName == "reg.exe"
    | where RegistryValueData startswith "c:\\temp"
    ```

1. 或者，可以使用 DeviceProcessEvents 表运行以下 KQL 查询：

    ```KQL
    DeviceProcessEvents | where ActionType == "ProcessCreated"
    | where FileName == "reg.exe"
    | where ProcessCommandLine contains "c:\\temp"
    ```

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

    ```KQL
    DeviceRegistryEvents
    | where ActionType == "RegistryValueSet"
    | where InitiatingProcessFileName == "reg.exe"
    | where RegistryValueData startswith "c:\\temp"
    | extend timestamp = TimeGenerated, HostCustomEntity = DeviceName, AccountCustomEntity = InitiatingProcessAccountName
    ```

   ![屏幕快照](../Media/SC200_sysmon_query2.png)

1. 或者，可以使用 DeviceProcessEvents 表运行以下 KQL 查询：

    ```KQL
    DeviceProcessEvents | where ActionType == "ProcessCreated"
    | where FileName == "reg.exe"
    | where ProcessCommandLine contains "c:\\temp"
    | extend timestamp = TimeGenerated, HostCustomEntity = DeviceName, AccountCustomEntity = InitiatingProcessAccountName
    ```

1. 你将使用 Log Analytics KQL 查询，并从这里创建自定义分析规则，以帮助发现环境中的威胁和异常行为。

1. This starts the "Analytics rule wizard". For the <bpt id="p1">*</bpt>General<ept id="p1">*</ept> tab type:

    |设置|值|
    |---|---|
    |名称|MDE Startup RegKey|
    |说明|c:\temp 中的 MDE Startup Regkey|
    |策略|**持久性**|
    |Severity|**高**|

1. 选择“下一页:**设置规则逻辑 >”按钮**。

1. 在“设置规则逻辑”选项卡上，“规则查询”应已填充 KQL 查询，以及“警报扩充 - 实体映射”下的实体  。

1. 对于“查询计划”，设置以下项：

    |设置|值|
    |---|---|
    |运行查询的时间间隔|5 分钟|
    |查看最近多久的数据|1 天|

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. 对于“事件设置”选项卡，保留默认值并选择“下一页: “下一步: 自动响应 >”按钮。

1. 对于“自动响应”选项卡，选择“警报自动化”下的“PostMessageTeams-OnAlert”，然后选择“下一页: 审阅”按钮。

1. 在“查看”选项卡上，选择“创建”按钮以新建计划分析规则。


### <a name="task-2-attack-2-detection-with-securityevent"></a>任务 2：使用 SecurityEvent 检测攻击 2

在此任务中，你将在安装了安全事件连接器的主机上创建针对攻击 2 的检测。

1. 如果你已离开此页面，在 Microsoft Sentinel 门户中，选择“常规”部分中的“日志”。

1. 运行以下 KQL 语句以标识任何引用管理员的条目：

    ```KQL
    search "administrators" | summarize count() by $table
    ```

1. The result might show events from different tables, but in our case, we want to investigate the SecurityEvent table. The EventID and Event that we are looking is "4732 - A member was added to a security-enabled local group". With this, we will identify adding a member to a privileged group. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL query to confirm:

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

1. Expand the row to see all the columns related to the record. The username of the account added as Administrator does not show. The issue is that instead of storing the username, we have the Security IDentifier (SID). <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL to match the SID to the username that was added to the Administrators group:

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    ```

   ![屏幕快照](../Media/SC200_sysmon_attack3.png)

    >**注意：** 实验室使用的数据集较小，因此该 KQL 可能不会返回预期结果。

1. Extend the row to show the resulting columns, in the last one, we see the name of the added user under the <bpt id="p1">*</bpt>UserName1<ept id="p1">*</ept> column we <bpt id="p2">*</bpt>project<ept id="p2">*</ept> within the KQL query. It is important to help the Security Operations Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following query:

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName1
    ```

1. 你现在有一个不错的检测规则，接下来请在“日志”窗口中，选择命令栏中的“+ 新建预警规则”，然后选择“创建 Microsoft Sentinel 警报” 。

1. 此检测将重点关注来自 Defender for Endpoint 的数据。

    |设置|值|
    |---|---|
    |名称|SecurityEvents 本地管理员用户添加操作|
    |说明|添加到本地管理员组的用户|
    |策略|**特权提升**|
    |Severity|**高**|

1. 选择“下一页:**设置规则逻辑 >”按钮**。 

1. 在“设置规则逻辑”选项卡上，“规则查询”应已填充 KQL 查询，以及“警报扩充 - 实体映射”下的实体  。

1. 对于“查询计划”，设置以下项：

    |设置|值|
    |---|---|
    |运行查询的时间间隔|5 分钟|
    |查看最近多久的数据|1 天|

    >运行以下 KQL 语句：

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. 对于“事件设置”选项卡，保留默认值并选择“下一页: “下一步: 自动响应 >”按钮。

1. 对于“自动响应”选项卡，选择“警报自动化”下的“PostMessageTeams-OnAlert”，然后选择“下一页: 审阅”按钮。

1. 在“查看”选项卡上，选择“创建”按钮以新建计划分析规则。

## <a name="proceed-to-exercise-8"></a>继续完成练习 8
