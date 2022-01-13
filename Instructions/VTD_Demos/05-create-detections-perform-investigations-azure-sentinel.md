# 模块 5 使用 Azure Sentinel 创建检测并执行调查

**备注**：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## 使用 Sysmon 检测攻击 1

在此任务中，你将在安装了安全事件连接器和 Sysmon 的主机上创建针对攻击 1 的检测。

此攻击会创建一个在启动时运行的注册表项。  
```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 在 Edge 浏览器中，通过 https://portal.azure.com 导航到 Azure 门户。

3. 在 **“登录”** 对话框中，复制粘贴实验室托管提供者为管理员提供的**租户电子**邮件帐户，然后选择 **“下一步”**。

4. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者为管理员提供的**租户密码**，然后选择 **“登录”**。

5. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择 **“Azure Sentinel”**。

6. 选择之前创建的 Azure Sentinel 工作区。

7. 从“常规”部分选择 **“日志”**。

8. 首先需要查看存储数据的位置。原因是你刚刚执行了攻击。  将日志时间范围设置为 **“过去 24 小时”**。

9. 运行以下 KQL 语句

```KQL
search "temp\\startup.bat"
```

10. 针对 3 个不同的表显示结果：
    DeviceProcessEvents
    DeviceRegistryEvents
    Event

    设备*表来自 Defender for Endpoint（数据连接器 - Microsoft 365 Defender）。  事件来自数据连接器安全事件。 

    我们将接收来自两个不同源（Sysmon 和 Defender for Endpoint）的数据，因此需要生成两个之后可联合的 KQL 语句。  初次调查时，你将分别查看每份数据。

11. 第一个数据源是 Windows 主机中的 Sysmon。  运行以下 KQL 语句。

```KQL
search in (Event) "temp\\startup.bat"
```
现在仅显示 Event 表的结果。  

16. 创建你自己的 KQL 语句，显示所有“注册表项集值”行。  运行以下 KQL 查询：

```KQL

Event
| where Source == "Microsoft-Windows-Sysmon"
| where EventID == 13
| extend RenderedDescription = tostring(split(RenderedDescription, ":")[0])
| project TimeGenerated, Source, EventID, Computer, UserName, EventData, RenderedDescription
| extend EvData = parse_xml(EventData)
| extend EventDetail = EvData.DataItem.EventData.Data
| project-away EventData, EvData  
| extend RuleName = EventDetail.[0].["#text"], EventType = EventDetail.[1].["#text"], UtcTime = EventDetail.[2].["#text"], ProcessGuid = EventDetail.[3].["#text"], 
    ProcessId = EventDetail.[4].["#text"], Image = EventDetail.[5].["#text"], TargetObject = EventDetail.[6].["#text"], Details = EventDetail.[7].["#text"]
    | project-away EventDetail 


```

17.  可从这里继续生成检测规则，但该 KQL 语句似乎可在其他检测规则的 KQL 语句中重复使用。  
    
    在“日志”窗口中，选择 **“保存”**，然后选择 **“保存为函数”**。
    在“保存”弹出窗口中，输入以下内容：

    名称：Event_Reg_SetValue
    另存为：函数
    函数别名：Event_Reg_SetValue
    类别：Sysmon

18. 打开新的“日志查询”选项卡。然后运行以下 KQL 语句：

```KQL

Event_Reg_SetValue

```
根据当前的数据集合，你可接收多个行。  这在预料之中。  下一个任务是筛选特定方案。

19. 运行以下 KQL 语句：

```KQL

Event_Reg_SetValue | search "startup.bat"

```

22. 请务必尽可能多地提供关于警报的上下文，为安全操作分析师提供帮助。这包括投影在调查关系图中使用的实体。  运行以下查询：

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

## 你已完成本演示。