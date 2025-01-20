---
lab:
  title: 练习 2 - 创建 Playbook
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 9 - 实验室 1 - 练习 2 - 在 Microsoft Sentinel 中创建 Playbook

## 实验室方案

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你需要了解如何使用 Microsoft Sentinel 检测和缓解威胁。 现在，你想要响应和修正可以从 Microsoft Sentinel 作为例程运行的操作。

使用 playbook，可以帮助自动执行和协调威胁响应，与其他内部系统和外部系统集成，并可以设置为自动运行以响应特定警报或事件（分别由分析规则或自动化规则触发时）。

>**重要说明：** 学习路径 #9 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

### 任务 1：在 Microsoft Sentinel 创建 Playbook

在此任务中，你将创建在 Microsoft Sentinel 用作 Playbook 的逻辑应用。

>**备注：** Microsoft Sentinel 已在 Azure 订阅中预先部署了名称 **defenderWorkspace**，并且已安装所需的“*内容中心*”解决方案。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel **defenderWorkspace**。

1. 在 *Microsoft Sentinel* 中，导航到“**内容中心**”。

1. 在搜索栏中，查找 **Sentinel SOAR Essentials**。

1. 选择结果中显示的解决方案。

1. 在解决方案详细信息中，选择“**管理**”。

1. 找到 **Defender_XDR_Ransomware_Playbook_for_SecOps-Tasks** playbook 并选择名称。

1. 选择**事件任务 - Microsoft Defender XDR 勒索软件 Playbook for SecOps** 模板。

1. 在“详细信息”窗格中选择“**创建 playbook**”。

1. 对于资源组，选择“**新建**”并输入 **RG-Playbooks**，然后选择“确定”。

1. 从 playbook 名称中移除 **for**（将超过 64 个字符的限制）。

1. 选择**连接**。

1. 选择“下一步: 查看并创建”。

1. 现在，选择“**创建 Playbook**”。

    >**注意：** 请等待部署完成后再继续下一个任务。

### 任务 2：在 Microsoft Sentinel 中更新 Playbook

在此任务中，你将使用适当的连接信息更新创建的新 playbook。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择 Microsoft Sentinel 工作区。

1. 在“配置”区域下选择“自动化”，然后选择“可用的 Playbook”选项卡。

1. 如果看不到任何 playbook，请在命令栏中选择“刷新”。 应会显示在上一步中创建的 Playbook。

1. 选择 **Defender_XDR_Ransomware_Playbook_SecOps_Tasks** playbook 名称。

1. 在 **Defender_XDR_Ransomware_Playbook_for_SecOps_Tasks** 的逻辑应用页上的命令菜单中，选择“编辑”。

    >**注意：** 可能需要刷新页面。

1. 选择第一个块“Microsoft Sentinel 事件”。

1. 选择“更改连接”链接。

1. 选择“添加新项”，然后选择“登录” 。 当系统提示时，在新窗口中，选择 Azure 订阅管理员凭据。 现在，块的最后一行应显示“已连接到 your-admin-username”。

1. 在逻辑拆分下方，选择“将任务添加到事件”。

1. 在命令栏上选择“保存”。 将来的实验室中将使用逻辑应用。

### 任务 3：创建自动化规则

1. 在 Microsoft Sentinel 中，转到“配置”下的“自动化”。

1. 选择“创建”，然后选择自动化规则。

1. 为规则命名

1. 将事件提供程序保留为“全部”。

1. 将分析规则名称保留为“全部”。

1. 单击“添加”并选择“And”。

1. 从下拉列表中选择“策略”。

1. 从下拉菜单中选择“**包含**”运算符。

1. 选择以下策略：
    - 侦测
    - 执行
    - 持久性
    - 命令和控制
    - 外泄
    - 预攻击

1. 在“操作”下，选择“运行 Playbook”。

1. 选择“**管理 playbook 权限**链接”

1. 在“管理权限”页上，选择在上一个实验室中创建的“RG-Playbooks”资源组，然后选择“应用”。

1. 从下拉列表中选择 **Defender_XDR_Ransomware_Playbook_SecOps_Tasks** playbook。

1. 选择底部的“应用”。****

在这里，根据你的角色，你将继续执行更多的架构师练习，或者转向分析师练习。

## 继续完成练习 3
