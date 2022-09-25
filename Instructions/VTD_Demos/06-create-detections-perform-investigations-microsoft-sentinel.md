# <a name="module-6-create-detections-and-perform-investigations-with-microsoft-sentinel"></a>模块 6 使用 Microsoft Sentinel 创建检测并执行调查

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="attack-1-detection-with-sysmon"></a>使用 Sysmon 检测攻击 1

在此任务中，你将在安装了安全事件连接器和 Sysmon 的主机上创建针对攻击 1 的检测。

此攻击会创建一个在启动时运行的注册表项。  
```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

3. 在“登录”对话框中，复制粘贴实验室托管提供者为管理员提供的租户电子邮件帐户，然后选择“下一步”  。

4. 在“输入密码”对话框中，复制粘贴实验室托管提供者为管理员提供的租户密码，然后选择“登录”  。

5. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

6. 选择之前创建的 Microsoft Sentinel 工作区。

7. 从“常规”部分选择“日志”。

8. First, you need to see where the data is stored. Since you just performed the attacks.  Set the Log Time Range to <bpt id="p1">**</bpt>Last 24 hours<ept id="p1">**</ept>.

9. 运行以下 KQL 语句

```KQL
search "temp\\startup.bat"
```

10. 针对 3 个不同的表显示结果：DeviceProcessEvents DeviceRegistryEvents Event

    The Device* tables are from Defender for Endpoint (Data Connector - Microsoft 365 Defender).  Event is from our Data Connector Security Events. 

    Since we are receiving data from two different sources - Sysmon and Defender for Endpoint,  we will need to build two KQL statements that could be unioned later.  In our initial investigation, you will look at each separately.

11. Our first data source is Sysmon from Windows hosts.  Run the following KQL Statement.

```KQL
search in (Event) "temp\\startup.bat"
```
现在仅显示 Event 表的结果。  

16. Create your own KQL statement to display all Registry Key Set Value rows.  Run the following KQL query:

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
    
    In the Log window, select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>, then <bpt id="p2">**</bpt>Save as function<ept id="p2">**</ept>.
    In the Save flyout, enter the following:

    名称：Event_Reg_SetValue Save as:Function Function Alias:Event_Reg_SetValue Category:Sysmon

18. 打开新的“日志查询”选项卡。然后运行以下 KQL 语句：

```KQL

Event_Reg_SetValue

```
Depending on the current data collection, you could receive many rows.  This is expected.  Our next task is to filter to our specific scenario.

19. 运行以下 KQL 语句：

```KQL

Event_Reg_SetValue | search "startup.bat"

```

22. It is important to help the Security Operations Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph.  Run the following query:

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

## <a name="you-have-completed-the-demo"></a>你已完成本演示。