---
lab:
  title: 练习 1 - 启用 Microsoft Defender for Cloud
  module: Learning Path 5 - Mitigate threats using Microsoft Defender for Cloud
---

# 学习路径 5 - 实验室 1 - 练习 1 - 启用 Microsoft Defender for Cloud

## 实验室方案

你是一名安全运营分析师，所在公司正在使用 Microsoft Defender for Cloud 实现云工作负载保护。 在此实验室中，你将启用 Microsoft Defender for Cloud。

>**重要说明：** 学习路径 #5 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

### 完成本实验室的估计时间：25 分钟

### 任务 1：连接到本地服务器

在此任务中，将把本地服务器连接到 Azure 订阅。 Azure Arc 已在此服务器上预安装。 服务器将在下一练习中使用，以提供用于应用合规性标准和工作负荷保护的资源。

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 在引用选项卡中查找虚拟机名称。

1. 使用以下密码以管理员身份登录到 WINServer 虚拟机：Passw0rd! 如有必要。  

如上所述，已在 **WINServer** 计算机上安装了 Azure Arc。 现在，将把此计算机连接到 Azure 订阅。

1. 在 *WINServer* 计算机上，选择“*搜索*”图标并键入 **cmd**。

1. 在搜索结果中，右键单击“*命令提示符*”，然后选择“**以管理员身份运行**”。

1. 在命令提示符窗口中，键入以下命令。 *请勿按 Enter*：

    ```cmd
    azcmagent connect -g "defender-RG" -l "EastUS" -s "Subscription ID string"
    ```

1. 将“**订阅 ID 字符串**”替换为实验室主机托管服务提供商提供的“*订阅 ID*”（*资源选项卡）。 请确保保留引号。

1. 键入 **Enter** 以运行命令（这可能需要几分钟时间）。

    >**备注**：如果看到“*如何打开此内容？*”浏览器选择窗口，请选择 **Microsoft Edge**。

1. 在“*登录*”对话框中，输入实验室托管提供商提供的“**租户电子邮件**”和“**租户密码**”，然后选择“**登录**”。 等待“*身份验证完成*”消息，关闭浏览器选项卡并返回到“*命令提示符*”窗口。

1. 命令运行完成后，将“*命令提示符*”窗口保持打开状态，并键入以下命令以确认连接是否成功：

    ```cmd
    azcmagent show
    ```

1. 在命令输出中，验证“*代理状态*”是否为“**已连接**”。

### 任务 2：启用 Microsoft Defender for Cloud

在此任务中，你将启用和配置 Microsoft Defender for Cloud。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：Pa55w.rd 。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com> )。
  
1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

1. 在 Microsoft Azure 门户的搜索栏中，键入 *Defender*，然后选择“Microsoft Defender for Cloud”****。

1. 在 Microsoft Defender for Cloud 的左侧导航菜单中展开“*管理*”部分，选择“**环境设置**”。

1. 选择“**展开所有**”按钮以查看所有订阅和资源。

1. 选择 **MOC Subscription-lodxxxxxxxx** 订阅（或语言中的等效名称）。

1. 查看现在受 Defender for Cloud 计划保护的 Azure 资源。

<!---
    >**Important:** If all Defender plans are *Off*, select **Enable all plans**. Select the *$200/month Microsoft Defender for APIs Plan 1* and then select **Save**. Select **Save** at the top of the page and wait for the *"Defender plans (for your) subscription were saved successfully!"* notifications to appear.--->

1. 在“*云安全态势管理 (CSPM)*”部分中，为“*Defender CSPM*”选择“**开启**”。

1. 在“*云工作负载保护 (CWP)*”部分中，为“*服务器计划 2*”选择“**开启**”。

1. 选择页面顶部的“**保持**”按钮。

1. 从“设置”区域（“保存”旁边）选择“设置和监视”选项卡。

1. 查看监视扩展。 它包括虚拟机、容器和存储帐户的配置。

1. 选择“**继续**”按钮，或通过选择页面右上角的“X”，关闭“设置和监控”页面。

1. 选择页面右上角的“X”关闭设置页面，以返回“**环境设置**”。

<!---1. Select the Log analytics workspace you created earlier *uniquenameDefender* to review the available options and pricing.

1. Select **Enable all plans** (to the right of Select Defender plan) and then select **Save**. Wait for the *"Microsoft Defender plan for workspace uniquenameDefender were saved successfully!"* notification to appear.

    >**Note:** If the page is not being displayed, refresh your Edge browser and try again.

1. Close the Defender plans page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**. --->

### 任务 3：了解 Microsoft Defender for Cloud 仪表板

1. 在 Microsoft Azure 门户的搜索栏中，键入 *Defender*，然后选择 **Microsoft Defender for Cloud**。

1. 在Microsoft Defender for Cloud 的左侧导航菜单中，在“常规”** 部分选择“概述”****。

1. “概述”边栏选项卡提供安全态势的统一视图，并包括多个独立的云安全支柱，例如安全态势、法规合规性、工作负载保护、防火墙管理器、清单和信息保护（预览版）。 每个支柱都有其专用仪表板，允许在垂直方向上有更深入的见解和操作，为安全专业人员提供便捷的访问和更好的可见性。

    >**注意：** 顶部菜单栏允许通过选择“订阅”按钮来查看和筛选订阅。 在此实验室中，我们将仅使用一个订阅，但选择不同/其他订阅将调整界面以反映所选订阅的安全态势

1. 单击“新增内容”**** 图标链接 – 此时会打开一个新选项卡，其中包含最新的发行说明，你可以通过它随时了解新功能、bug 修复等。

    >**注意：** 顶部菜单中的高级别数目；此视图允许你查看订阅摘要、可用建议以及连接的云帐户旁边的安全警报。

1. 从顶部菜单栏中，选择“Azure 订阅”****。 这会将你引入可从可用订阅中选择的环境设置。

1. 返回到“概述”**** 页，并查看“安全态势”**** 磁贴。 可以看到当前的*安全功能分数*以及已完成的控制和建议的数量。 选择此磁贴会将你重定向到跨订阅的向下钻取视图中

    >**备注：**“*安全状况*”磁贴上的安全功能分数和其他信息可能需要长达 24 小时才能计算。 它在此实验室期间可能不会完全填充。

1. 在“法规合规性”**** 磁贴上，你可以根据对 Azure 和混合云环境的持续评估来深入了解合规性状况。 此磁贴显示了以下标准，这些标准是 Microsoft Cloud 安全基准和最低合规性法规标准。 若要查看数据，我们首先需要添加安全策略。

1. 选择此磁贴会将你重定向到“法规合规性”**** 仪表板 ，你可以在其中添加其他标准并浏览当前标准

1. 在下一练习中，我们将继续探索 *Microsoft Defender for Cloud*** 安全态势**和**法规合规性**。

## 继续进行练习 2
