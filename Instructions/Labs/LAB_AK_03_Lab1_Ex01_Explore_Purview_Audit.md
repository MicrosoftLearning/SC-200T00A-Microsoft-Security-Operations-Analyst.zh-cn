---
lab:
  title: 练习 1 - 浏览 Microsoft Purview 审核日志
  module: Learning Path 3 - Mitigate threats using Microsoft Purview
---

# 学习路径 3 - 实验室 1 - 练习 1 - 浏览 Microsoft Purview 审核日志

## 实验室方案

你是一家公司的安全运营分析师，所在公司正在实施 Microsoft Defender XDR 和 Microsoft Purview。 你正在协助 IT 合规性团队的同事配置 Purview 审核（标准）和审核（高级）。 其目标是确保准确记录对医疗保健机构网络中患者数据的所有访问和修改，以满足健康数据保护法规。

### 完成本实验室的预计时间：15 分钟

### 任务 1：启用 Purview 审核日志

在此任务中，你将在 Microsoft 365 安全门户中为 Exchange Online Protection (EOP) 和 Microsoft Defender for Office 365 分配预设安全策略。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 启动 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，转到 Microsoft Defender XDR 门户 (<https://security.microsoft.com>)。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

1. 在导航菜单中，展开“*运营技术*”并选择“**更多资源**”。

1. 在“**更多资源**”窗格中，选择“*Microsoft Purview 门户*”磁贴上的“**打开**”按钮。

1. Microsoft Purview 门户打开时，将显示一条消息，指出“*合规性门户已停用*”。 此消息将超时，并将你重定向到新的 *Microsoft Purview 门户*。

1. 在“*欢迎使用新的 Microsoft Purview 门户*”消息中，选择同意数据流披露条款和隐私声明的选项，然后选择“**立即试用**”。

    ![显示“欢迎使用新的 Microsoft Purview 门户屏幕”的屏幕截图。](../Media/welcome-purview-portal.png)

1. 从左侧边栏中选择“**解决方案**”，然后选择“**审核**”。

1. 在“**搜索**”页上，选择蓝色的“**开始录制用户和管理员活动**”栏以启用审核日志。

    ![显示“开始录制用户和管理员活动”按钮的屏幕截图。](../Media/enable-audit-button.png)

1. 选择此选项后，蓝色栏应从此页面消失。

    >**备注：** 开始录制活动可能需要 60 分钟。

## 你已完成本实验室
