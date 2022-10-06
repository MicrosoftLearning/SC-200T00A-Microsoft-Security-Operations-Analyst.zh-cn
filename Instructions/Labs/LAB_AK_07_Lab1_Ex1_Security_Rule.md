---
lab:
  title: 练习 1 - 修改 Microsoft 安全规则
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-1---modify-a-microsoft-security-rule"></a>模块 7 - 实验室 1 - 练习 1 - 修改 Microsoft 安全规则

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. First, you need to filter the alerts coming from Defender for Cloud into Microsoft Sentinel, by Severity. 


### <a name="task-1-activate-a-microsoft-security-rule"></a>任务 1：激活 Microsoft 安全规则

在此任务中，你将激活 Microsoft 安全规则。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com) )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择你在前面实验室中创建的 Microsoft Sentinel 工作区。

1. Select <bpt id="p1">**</bpt>Analytics<ept id="p1">**</ept> from the Configuration area. By default, you will see the <bpt id="p1">*</bpt>Active rules<ept id="p1">*</ept>. Click on <bpt id="p1">*</bpt>Rule templates<ept id="p1">*</ept>.

1. Search for and select <bpt id="p1">**</bpt>Create incidents based on Microsoft Defender for Cloud<ept id="p1">**</ept>. This rule was activated by the Defender for Cloud connector we configured in "Module 6 - Exercise 1 - Task 4". 

1. 在右侧边栏选项卡上，选择“编辑”按钮。

1. 向下滚动页面，在“分析规则逻辑 - 按严重性筛选”下选择“自定义”下拉列表。

1. 取消选择“低”作为严重性级别，然后返回到规则。

1. 选择底部的自动响应”按钮，然后选择“下一步:审阅”按钮。

1. Review the changes made and select the <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> button. The Analytics rule will be saved.

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
