---
lab:
  title: 练习 1 - 在 Microsoft Sentinel 中执行威胁搜寻
  module: Learning Path 10 - Perform threat hunting in Microsoft Sentinel
---

# 学习路径 10 - 实验室 1 - 练习 1 - 在 Microsoft Sentinel 中执行威胁搜寻

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你收到了关于命令和控制（C2 或 C&C）技术的威胁情报。 你需要执行搜寻并监视威胁。

>**重要说明：** 学习路径 #10 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

>**备注：** 如果不重新运行练习 5 中的任务 1 和 2，以及练习 6 中 WIN1 服务器上的“*攻击 3*”，则无法在本实验室中使用在学习路径 9 实验练习中创建的日志数据。 可以通过选择以下链接，在新的浏览器选项卡中打开这些指令：

**[实验室 09 练习 5](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_09_Lab1_Ex05_Attacks.html)**

**[实验室 09 练习 6](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_09_Lab1_Ex06_Perform_Attacks.html)**

### 完成本实验室的估计时间：40 分钟

### 任务 1：创建搜寻查询

在此任务中，你将创建搜寻查询、为结果添加书签并创建 Livestream。

>**备注：** Microsoft Sentinel 已在 Azure 订阅中预先部署了名称 **defenderWorkspace**，并且已安装所需的“*内容中心*”解决方案。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com> )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel **defenderWorkspace**。

1. 选择“日志”

1. 在“新查询 1”空间输入以下 KQL 语句：

   >**重要提示：** 请首先将任意 KQL 查询粘贴到记事本，然后从此处复制到“新建查询 1 日志”窗口以避免任何错误。

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam 
    | order by count_ desc nulls last 
    ```

1. 查看不同的结果。 现在，你已确定在自己的环境中运行的 PowerShell 请求。

1. 选中显示“-file c2.ps1”的结果的复选框。

1. 在“结果”** 窗格命令栏中，选择“添加书签”**** 按钮。

1. 在“实体映射”下选择“+ 添加新实体”。

1. 对于“实体”，选择“主机”，然后选择“主机名”和“计算机”作为值  。

1. 对于“策略和技术”，选择“命令和控制”。

1. 在“添加书签”** 边栏选项卡中，选择“创建”****。 稍后我们会将此书签映射到事件。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 再次选择 Microsoft Sentinel 工作区，并在“威胁管理”区域下选择“搜寻”页面。

1. 选择“查询”选项卡，然后在命令栏中选择“+ 新建查询” 。

1. 在“创建自定义查询”窗口中，输入“PowerShell 搜寻”作为“名称” 。

1. 对于“自定义查询”，输入以下 KQL 语句：

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam 
    | order by count_ desc nulls last 
    ```

1. 向下滚动，在“实体映射”下，选择：

    - 对于“实体类型”下拉列表，请选择“Host”。
    - 对于“标识符”下拉列表，选择“HostName”。
    - 对于“值”下拉列表，选择“计算机”。

1. 向下滚动，然后在“策略与技术”下选择“命令和控制”，然后选择“创建”以创建搜寻查询 。

1. 在“Microsoft Sentinel | 搜寻”边栏选项卡中，在列表中搜索刚刚创建的查询，即“PowerShell 搜寻” 。

1. 在列表中选择“PowerShell 搜寻”。

1. 在中间窗格的“结果”列下查看结果数。

1. 在右窗格中选择“查看结果”按钮。 KQL 查询将自动运行。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 右键单击“PowerShell 搜寻”查询，然后选择“添加到实时流” 。 提示：也可通过向右滑动并选择行末尾的省略号 (...) 打开上下文菜单完成此操作。

1. 查看“状态”现在为“正在运行” 。 这将在后台每 30 秒运行一次，当找到新结果时，你将在 Azure 门户（铃铛图标）中收到通知。 

1. 在中间窗格中选择“书签”选项卡。

1. 在结果列表中选择你刚刚创建的书签。

1. 在右窗格中，向下滚动并选择“调查”按钮。 提示：可能需要几分钟时间才能显示调查图。

1. 像在上一模块中一样浏览调查图。 注意 WINServer 的相关警报数量很多 。

1. 选择窗口右上角的 X 关闭调查图。 

1. 选择 >> 图标，然后向右滚动，直到看到省略号 (...) 图标，以此隐藏右侧边栏选项卡 。

1. 选择“添加到现有事件”。 所有事件都显示在右窗格中。

1. 选择其中一个事件，然后选择“添加”。

1. 向左滚动可注意到“严重性”列现在填充了事件的数据。

### 任务 2：创建 NRT 查询规则

在此任务中，你将创建 NRT 分析查询规则，而不是使用 LiveStream。 NRT 规则每分钟运行一次，并回溯一分钟。 NRT 规则的优点是可以使用警报和事件创建逻辑。

1. 在 Microsoft Sentinel 中的“配置”下选择“Analytics”页面。 

1. 选择“创建”**** 选项卡，然后选择“NRT 查询规则”****。

1. 这会启动“分析规则向导”。 在“常规”选项卡中，键入以下内容：

    |设置|值|
    |---|---|
    |名称|**NRT PowerShell 搜寻**|
    |说明|**NRT PowerShell 搜寻**|
    |策略|**命令和控制**|
    |Severity|**高**|

1. 选择“下一页:**设置规则逻辑 >”按钮**。 

1. 对于“规则查询”，输入以下 KQL 语句：

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

1. 选择“查看查询结果 >”，确保查询没有任何错误。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 在“结果模拟”下选择“使用当前数据进行测试”。 注意每天的预期警报数。

1. 在“实体映射”下，选择：

    - 对于“实体类型”下拉列表，请选择“Host”。
    - 对于“标识符”下拉列表，选择“HostName”。
    - 对于“值”下拉列表，选择“计算机”。

1. 向下滚动，选择“下一步: 事件设置>”按钮。

1. 对于“事件设置”** 选项卡，保留默认值并选择“下一步: 自动响应 >”**** 按钮。

1. 在“自动响应”** 选项卡上，选择“下一步: 查看和创建”**** 按钮。

1. 在“查看和创建”选项卡上，选择“保存”按钮以创建并保存新的计划分析规则。

### 任务 3：创建搜索作业

在此任务中，你将使用搜索作业查找 C2。

<!--- >**Note:** The *Restore* operation incurs costs that can deplete your Azure Pass subscription credits. For that reason, you will not be performing the restore operation in this lab. However, you can follow the steps below to perform the restore operation in your own environment. --->

1. 在 Microsoft Sentinel 的“常规”下，选择“搜索”页面。

1. 在搜索框中，输入 reg.exe，然后选择“启动” 。

1. 此时会打开一个运行查询的新窗口。 选择右上角的省略号图标 (...)，然后切换“搜索作业模式” 。

1. 选择命令栏中的“搜索作业”按钮。 

1. 搜索作业会在结果到达后立即使用结果创建一个新表。 你可以在“保存的搜索”选项卡中查询结果。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。

1. 在命令栏中选择“还原”选项卡，然后选择“还原”按钮 。

1. 在“选择要还原的表”下，搜索并选择 SecurityEvent。

1. 查看可用的选项，然后选择“取消”**** 按钮。

    >**备注：** 如果运行作业，还原将运行几分钟，并且数据将在新表中可用。

### 任务 4：创建将多个查询合并为 MITRE 策略的搜寻

1. MITRE ATT&CK 映射可帮助你识别检测覆盖范围中的特定缺口。 使用针对特定 MITRE ATT&CK 技术的预定义搜寻查询作为开发新检测逻辑的起点。

1. 在 Microsoft Sentinel 中，从左侧导航菜单中展开“**威胁管理**”。

1. 选择 **MITRE ATT&CK（预览版）**。

1. 取消选择“*可用规则*”下拉菜单中的项。

1. 在“*模拟规则*”筛选器中选择“**搜寻查询**”，查看哪些技术具有与之关联的搜寻查询。

1. 选择“**帐户操作**”卡。

1. 在详细信息窗格中，找到“*模拟覆盖范围*”，然后选择“*搜寻查询*”旁边的“**视图**”链接。

1. 此链接将基于所选技术转到“搜寻”页上的“查询”选项卡的筛选视图。

1. 通过选择左侧列表顶部附近的框，选择该技术的所有查询。

1. 选择筛选器上方屏幕中间附近的“**搜寻操作**”下拉菜单。

1. 选择“**创建新搜寻**”。 会为此新搜寻克隆你选定的所有查询。

1. 填写搜寻名称和可选字段。 可通过说明来描述你的假设。 可在“假设”下拉菜单设置正在工作的假设的状态。

1. 若要开始，请选择“创建”。

1. 选择“搜寻(预览)”选项卡来查看新搜寻。

1. 按名称选择搜寻链接来查看详细信息并执行操作。

1. 查看详细信息窗格，其中包含“搜寻名称”、“说明”、“内容”、“上次更新时间”和“创建时间”。

1. 使用“*查询*”列旁边的框选择所有查询。

1. 选择“**运行所选查询**”或取消选中所选行，然后*右键单击*并“**运行**”单个查询。

1. 还可以选择单个查询，然后在详细信息窗格中选择“**查看结果**”。

1. 查看哪些查询返回了结果。

1. 根据结果，确定是否有足够强大的证据来验证假设。 如果没有，请关闭“搜寻”并将其标记为无效。

1. 备用步骤：
    - 转到 Microsoft Sentinel。
    - 展开威胁管理。
    - 选择搜寻。
    - 选择“添加筛选器”。
    - 将筛选器设置为策略：暂留。
    - 添加另一个筛选器。
    - 将第二个筛选器设置为具有技术：T1098。

## 继续进行练习 2
