---
lab:
  title: 练习 2 - 使用 Microsoft Defender for Endpoint 缓解攻击
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# 学习路径 2 - 实验室 1 - 练习 2 - 使用 Microsoft Defender for Endpoint 缓解攻击

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

你是一家公司的安全操作分析师，你的公司正在实施 Microsoft Defender for Endpoint。 你的主管计划加入一些设备，以深入了解安全运营 (SecOps) 团队响应程序所需的更改。

要探索 Defender for Endpoint 攻击缓解功能，你将验证设备载入是否成功，并调查在该过程中创建的警报和事件。

>**注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。

### 任务 1：验证设备加入

在此任务中，你将确认设备已成功加入并创建测试警报。

1. 如果尚未访问 Microsoft Edge 浏览器中的 Microsoft Defender XDR 门户，请转到 (https://security.microsoft.com) 并以租户的管理员身份登录。

1. 在左侧菜单的“资产”区域下，选择“设备” 。 请等到 WIN1 出现在“设备”页面中，然后再继续操作。 否则，可能需要重复此任务以查看稍后将生成的警报。

    >**注意：** 如果你已完成载入过程，但在一小时后未在“设备”列表中看到设备，这可能指示存在载入或连接问题。

1. 从左侧菜单栏中选择“设置”，然后从“设置”页面中选择“终结点” 。

1. 在“设备管理”部分选择“加入”，并确保选择“Windows 10 和 11”作为操作系统。 “第一个设备已加入”消息现在显示“已完成” 。

1. 向下滚动，在“2. 运行检测测试”部分，选择“复制”按钮以复制检测测试脚本。  

1. 在 WIN1 虚拟机的 Windows 搜索栏中，键入“CMD”，然后在命令提示符应用的右窗格上，选择“以管理员身份运行” 。

1. 显示“用户帐户控制”窗口时，选择“是”以允许应用运行。 

1. 粘贴脚本的方法是右键单击“管理员:**命令提示符”窗口，并按 Enter 键运行** 。

    >**注意：** 该窗口会在成功运行脚本后自动关闭，并在几分钟后，在 Microsoft Defender XDR 门户中生成警报。

<!--- ### Task 2: Simulated Attacks

>**Note:** The Evaluation lab and the Tutorials & simulations section of the portal is no longer available. Please refer to the **[interactive lab simulation](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** for a demonstration of the simulated attacks.

1. From the left menu, under **Endpoints**, select **Evaluation & tutorials** and then select **Tutorials & simulations** from the left side.

1. Select the **Tutorials** tab.

1. Under *Automated investigation (backdoor)* you will see a message describing the scenario. Below this paragraph, click **Read the walkthrough**. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named **Run the simulation** (page 5, starting at step 2) and follow the steps to run the attack. **Hint:** The simulation file *RS4_WinATP-Intro-Invoice.docm* can be found back in portal, just below the **Read the walkthrough** you selected in the previous step by selecting the **Get simulation file** button.

    <!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### 任务 2：调查警报和事件

在此任务中，你将调查上一任务中载入检测测试脚本生成的警报和事件。

1. 在 Microsoft Defender XDR 门户中，从左侧菜单栏中选择“事件和警报”，然后选择“警报”********。

1. 在“警报”窗格中，选择名为“可疑 PowerShell”命令行”的警报以加载其详细信息******。

1. 查看“警报情景”时间线，然后查看“详细信息”和“建议”选项卡******。

    >**注意：** 在警报“详细信息”选项卡下，可以向下滚动到“事件详细信息”部分，然后选择“一个终结点上的执行事件”链接以打开该事件******。

1. 在 Microsoft Defender XDR 门户中，从左侧菜单栏选择“事件和警报”，然后选择“事件”********

1. 右侧窗格中会出现名为“一个终结点上的执行事件”的新事件**。 选择事件名称以加载其详细信息。

1. 选择“管理事件”链接（带有铅笔图标），并显示一个新的窗口边栏选项卡****。

1. 在“事件标记”下，键入“模拟”，然后选择“模拟(新建)”以创建新标记。********

1. 选择切换“分配给”，将用户帐户（我）添加为事件所有者。

1. 在“分类”下，展开下拉菜单。

1. 在“参考性预期活动”下，选择“安全测试” 。

1. 根据需要添加任何注释，然后选择“保存”以更新事件并结束。

1. 查看“攻击情景、警报、资产、调查、证据和响应”以及“摘要”选项卡的内容。 设备和用户位于“资产”选项卡下**。在实际事件中，“攻击情景”选项卡会显示“事件图”****。 提示：某些选项卡可能由于显示器的大小而被隐藏。 选择省略号选项卡 (...) 显示它们。

<!---    >**Warning:** The simulated attacks here are an excellent source of learning through practice. Only perform the attacks in the instructions provided for this lab when using the course provided Azure tenant.  You may perform other simulated attacks *after* this training course is complete with this tenant. --->

## 你已完成本实验室
