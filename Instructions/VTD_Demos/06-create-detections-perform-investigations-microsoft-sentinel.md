# 模块 6 使用 Microsoft Sentinel 创建检测并执行调查

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## 创建 NRT 查询规则

在此任务中，你将创建 NRT（近实时）分析查询规则。

1. 在 Microsoft Sentinel 中的“配置”下选择“Analytics”页面。

1. 选择“创建”**** 选项卡，然后选择“NRT 查询规则”****。

1. 这会启动“分析规则向导”。 在“常规”选项卡中，键入以下内容：

    |设置|值|
    |---|---|
    |名称|**NRT PowerShell 搜寻**|
    |说明|**NRT PowerShell 搜寻**|
    |策略和技术|**命令和控制**|
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

1. 选择“下一步: 查看 + 创建 >”****。

1. 在“查看和创建”选项卡上，选择“保存”按钮以创建并保存新的计划分析规则。

## 配置了 Azure Monitor 代理 (AMA) 的 Windows 攻击检测

在此任务中，你将调查根据创建的 `NRT` 规则创建的事件。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者为管理员提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者为管理员提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在 `Microsoft Sentinel` 中，转到 `Threat management` 菜单部分并选择“事件”****

**备注**：`Incident` 可能需要几分钟才会显示出来。

1. 你应该会看到一个事件，该事件与你在创建的 `NRT` 规则中配置的 `Severity` 和 `Title` 匹配

1. 选择 `Incident`，`detail` 窗格随即打开

1. 选择“查看完整详细信息”****，然后选择“调查”**** 按钮。

1. 浏览与 `NRT PowerShell Hunt` 事件关联的 `Entities`。

1. 通过选择窗口右上角的“X”**** 关闭 `Investigation` 窗口。

1. 选择 `Logs` 选项卡，并输入以下 KQL 语句：

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

**备注**：可以在 `Queries History` 中查找此查询，并且可以从此处运行**** 它。

1. 选择“完成”**** 按钮以关闭 `Logs` 窗口。

1. 通过选择窗口右上角的“X”**** 关闭 `Incident` 窗口。

## 你已完成本演示
