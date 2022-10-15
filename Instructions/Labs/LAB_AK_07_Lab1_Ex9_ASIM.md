---
lab:
  title: 练习 9 - 创建 ASIM 分析程序
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-9---create-asim-parsers"></a>模块 7 - 实验室 1 - 练习 9 - 创建 ASIM 分析程序

## <a name="lab-scenario"></a>实验室方案

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 需要为特定 Windows 注册表事件建模 ASIM 分析程序。  这些简化的分析程序将稍后按照 ASIM 分析程序注册表事件规范化标准完成（ https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema) 。

>重要提示：此实验室需要将较长的 KQL ASIM 分析程序脚本输入到 Microsoft Sentinel 中。 这些脚本是在此实验室开始时通过下载文件提供的。 另一个下载这些脚本的位置是： https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Allfiles

### <a name="task-1-develop-kql-function-for-microsoft-365-defender-registry-event"></a>任务 1：为 Microsoft 365 Defender 注册表事件开发 KQL 函数 

在此任务中，将创建一个函数，它是 DeviceRegistryEvents 的工作区分析程序。 

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 选择“日志”页。

1. 打开已下载的 SC200_module7_ASIM_Parser_scripts.txt，然后复制任务 1 脚本 KQL 语句并将其粘贴到新的查询选项卡。

>注意：下面的脚本仅供参考。

    ```KQL
    let RegistryType = datatable (TypeCode: string, TypeName: string) [
    "None", "Reg_None",
    "String", "Reg_Sz",
    "ExpandString", "Reg_Expand_Sz",
    "Binary", "Reg_Binary",
    "Dword", "Reg_DWord",
    "MultiString", "Reg_Multi_Sz",
    "QWord", "Reg_QWord"
    ];
    let RegistryEvents_M365D=() {
    DeviceRegistryEvents
    | extend
        // Event
        EventOriginalUid = tostring(ReportId), 
        EventCount = int(1), 
        EventProduct = 'M365 Defender for Endpoint', 
        EventVendor = 'Microsoft', 
        EventSchemaVersion = '0.1.0', 
        EventStartTime = TimeGenerated, 
        EventEndTime = TimeGenerated, 
        EventType = ActionType,
        // Registry
        RegistryKey = iff (ActionType in ("RegistryKeyDeleted", "RegistryValueDeleted"), PreviousRegistryKey, RegistryKey),
        RegistryValue = iff (ActionType == "RegistryValueDeleted", PreviousRegistryValueName, RegistryValueName),
        // RegistryValueType -- original name is fine 
        // RegistryValueData -- original name is fine 
        RegistryKeyModified = iff (ActionType == "RegistryKeyRenamed", PreviousRegistryKey, ""),
        RegistryValueModified = iff (ActionType == "RegistryValueSet", PreviousRegistryValueName, ""),
        // RegistryValueTypeModified -- Not provided by Defender
        RegistryValueDataModified = PreviousRegistryValueData
    | lookup RegistryType on $left.RegistryValueType == $right.TypeCode
    | extend RegistryValueType = TypeName
    | project-away
        TypeName,
        PreviousRegistryKey,
        PreviousRegistryValueName,
        PreviousRegistryValueData
    // Device
    | extend
        DvcHostname = DeviceName, 
        DvcId = DeviceId, 
        Dvc = DeviceName 
    // Users
    | extend
        ActorUsername = iff (InitiatingProcessAccountDomain == '', InitiatingProcessAccountName, strcat(InitiatingProcessAccountDomain, '\\', InitiatingProcessAccountName)), 
        ActorUsernameType = iff(InitiatingProcessAccountDomain == '', 'Simple', 'Windows'), 
        ActorUserIdType = 'SID'
    | project-away InitiatingProcessAccountDomain, InitiatingProcessAccountName
    | project-rename
    ActorUserId = InitiatingProcessAccountSid, 
    ActorUserAadId = InitiatingProcessAccountObjectId, 
    ActorUserUpn = InitiatingProcessAccountUpn
    // Processes
    | extend
    ActingProcessId = tostring(InitiatingProcessId), 
    ParentProcessId = tostring(InitiatingProcessParentId) 
    | project-away InitiatingProcessId, InitiatingProcessParentId
    | project-rename
    ParentProcessName = InitiatingProcessParentFileName, 
    ParentProcessCreationTime = InitiatingProcessParentCreationTime, 
    ActingProcessName = InitiatingProcessFolderPath, 
    ActingProcessFileName = InitiatingProcessFileName,
    ActingProcessCommandLine = InitiatingProcessCommandLine, 
    ActingProcessMD5 = InitiatingProcessMD5, 
    ActingProcessSHA1 = InitiatingProcessSHA1, //OK
    ActingProcessSHA256 = InitiatingProcessSHA256, 
    ActingProcessIntegrityLevel = InitiatingProcessIntegrityLevel, 
    ActingProcessTokenElevation = InitiatingProcessTokenElevation, 
    ActingProcessCreationTime = InitiatingProcessCreationTime 
    // -- aliases
    | extend 
    Username = ActorUsername,
    UserId = ActorUserId,
    UserIdType = ActorUserIdType,
    User = ActorUsername,
    CommandLine = ActingProcessCommandLine,
    Process = ActingProcessName
    };
    RegistryEvents_M365D
    ```
>**注意：** 花些时间逐行检查 KQL。  
1. 选择“运行”以确认 KQL 有效。
1. 选择“保存”，然后选择“另存为函数”。
1. 向下滚动并在“查询计划”下设置以下项：

    |设置|值|
    |---|---|
    |函数名称|vimRegEvtM365D|
    |旧类别|MyASIM|
1. 再选择“保存”。
1. 在“新建查询”选项卡中，输入“vimRegEvtM365D”，然后选择“运行”。


### <a name="task-2-develop-kql-function-for-securityevent-table"></a>任务 2：为 SecurityEvent 表开发 KQL 函数。 

在此任务中，将创建一个函数，它是 SecurityEvent 的工作区分析程序。

1. 新建查询选项卡。
1. 打开已下载的 SC200_module7_ASIM_Parser_scripts.txt，然后复制任务 2 脚本 KQL 语句并将其粘贴到新的查询选项卡。

>注意：下面的脚本仅供参考。

    ```KQL
    let RegistryType = datatable (TypeCode: string, TypeName: string) [
    "%%1872", "Reg_None",
    "%%1873", "Reg_Sz",
    "%%1874", "Reg_Expand_Sz",
    "%%1875", "Reg_Binary",
    "%%1876", "Reg_DWord",
    "%%1879", "Reg_Multi_Sz",
    "%%1883", "Reg_QWord"
    ];
    let RegistryAction = datatable (EventOriginalSubType: string, EventType: string) [
        "%%1904", "RegistryValueSet",
        "%%1905", "RegistryValueSet",      
        "%%1906", "RegistryValueDeleted"             
    ];
    let Hives = datatable (KeyPrefix: string, Hive: string) [
        "MACHINE", "HKEY_LOCAL_MACHINE",
        "USER", "HKEY_USERS",   
    ];
    let RegistryEvents=() {
        SecurityEvent
        // -- Filter
        | where EventID == 4657          
        // Event
        | extend
            EventCount = int(1), 
            EventVendor = 'Microsoft', 
            EventProduct = 'Security Events', 
            EventSchemaVersion = '0.1.0', 
            EventStartTime = todatetime(TimeGenerated), 
            EventEndTime = todatetime(TimeGenerated),
            EventOriginalType = tostring(EventID) 
        | project-rename
            EventOriginalSubType = OperationType,
            EventOriginalUid = EventOriginId
        | lookup RegistryAction on EventOriginalSubType
        // Registry
        // Normalize key hive
        | parse ObjectName with "\\REGISTRY\\" KeyPrefix "\\" Key
        | lookup Hives on KeyPrefix
        | extend RegistryKey = strcat (Hive, "\\", Key)
        | project-away Hive, Key, KeyPrefix, ObjectName
        | project-rename
            RegistryValue = ObjectValueName
        | extend
            RegistryValueData = iff (EventOriginalSubType == "%%1906", OldValue, NewValue), 
            RegistryKeyModified = iff (EventOriginalSubType == "%%1905", RegistryKey, ""),
            RegistryValueModified = iff (EventOriginalSubType == "%%1905", RegistryValue, ""),
            RegistryValueDataModified = iff (EventOriginalSubType == "%%1905", OldValue, "")
        | lookup RegistryType on $left.NewValueType == $right.TypeCode
        | project-rename RegistryValueType = TypeName
        | lookup RegistryType on $left.OldValueType == $right.TypeCode
        | project-rename RegistryValueTypeModified = TypeName
        | project-away OldValue, NewValue, OldValueType, NewValueType
        // Device
        | extend
            DvcId = SourceComputerId,
            DvcHostname = Computer,
            DvcOs = 'Windows'
        // User
        | project-rename
            ActorUserId = SubjectUserSid, 
            ActorSessionId = SubjectLogonId, 
            ActorDomainName = SubjectDomainName
        | extend
            ActorUserIdType = 'SID',
            ActorUsername = iff (ActorDomainName == '-', SubjectUserName, SubjectAccount), 
            ActorUsernameType = iff(ActorDomainName == '-', 'Simple', 'Windows'),
            ActingProcessId = tostring(toint(ProcessId)) 
        // Process 
        | project-rename
            ActingProcessName = ProcessName
        // -- Aliases
        | extend
            User = ActorUsername,
            UserId = ActorUserId,
            Dvc = DvcHostname,
            Process = ActingProcessName
        // -- Remove potentially confusing
        | project-away 
            SubjectUserName,
            SubjectAccount
    };
    RegistryEvents
    ```

>**注意：** 花些时间逐行检查 KQL。  
1. 选择“运行”以确认 KQL 有效。
1. 选择“保存”，然后选择“另存为函数”。
1. 向下滚动并在“查询计划”下设置以下项：

    |设置|值|
    |---|---|
    |函数名称|vimRegEvtSecurityEvent|
    |旧类别|MyASIM|
1. 再选择“保存”。
1. 在新查询选项卡中，输入“vimRegEvtSecurityEvent”，然后选择“运行”


### <a name="task-3-create-a-unifying-workspace-parser"></a>任务 3：创建一个统一的工作区分析程序。 

在此任务中，将创建合并前两个函数的统一分析程序函数。  

1. 新建查询选项卡。
1. 在“新建查询”选项卡中输入以下 KQL 语句：

    ```KQL
    union isfuzzy=true
    vimRegEvtM365D,
    vimRegEvtSecurityEvent
    ```

1. 选择“运行”以确认 KQL 有效。
1. 选择“保存”，然后选择“另存为函数”。
1. 向下滚动并在“查询计划”下设置以下项：

    |设置|值|
    |---|---|
    |函数名称|imRegEvt|
    |旧类别|MyASIM|
1. 再选择“保存”。
1. 在新查询选项卡中，输入“imRegEvt”并选择“运行”
1. 将查询更新为“imRegEvt | where ActionType == 'RegistryValueSet'”并选择“运行”


## <a name="proceed-to-exercise-10"></a>继续完成练习 10

