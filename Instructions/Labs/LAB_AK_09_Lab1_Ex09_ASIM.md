---
lab:
  title: 练习 9 - 创建 ASIM 分析程序
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 9 - 实验室 1 - 练习 9 - 部署 ASIM 分析程序

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 需要为特定 Windows 注册表事件建模 ASIM 分析程序。 这些分析程序将在稍后按照[高级安全信息模型 (ASIM) 注册表事件规范化架构参考](https://docs.microsoft.com/azure/sentinel/registry-event-normalization-schema)来完成。

>**重要说明：** 学习路径 #9 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

### 完成本实验室的估计时间：30 分钟

### 任务 1：部署注册表架构 ASIM 分析程序

在此任务中，你将查看 Microsoft Sentinel 部署随附的注册表架构分析程序。

>**备注：** 已在名称为 **defenderWorkspace** 的 Azure 订阅中预先部署了 Microsoft Sentinel，并且已安装所需的*内容中心*解决方案。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com> )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择 Microsoft Sentinel **defenderWorkspace**。

<!--- 1. In the Edge browser, open a new tab (Ctrl+T) and navigate to the Microsoft Sentinel GitHub ASIM page <https://github.com/Azure/Azure-Sentinel/tree/master/ASIM>.

 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel).

    >**Note:** In the **ASIM** folder you can deploy templates that contain all ASIM parsers, but we will only focus on the Registry Schema.

1. Scroll down and next to **Registry Event**, select the **Deploy to Azure** button.

1. For *Resource Group*, select **RG-Defender** where your Sentinel workspace resides.

1. For *Workspace*, type your Sentinel workspace name, like *uniquenameDefender*.

1. Leave the other default values and select **Review + create**.

1. Select **Create** to deploy the template. Notice the Names of the different resources. 

1. After the deployment completes return to the *Microsoft Sentinel* tab. --->

1. 选择导航菜单的“*常规*”部分下的“**日志**”。

1. 根据需要选择 >>，打开“架构和筛选器”边栏选项卡。

1. 选择“函数”选项卡（在“表”和“查询”选项卡旁边）。 提示：可能需要选择省略号图标 (...) 才能选择该选项卡 。

1. 在“搜索”栏中键入“注册表”，向下滚动查看 ASIM 分析程序函数，直到在“Microsoft Sentinel”标题下看到 Microsoft Windows 对应以下 _Im_RegistryEvent_MicrosoftWindowsEventxxx。**********

    >**注意：** 我们在 ASIM 分析程序函数名称中使用 xxx 来解释版本更改。 在此实验室更新时，函数为 _Im_RegistryEvent_MicrosoftWindowsEventV02。**

1. 将鼠标悬停在 _Im_RegistryEvent_MicrosoftWindowsEventxxx ASIM 函数上，然后在弹出窗口中选择“加载函数代码”。********

1. 查看正在分析事件 ID 4657 的 KQL，以简化对 Microsoft Sentinel 工作区中的数据的分析。

    >提示****：在代码窗口中键入 ctrl+f 会显示“查找”并让搜索“EventID:**** 4657”变得更容易。

1. 在“日志”** 中打开“新建查询”选项卡。

1. 返回到“架构和筛选器”边栏选项卡，现在将鼠标悬停在 Microsoft Windows 事件和安全事件的 _Im_RegistryEvent_MicrosoftWindowsEventxxx 注册表事件 ASIM 筛选分析程序，然后选择“在编辑器中使用”。************

1. 运行 ASIM 函数查询。**** 如果已完成上一个实验室练习，应会看到结果和无错误消息。

## 继续完成练习 10
