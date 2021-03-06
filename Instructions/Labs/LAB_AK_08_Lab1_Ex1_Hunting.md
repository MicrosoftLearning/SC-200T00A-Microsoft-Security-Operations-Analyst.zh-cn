---
lab:
  title: 练习 1 - 在 Microsoft Sentinel 中执行威胁搜寻
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
ms.openlocfilehash: 5fe3c20f10e420294fdb2b1048daec19ce359f02
ms.sourcegitcommit: 175df7de88c9a609f8caf39840664bf992c5b6dc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2022
ms.locfileid: "138025498"
---
# <a name="module-8---lab-1---exercise-1---perform-threat-hunting-in-microsoft-sentinel"></a>模块 8 - 实验室 1 - 练习 1 - 在 Azure Sentinel 中执行威胁搜寻

## <a name="lab-scenario"></a>实验室方案

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

1. 上一个 KQL 查询的目标是为 C2 信标提供一致的可视化效果。 将 bin () 中的 3m 设置设置为 30s 以调整值的分组，然后再次运行查询 。

1. 请改回 3m。 现在，将 count_ 阈值更改为 10，然后再次运行查询以见证影响 。

1. 你现已确定要向 C2 服务器发送信标的 DNS 请求。 接下来，请确定要发送信标的设备。 运行以下 KQL 语句：

   ```KQL
   let lookback = 2d;
   DeviceEvents | where TimeGenerated >= ago(lookback) 
   | where ActionType == "DnsQueryResponse"
   | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
   | where c2 startswith "sub"
   | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
   | where cnt > 15
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

1. 选择“查看结果”按钮。 KQL 查询将自动运行。

1. 选中结果中第一行的复选框。 

1. 在中间的命令栏中，选择“添加书签”按钮。

1. 查看默认填充的值，在“添加书签”边栏选项卡中，选择“创建”。

1. 通过选择窗口右上方的“X”关闭“日志”窗口，然后选择“确定”以放弃更改 。 

1. 返回到 Microsoft Sentinel 门户的“搜寻”页，选择中间窗格中的“书签”选项卡。

1. 从结果列表中选择刚刚创建的“C2 Hunt”书签。

1. 在右窗格中，向下滚动并选择“调查”按钮。

1. 像在上一模块中一样浏览调查图。

1. 通过选择窗口右上方的“X”关闭“调查图”窗口，然后选择“确定”以放弃更改 。 

1. 选择“查询”选项卡。

1. 再次搜索并选择“C2 Hunt”查询。

1. 右键单击查询，然后选择“添加到直播”。 提示：也可通过向右滑动并选择行末尾的省略号 (...) 打开上下文菜单完成此操作。

1. 查看“状态”现在为“正在运行” 。 如果找到结果，将在 Azure 门户（钟形图标）中收到通知。

# <a name="proceed-to-exercise-2"></a>继续进行练习 2
