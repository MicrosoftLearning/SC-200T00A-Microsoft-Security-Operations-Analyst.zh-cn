---
lab:
  title: 练习 8 - 调查事件
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-8---investigate-incidents"></a>模块 7 - 实验室 1 - 练习 8 - 调查事件

## <a name="lab-scenario"></a>实验室方案


You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules. The Fusion and Anomalies Analytics rules are also enabled in your environment. Now is the time to investigate the Incidents created by them.

An incident can include multiple alerts. It is an aggregation of all the relevant evidence for a specific investigation. The properties related to the alerts, such as severity and status, are set at the incident level. After you let Microsoft Sentinel know what kinds of threats you are looking for and how to find them, you can monitor detected threats by investigating incidents.


### <a name="task-1-investigate-an-incident"></a>任务 1：调查一个事件

在此任务中，你将调查一个事件。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 选择“事件”页面。

1. 查看事件列表。

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The Analytics rules are generating alerts and incidents on the same specific log entry. Remember that this was done in the <bpt id="p1">*</bpt>Query scheduling<ept id="p1">*</ept> configuration to generate more alerts and incidents to be utilized in the lab.
  
1. 选择其中一个 MDE Startup RegKey 事件。

1. Review the incident details on the right blade that opened. Scroll down and select the <bpt id="p1">**</bpt>View full details<ept id="p1">**</ept> button.

1. 在事件的左侧边栏选项卡上，将状态更改为“活动”，然后选择“应用” 。

1. 向下滚动到“标记”区域，选择“+”并键入“RegKey”，然后选择“确定”  。

1. 在中间窗格中，选择“注释”选项卡。

1. 在注释框中键入：“我将调查此事件”，然后选择“注释”按钮提交新注释。

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 你已创建“计划”规则和“Microsoft 安全分析”规则。

1. 环境中也启用了“融合”和“异常分析”规则。

1. 现在，可以调查他们创建的事件。

1.  When you select an entity, a window on the right opens for more detailed information. Review the <bpt id="p1">**</bpt>Info<ept id="p1">**</ept> page.

1. 一个事件可以包含多个警报。

1. 选择“实体”按钮，然后查看与 WIN1 相关的实体和警报  。

1. 通过选择页面右上方的 X 关闭调查图。

1. 其中聚合了特定调查的所有相关证据。

1. 在事件级别设置与警报相关的属性，例如严重性和状态。

## <a name="proceed-to-exercise-9"></a>继续完成练习 9
