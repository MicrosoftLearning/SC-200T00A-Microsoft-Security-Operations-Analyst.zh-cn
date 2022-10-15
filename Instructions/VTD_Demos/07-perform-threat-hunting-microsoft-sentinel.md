# <a name="module-7---threat-hunting-in-microsoft-sentinel"></a>模块 7 - 在 Microsoft Sentinel 中执行威胁搜寻

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="create-a-hunting-query"></a>创建搜寻查询

在此任务中，你将创建搜寻查询、为结果添加书签并创建 Livestream。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 选择“日志” 

1. 在新查询 1 区域输入以下 KQL 语句：

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

1. 该语句是为了提供一个可视化效果，用于在一致基础上检查 C2 信标输出。  花点时间将“3 分钟”设置调整为 30 秒或更长时间。  将 count_ > 5 设置更改为其他阈值计数来观察影响。

1. 你现已确定要向 C2 服务器发送信标的 DNS 请求。  接下来，请确定要发送信标的设备。  输入以下 KQL 语句：

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

注意：生成的日志数据仅来自加入的设备。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 在 Microsoft Sentinel 门户的“威胁管理”区域中选择“搜寻”页面。

1. 从命令栏选择“新建查询”。

1. 在“创建自定义查询”窗口中，为“名称”输入“C2 Hunt” 

1. 对于“自定义查询”，输入以下 KQL 语句：

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
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

1. 选择“查看结果”。

1. 选择结果中的第一行。 

1. 选择“添加书签”。

1. 在显示的窗格中选择“创建”。

1. 返回到 Microsoft Sentinel 门户中的“搜寻”页面。

1. 选择“书签”选项卡。

1. 在结果列表中选择书签。

1. 在弹出窗格中选择“调查”。

1. 浏览调查图。

1. 返回到 Microsoft Sentinel 门户中的“搜寻”页面。

1. 选择“查询”选项卡

1. 选择“C2 搜寻”查询。

1. 选择该行末尾的 ...，打开上下文菜单。

1. 选择“添加到 livestream”。

## <a name="you-have-completed-the-demo"></a>你已完成本演示。