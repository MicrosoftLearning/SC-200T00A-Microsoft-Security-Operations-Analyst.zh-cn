---
lab:
    title: '练习 3 - 创建计划查询'
    module: '模块 7 - 使用 Microsoft Sentinel 创建检测并执行调查'
---

# 模块 7 - 实验室 1 - 练习 3 - 创建计划查询


### 任务 1：创建计划查询。

在此任务中，你将创建一个计划查询，并将其连接到在上一个练习中创建的 Teams 频道。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 在“**登录**”对话框中，复制粘贴实验室托管提供者提供的**租户电子**邮件帐户，然后选择“**下一步**”。

3. 在“**输入密码**”对话框中，复制粘贴实验室托管提供者提供的**租户密码**，然后选择“**登录**”。

4. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择“**Microsoft Sentinel**”。

5. 选择 Microsoft Sentinel 工作区。

6. 从“配置”区域选择 **“分析”**。

7. 选择“**+ 创建**”按钮，然后选择“**计划查询规则**”。

8. 在分析规则向导中的“常规”选项卡上，输入名称“*Azure AD 角色分配审核线索*”。

9. 对于“策略”，选择“**持续**”。

10. 对于“严重性”，选择“**低**”。

11. 选择 **“下一步: 设置规则逻辑 >”** 按钮：

12. 对于规则查询，粘贴以下 KQL 语句：

    >**警告**：使用 Paste 函数粘贴到虚拟机时，可添加额外（竖线）字符。确保先使用记事本粘贴以下查询。

```KQL
AuditLogs 
| where isnotempty(InitiatedBy.user.userPrincipalName) and Result == 'success' and OperationName contains "member to role" and AADOperationType startswith "Assign"
| extend InitiatedByUPN = tostring(InitiatedBy.user.userPrincipalName)
| extend InitiatedFromIP = iff(tostring(AdditionalDetails.[7].value) == '', tostring(AdditionalDetails.[6].value), tostring(AdditionalDetails.[7].value))
| extend TargetUser = tostring(TargetResources.[2].displayName)
| extend TargetRoleName = tostring(TargetResources.[0].displayName)
| project TimeGenerated, InitiatedByUPN, InitiatedFromIP, TargetUser, TargetRoleName, AADOperationType, OperationName
```

>**备注**：如果选择“查看查询结果”链接，应该不会收到任何结果和任何错误。如果接收到错误，请检查查询是否与之前的 KQL 语句相似。

13. 回到“*警报扩充(预览)*”区域中的“分析规则向导 - 新建计划规则”边栏选项卡，选择“*实体映射*”并选择以下值： 

    - 在“*实体类型*”下拉列表中，选择“**帐户**”。
    - 在“*标识符*”下拉列表中，选择“**全称**”。
    - 在“*值*”下拉列表中，选择“**InitiatedByUPN**”。

    选择“**添加新实体**”，然后选择以下值：

    - 在“*实体类型*”下拉列表中，选择“**IP**”。
    - 在“*标识符*”下拉列表中，选择“**地址**”。
    - 在“*值*”下拉列表中，选择“**InitiatedFromIP**”。

14. 在“*查询计划*”中，设置以下项：

    |设置|值|
    |---|---|
    |运行查询的时间间隔：|5 分钟|
    |查看最近多久的数据：|1 天|

    >**备注**：我们特意针对同一数据生成了多个事件。  这样，实验室就可使用这些警报。

15. 对于“*警报阈值*”区域，不更改任何选项。

    >**备注**：最佳做法是在 KQL 查询语句中管理阈值。

16. 对于“*事件分组*”区域，保持选中“**将所有事件分组到一个警报中**”。

17. 选择“**下一步: 事件设置 >**”按钮。  

18. 在“*事件设置(预览)*”选项卡上，查看默认选项。

19. 选择“**下一步: 自动响应 >**”按钮。

20. 在“*自动响应*”选项卡的“警报自动化”区域，选择在上一个练习中创建的“*PostMessageTeams-OnAlert*”playbook。

22. 选择“**下一步: 查看 >**”按钮。
  
23. 选择“**创建**”。


### 任务 2：测试我们的新规则。

在此任务中，你将测试新的计划查询规则。

1. 在 Azure 门户的搜索栏中，键入“*Azure Active Directory*”。然后选择“**Azure Active Directory**”。

2. 在“**管理**”区域中选择“用户”，这会显示“用户 - 所有用户(预览)”页面。

3. 选择列表中的用户“**Christie Cline**”，这会显示“Christie Cline - 个人资料”页面。

4. 在“**管理”区域中选择**“分配的角色”，这会显示“Christie Cline - 分配的角色”页面。

5. 从命令栏中选择“**+ 添加分配**”。

6. 在“**添加分配**”页的“**成员资格**”选项卡中，在“**选择角色**”下选择“**用户管理员**”，然后选择“**下一步 >**”。

7. 在“**设置**”选项中查看默认分配类型，然后选择“**分配**”。如果无法完成分配，请重试。

8. 选择右上角的“x”两次，关闭“Christie Cline - 分配的角色”和“用户 - 所有用户(预览)”页面。

9. 在“Contoso - 概述”页面的“**监视**”下，选择“**审核日志**”。

10. 选择“**导出数据设置**”，验证“Azure Active Directory”数据连接器是否在 Sentinel 中正确设置。

11. 检查之前为 Sentinel 创建的 *Log Analytics 工作*区是否有一个“*诊断设置*”条目。

12. 选择右上角的“x”关闭页面。

13. 选择“**刷新**”，直到看到“类别” “*的条目：RoleManagement*”，它指示之前在角色中所做的更改。

14. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择“**Microsoft Sentinel**”。

15. 选择 Microsoft Sentinel 工作区。

16. 选择“**事件**”菜单选项。

    >**备注**：触发的警报可能需要至少 5 分钟来处理。你可以继续进行下一个练习，稍后再返回到这里。若要自动更新“事件”页面，请选择“**自动刷新事件**”开关。

17. 应该会看到新创建的事件。选择“事件”并查看右侧边栏选项卡中的信息。

18. 打开浏览器选项卡并转到 https://teams.microsoft.com， 以打开 Microsoft Teams。转到 *SOC* 团队，查看发布的有关该事件的消息。

## 转到练习 4
