---
lab:
  title: 练习 1 - 在 Microsoft Sentinel 中执行威胁搜寻
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-1---perform-threat-hunting-in-microsoft-sentinel"></a>模块 8 - 实验室 1 - 练习 1 - 在 Azure Sentinel 中执行威胁搜寻

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你收到了关于命令和控制（C2 或 C&C）技术的威胁情报。 你需要执行搜寻并监视威胁。

>**重要提示：** 本实验室使用的日志数据是在上一个模块中创建的。 请参阅练习 5 中 WIN1 服务器上的攻击 3。

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

1. 上一个 KQL 查询的目标是为 C2 信标提供一致的可视化效果。 将 bin () 中的 3m 设置设置为 1m 以调整值的分组，然后再次运行查询 。

1. 请改回 3m。 现在，将 count_ 阈值更改为 10，然后再次运行查询以见证影响 。

1. 你现已确定要向 C2 服务器发送信标的 DNS 请求。 接下来，请确定要发送信标的设备。 运行以下 KQL 语句：

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 3m), c2, DeviceName
    | where cnt > 5
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
    | summarize cnt=count() by bin(TimeGenerated, 3m), c2, DeviceName
    | where cnt > 5
    ```

1. 向下滚动，在“实体映射（预览）”下，选择：

    - 对于“实体类型”下拉列表，请选择“Host”。
    - 对于“标识符”下拉列表，选择“HostName”。
    - 对于“值”下拉列表，选择“DeviceName”。

1. 向下滚动，然后在“策略与技术”下选择“命令和控制”，然后选择“创建”以创建搜寻查询 。

1. 在“Microsoft Sentinel - 搜寻”边栏选项卡中，在列表中搜索刚刚创建的查询“C2 Hunt” 。

1. 从列表中选择“C2 Hunt”。

1. 在右窗格中，向下滚动并选择“运行查询”按钮。

1. 结果数显示在“结果”列下的中间窗格中。 或者，向上滚动以查看“结果”框的计数。

1. 选择“查看结果”按钮。 KQL 查询将自动运行。

1. 选中结果中第一行的复选框。 

1. 在中间的命令栏中，选择“添加书签”按钮。

1. 查看默认填充的值，在“添加书签”边栏选项卡中，选择“创建”。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 返回到 Microsoft Sentinel 门户的“搜寻”页，选择中间窗格中的“书签”选项卡。

1. 从结果列表中选择刚刚创建的“C2 Hunt”书签。

1. 在右窗格中，向下滚动并选择“调查”按钮。 提示：可能需要几分钟时间才能显示调查图。

1. 像在上一模块中一样浏览调查图。

1. 通过选择窗口右上方的“X”关闭“调查图”窗口，然后选择“确定”以放弃更改 。 

1. 选择“查询”选项卡。

1. 再次搜索并选择“C2 Hunt”查询。

1. 右键单击查询，然后选择“添加到直播”。 提示：也可通过向右滑动并选择行末尾的省略号 (...) 打开上下文菜单完成此操作。

1. 查看“状态”现在为“正在运行” 。 

1. 在“模块 7 - 实验室 1 - 练习 6 - 任务 1 - 攻击 3”中，你执行了 PowerShell 脚本来模拟 C2 攻击。 返回命令提示符窗口，在 C:\Temp 中输入以下命令并按 Enter 键。 

    >**注意：** 系统将打开一个新的 PowerShell 窗口，你将看到解决错误。 这是正常情况。

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

1. 当我们找到结果时，你将在 Azure 门户（钟形图标）中收到通知。


### <a name="task-2-create-a-nrt-query-rule"></a>任务 2：创建 NRT 查询规则

在此任务中，你将创建 NRT 分析查询规则，而不是使用 LiveStream。 NRT 规则每分钟运行一次，并回溯一分钟。 NRT 规则的优点是可以使用警报和事件创建逻辑。


1. 在 Microsoft Sentinel 中选择“分析”页面。 

1. 选择“创建”选项卡，然后选择“NRT 查询规则(预览版)” 。

1. 这会启动“分析规则向导”。 在“常规”选项卡中，键入以下内容：

    |设置|值|
    |---|---|
    |名称|**NRT C2 搜寻**|
    |说明|**NRT C2 搜寻**|
    |策略|**命令和控制**|
    |Severity|**高**|

1. 选择“下一页:**设置规则逻辑 >”按钮**。 

1. 对于“规则查询”，输入以下 KQL 语句：

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 3m), c2, DeviceName
    | where cnt > 5
    ```

1. 将其余选项保留为默认值。 选择“下一页:**事件设置 >”按钮**。

1. 对于“事件设置”选项卡，保留默认值并选择“下一页: “下一步: 自动响应 >”按钮。

1. 对于“自动响应”选项卡，选择“警报自动化(经典)”下的“PostMessageTeams-OnAlert”，然后选择“下一页: 审阅”按钮。

1. 在“查看”选项卡上，选择“创建”按钮以新建计划分析规则。

1. 在 Microsoft Sentinel 中“威胁管理”部分中选择“事件”页，然后等待新的“C2 搜寻”警报显示 。


### <a name="task-3-create-a-search"></a>任务 3：创建搜索

在此任务中，你将使用搜索作业查找 C2。 

1. 在 Microsoft Sentinel 中选择“搜索(预览版)”页。 

1. 选择命令栏中的“还原”按钮。

    >注意：实验室没有要从中还原的存档表。 正常过程将还原已存档的表，以包含在搜索作业中。

1. 查看可用的选项，然后选择“取消”按钮。

1. 选择“搜索”选项卡。

1. 选择搜索框下方的“表”筛选器，并将其更改为 DeviceRegistryEvents，然后选择“应用” 。

1. 在搜索框中，输入 reg.exe，然后选择“运行搜索” 。

1. 选择“保存的搜索”选项卡。

1. 搜索作业将创建名为“DeviceRegistryEvents_####_SRCH”的新表。

1. 等待搜索作业完成。 状态将依次显示“正在更新”、“正在进行”和“搜索已完成”  。

1. 选择“查看搜索结果”。 这将在“日志”中打开一个新选项卡，并查询新表名“DeviceRegistryEvents_####_SRCH”，然后显示结果。


## <a name="proceed-to-exercise-2"></a>继续进行练习 2
