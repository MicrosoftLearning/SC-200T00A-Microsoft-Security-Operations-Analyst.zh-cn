---
lab:
  title: 练习 3 - 创建计划查询
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-3---create-a-scheduled-query"></a>模块 7 - 实验室 1 - 练习 3 - 创建计划查询

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex3.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. After connecting your data sources to Microsoft Sentinel, you create custom analytics rules to help discover threats and anomalous behaviors in your environment.

分析规则将在你的整个环境中搜索特定事件或事件集，在达到特定事件阈值或条件时发出警报，生成故障事件以供 SOC 进行会审和调查，并通过自动化跟踪和修正流程来响应威胁。


### <a name="task-1-create-a-scheduled-query"></a>任务 1：创建计划查询

在此任务中，你将创建一个计划查询，并将其连接到在上一个练习中创建的 Teams 频道。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 从“配置”区域选择“分析”。

1. 选择“+ 创建”按钮，然后选择“计划查询规则” 。

1. 在“分析”规则向导中的“常规”选项卡上，键入名称“Azure AD 角色分配审核线索”。

1. 对于“策略”，请选择“持久性”。

1. 对于“严重性”，选择“低”。

1. 选择“下一页:设置规则逻辑 >”按钮：

1. 对于规则查询，粘贴以下 KQL 语句：

    ><bpt id="p1">**</bpt>Warning:<ept id="p1">**</ept> When using the Paste function to the virtual machine extra (pipe) characters could be added. Make sure you use Notepad first to paste the following query.

    ```KQL
    AuditLogs  
    | where isnotempty(InitiatedBy.user.userPrincipalName) and Result == 'success' and OperationName contains "member to role" and AADOperationType startswith "Assign"
    | extend InitiatedByUPN = tostring(InitiatedBy.user.userPrincipalName)
    | extend InitiatedFromIP = iff(tostring(AdditionalDetails.[7].value) == '', tostring(AdditionalDetails.[6].value), tostring(AdditionalDetails.[7].value))
    | extend TargetUser = tostring(TargetResources.[2].displayName)
    | extend TargetRoleName = tostring(TargetResources.[0].displayName)
    | project TimeGenerated, InitiatedByUPN, InitiatedFromIP, TargetUser, TargetRoleName, AADOperationType, OperationName
    ```

1. Select <bpt id="p1">**</bpt>View query results<ept id="p1">**</ept>. You should not receive any results nor any errors. If you receive an error, please review that the query appears just like the previous KQL statement. Close the <bpt id="p1">*</bpt>Logs<ept id="p1">*</ept> window by selecting the upper right <bpt id="p2">**</bpt>X<ept id="p2">**</ept> and select <bpt id="p3">**</bpt>OK<ept id="p3">**</ept> to discard to save changes to go back to the wizard.

1. 在“分析规则向导 - 创建新计划规则”选项卡中的“警报扩充”区域下，选择“实体映射”，然后选择以下值： 

    - 对于“实体类型”下拉列表，请选择“帐户”。
    - 对于“标识符”下拉列表，选择“FullName”。
    - 对于“值”下拉列表，请选择“InitiatedByUPN”。

1. 然后选择“添加新实体”并选择以下值：

    - 对于“实体类型”下拉列表，请选择“IP”。
    - 对于“标识符”下拉列表，选择“地址”。
    - 对于“值”下拉列表，请选择“InitiatedFromIP”。

1. 向下滚动并在“查询计划”下设置以下项：

    |设置|值|
    |---|---|
    |运行查询的时间间隔|5 分钟|
    |查看最近多久的数据|1 天|

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. 在“警报阈值”区域下，保留值不变，因为我们希望警报注册每个事件。

1. 在“事件分组”区域下，将“将所有事件分组到一个警报中”保留为所选选项，因为我们希望在每次运行时生成单个警报，只要查询返回的结果多于上述指定的警报阈值。

1. 选择底部的“下一步: 事件设置 >”按钮。 

1. 在“事件设置”选项卡上，查看默认选项。

1. 选择底部的“下一步: 自动响应 >”按钮。

1. 在“自动响应”选项卡的“警报自动化”区域下，选择在上一个练习中创建的“PostMessageTeams-OnAlert”playbook 。
1. 在“事件自动化”选项卡上，选择“新增”
1. 对于“自动化规则名称”，请输入“第 2 层”
1. 对于“操作”，请选择“分配所有者”
1. Then select <bpt id="p1">**</bpt>Assign to me<ept id="p1">**</ept>. Then select <bpt id="p1">**</bpt>Apply<ept id="p1">**</ept>.

1. 选择底部的“下一步: 查看 >”按钮。
  
1. 选择“创建”。


### <a name="task-2-test-our-new-rule"></a>任务 2：测试我们的新规则

在此任务中，你将测试新的计划查询规则。

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 选择“管理”区域中的“用户”，以便显示“用户 - 所有用户”页。

1. 选择列表中的用户“Christie Cline”，以便显示“Christie Cline - 个人资料”页。

1. 选择“管理”区域中的“分配角色”，以便显示“Christie Cline - 分配角色”页。

1. 从命令栏中选择“+ 添加分配”。

1. 你需要了解如何使用 Microsoft Sentinel 检测和缓解威胁。

    >**注意：** 可能需要单击“刷新”按钮才能看到新的角色分配。 

1. 通过选择两次右上方的“x”来关闭“Christie Cline - 分配角色”和“用户 - 所有用户”页。

1. 在“Contoso - 概述”Azure Active Directory 页中的“监视”下，选择“审核日志”。

1. 将数据源连接到 Microsoft Sentinel 后，可以创建自定义分析规则来帮助发现环境中的威胁和异常行为。

1. 查看之前为 Sentinel 创建的 Log Analytics 工作区是否具有“诊断设置”条目 。

1. 通过选择右上方的“x”关闭页面。

1. 返回“Contoso - 审核日志”，选择“刷新”直到看到指示你之前在角色中所做更改的“类别：RoleManagement”的条目。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 选择“事件”菜单选项。

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The alert triggered may take 5+ minutes to process. You may continue with the next exercise and return to this point later. For automatic updating of the Incidents page, select the <bpt id="p1">**</bpt>Auto-refresh incidents<ept id="p1">**</ept> toggle.

1. You should see the newly created Incident. Select the Incident and review the information in the right blade.

1. Go back to Microsoft Teams by selecting the tab in your Edge browser. If you closed it, just open a new tab and type <ph id="ph1">https://teams.microsoft.com</ph>. Go to the <bpt id="p1">*</bpt>SOC<ept id="p1">*</ept> Teams, select the <bpt id="p2">*</bpt>New Alerts<ept id="p2">*</ept> channel and see the message post about the incident.

## <a name="proceed-to-exercise-4"></a>继续完成练习 4
