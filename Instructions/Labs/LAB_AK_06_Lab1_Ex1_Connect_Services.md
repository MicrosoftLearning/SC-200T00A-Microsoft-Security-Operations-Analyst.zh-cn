---
lab:
    title: '练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel'
    module: '模块 6 - 将日志连接到 Microsoft Sentinel'
---

# 模块 6 - 实验室 1 - 练习 1 - 使用数据连接器将数据连接到 Microsoft Sentinel

## 实验室场景

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。你需要了解如何连接来自组织中多个数据源的日志数据。组织的数据来自 Microsoft 365、Microsoft 365 Defender、Azure 资源、非 Azure 虚拟机和网络设备。

你计划使用 Microsoft Sentinel 数据连接器集成来自各种源的日志数据。你需要编写用于管理的连接器计划，将组织的每个数据源映射到适当的 Microsoft Sentinel 数据连接器。


### 任务 1：访问 Microsoft Sentinel 工作区。

在此任务中，你将访问 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 打开 Microsoft Edge 浏览器。

3. 在 Microsoft Edge 浏览器中，通过 https://portal.azure.com 导航到 Azure 门户。

4. 在 **“登录”** 对话框中，复制粘贴实验室托管提供者提供的 **租户电子邮件** 帐户，然后选择 **“下一步”**。

5. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者提供的 **租户密码**，然后选择 **“登录”**。

6. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择“**Microsoft Sentinel**”。

7. 选择你在上一个实验室中创建的 Microsoft Sentinel 工作区。


### 任务 2：连接 Azure Active Directory 连接器。

在此任务中，你要将 Azure Active Directory 连接器连接到 Microsoft Sentinel。

1. 在“配置”区域，选择“**数据连接器**”。  在“数据连接器”页面中，从列表搜索 **Azure Active Directory** 连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 从“配置”区域中选择 **“登录日志”** 和 **“审核日志”** 选项，然后选择 **“应用更改”**。


### 任务 3：连接 Azure Active Directory 标识保护连接器。

在此任务中，你要将 Azure Active Directory 标识保护连接器连接到 Microsoft Sentinel。

1. 在“数据连接器”选项卡中，从列表搜索“**Azure Active Directory 标识保护**”连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 从“配置”区域，选择 **“连接”** 按钮。


### 任务 4：连接 Microsoft Defender for Cloud 连接器。

在此任务中，你将连接 Microsoft Defender for Cloud 连接器。

1. 在“数据连接器”选项卡中，从列表搜索 **Microsoft Defender for Cloud** 连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 在订阅下的“配置”区域中，选择你的 Azure 订阅并单击“**连接**”。

4. 阅读“连接”消息并选择“**确定**”以继续。你的 Azure 订阅状态现应为“**已连接**”。

5. 向下滚动，在“创建事件 - 推荐!”区域，选择“**启用**”。


### 任务 5：连接 Microsoft Defender for Cloud Apps 连接器。

在此任务中，你将连接 Microsoft Defender for Cloud Apps 连接器。

1. 在“数据连接器”选项卡中，从列表搜索 **Microsoft Defender for Cloud Apps** 连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 选择 **“警报”**，然后选择 **“应用更改”**。


### 任务 6：连接 Microsoft Defender for Office 365 连接器。

在此任务中，你将连接 Microsoft Defender for Office 365 连接器。

1. 在“数据连接器”选项卡中，从列表搜索“**Microsoft Defender for Office 365 (预览版)**”连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 在“配置”区域，选择 **“连接”**。


### 任务 7：Microsoft Defender for Identity 连接器。

在此任务中，你将查看 Microsoft Defender for Identity 连接器。

1. 在“数据连接器”选项卡中，从列表搜索 **Microsoft Defender for Identity** 连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 查看连接选项。请不要连接。这仅用于了解信息。


### 任务 8：连接 Microsoft Defender for Endpoint 连接器。

在此任务中，你将连接 Microsoft Defender for Endpoint 连接器。

1. 在“数据连接器”选项卡中，从列表搜索 **Microsoft Defender for Endpoint** 连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 在“配置”区域，选择 **“连接”**。


### 任务 9：连接 Microsoft 365 Defender 连接器。

在此任务中，你将连接 Microsoft 365 Defender 连接器。

1. 在“数据连接器”选项卡中，从列表搜索“**Microsoft 365 Defender (预览版)**”连接器并将其选中。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 选择“*名称*”复选框，从而选择 Microsoft Defender for Endpoint 对应的所有复选框。

4. 选择 **“应用更改”**。


### 任务 10：连接“Azure 活动”连接器。

在此任务中，你将连接“Azure 活动”连接器。

1. 在“数据连接器”选项卡中，从列表搜索“**Azure 活动**”连接器并将其选中。

2. 在连接器信息边栏选项卡上选择“**打开连接器页面**”。

3. 在“配置”区域中，选择“**启动 Azure 策略分配向导>**”。

4. 在“**基本信息**”选项卡中，选择“**范围**”下带有三个点的按钮，从下拉列表中选择你的订阅，然后单击“**选择**”。

5. 选择“**参数**”选项卡，从“**主 Log Analytics 工作区**”下拉列表中选择你的 Microsoft Sentinel 工作区。

6. 选择“**修正**”选项卡，并勾选“**创建修正任务**”复选框。

7. 选择“**查看 + 创建**”按钮以查看配置。

8. 选择“**创建**”来完成操作。

## 继续进行练习 2
