---
lab:
    title: '练习 4 - 使用数据连接器将威胁情报连接到 Microsoft Sentinel'
    module: '模块 6 - 将日志连接到 Microsoft Sentinel'
---

# 模块 6 - 实验室 1 - 练习 4 - 使用数据连接器将威胁情报连接到 Microsoft Sentinel


### 任务 1：连接威胁情报。

在此任务中，你将通过威胁情报 - TAXII 连接器连接威胁情报提供程序。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com)。

3. 在 **“登录”** 对话框中，复制粘贴实验室托管提供者提供的**租户电子邮件**帐户，然后选择 **“下一步”**。

4. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者提供的**租户密码**，然后选择 **“登录”**。

5. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择“**Microsoft Sentinel**”。

6. 选择之前创建的 Microsoft Sentinel 工作区。

7. 在“数据连接器”选项卡中，选择 **“威胁情报 - TAXII”** 连接器。

8. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

9. 在“配置”区域的 **“(服务器)易记名称”** 处输入 *“PhishURLs”*

10. 输入 https://limo.anomali.com/api/v1/taxii2/feeds/ 作为 API 根 URL

11. 输入 **107** 作为集合 ID。

12. 输入 **guest** 作为用户名。

13. 输入 **guest** 作为密码。

14. 限制选择 **“添加”** 按钮。

    将拉取钓鱼 URL 并用其填充 ThreatIntelligenceIndicator 表。

>**备注**：如需更多集合，请在浏览器中打开 https://limo.anomali.com/api/v1/taxii2/feeds/collections/， 使用来宾用户名加密码查看可用的各种集合 ID。

## 你已完成本实验室。
