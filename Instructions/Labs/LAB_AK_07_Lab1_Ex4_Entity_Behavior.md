---
lab:
  title: 练习 4 - 探索实体行为分析
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-4---explore-entity-behavior-analytics"></a>模块 7 - 实验室 1 - 练习 4 - 探索实体行为分析

## <a name="lab-scenario"></a>实验室方案

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules. 


需要将 Microsoft Sentinel 配置为执行实体行为分析来发现异常并提供实体分析页面。


### <a name="task-1-enable-entity-behavior"></a>任务 1：启用实体行为 

在此任务中，将在 Microsoft Sentinel 中启用实体行为分析。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 选择“实体行为”页。
1. 在“实体行为设置”的弹出窗口中，选择“设置 EUBA””。
1. 在下一页上，选择“设置 UEBA”。
1. 在“实体行为配置”页上，启用 #1 功能。 
1. For <bpt id="p1">*</bpt>2.<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>Azure Active Directory<ept id="p2">**</ept>. Then select <bpt id="p1">**</bpt>Apply<ept id="p1">**</ept>.
1. 对于 3.，请选择“审核日志”、“Azure 活动”、“安全事件”和“登录日志”。 
1. 然后，选择“应用”。
1. 经常在实验室期间返回此页面，查看根据引入的日志数据和创建的警报填充的实体。


### <a name="task-2-confirm-and-review-anomalies-rules"></a>任务 2：确认并查看异常规则

在此任务中，你将确认是否已启用异常分析规则。

1. 选择“分析”页。
1. 选择“异常”选项卡。
1. 确认规则的状态列为“已启用”。
1. Select any rule. Then select <bpt id="p1">**</bpt>Edit<ept id="p1">**</ept> on the rule blade.
1. Review the <bpt id="p1">*</bpt>General<ept id="p1">*</ept> tab information. Then select <bpt id="p1">**</bpt>Next : Configuration<ept id="p1">**</ept>
1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。


## <a name="proceed-to-exercise-5"></a>继续完成练习 5
