# 模块 6 使用 Microsoft Sentinel 创建检测并执行调查

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## 配置了 Azure Monitor 代理 (AMA) 的 Windows 攻击检测

在此任务中，你将 

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者为管理员提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者为管理员提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 在 `Microsoft Sentinel` 中，转到 `Threat management` 菜单部分并选择“事件”

1. 你应该会看到一个事件，该事件与你在创建的 `NRT` 规则中配置的 `Severity` 和 `Title` 匹配

1. 选择 `Incident`，`detail` 窗格随即打开

1. `Owner` 分配应为 Operator1（从 `Automation rule` 创建），`Tactics and techniques` 应是“特权提升”（来自 `NRT` 规则） 

1. 选择“查看完整的详细信息”，查看所有 `Incident management` 功能和 `Incident actions`

## 你已完成本演示
