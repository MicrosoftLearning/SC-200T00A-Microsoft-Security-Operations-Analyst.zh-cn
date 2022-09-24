# <a name="module-2-demo---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>模块 2 演示 - 使用 Microsoft Defender for Endpoint 缓解攻击



备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。 

## <a name="simulated-attacks"></a>模拟攻击

在此任务中，你将运行一次模拟攻击来探索 Microsoft Defender for Endpoint 的功能。

1. 如果你还未在浏览器中打开 Microsoft Defender 安全中心，请转到 Microsoft Defender 安全中心 (https://security.microsoft.com) )，并以租户管理员的身份登录。

1. 从菜单中的“终结点”下，选择“评估和教程”，然后从左侧选择“教程和模拟”  。

1. 选择“教程”选项卡。

1. Under <bpt id="p1">*</bpt>Automated investigation (backdoor)<ept id="p1">*</ept> you will see a message describing the scenario. Below this paragraph, click <bpt id="p1">**</bpt>Read the walkthrough<ept id="p1">**</ept>. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named <bpt id="p1">**</bpt>Run the simulation<ept id="p1">**</ept> (page 5, starting at step 2) and follow the steps to run the attack. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The simulation file <bpt id="p2">*</bpt>RS4_WinATP-Intro-Invoice.docm<ept id="p2">*</ept> can be found back in portal, just below the <bpt id="p3">**</bpt>Read the walkthrough<ept id="p3">**</ept> you selected in the previous step by selecting the <bpt id="p4">**</bpt>Get simulation file<ept id="p4">**</ept> button.

    1. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> After executing the file with the  exploit, you can return to the <bpt id="p2">[</bpt>Microsoft 365 Defender Security Center<ept id="p2">](https://security.microsoft.com)</ept> and click on the <bpt id="p3">**</bpt>Incidents<ept id="p3">**</ept> tab to see the alerts. The guide incorrectly references the <bpt id="p1">*</bpt>Microsoft Defender ATP portal<ept id="p1">*</ept> which has been migrated and rebranded.
    1. Open the incident page and click <bpt id="p1">**</bpt>Manage Incident<ept id="p1">**</ept>. Click <bpt id="p1">**</bpt>Resolve incident<ept id="p1">**</ept> to resolve all of the active alerts.


## <a name="you-have-completed-the-demo"></a>你已完成本演示。