---
lab:
  title: 练习 2 - 使用 Microsoft Defender for Endpoint 缓解攻击
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# <a name="module-2---lab-1---exercise-2---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>模块 2 - 实验室 1 - 练习 2 - 使用 Microsoft Defender for Endpoint 缓解攻击

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2.png)

你是一家公司的安全操作分析师，你的公司正在实施 Microsoft Defender for Endpoint。 你的主管计划加入一些设备，以深入了解安全运营 (SecOps) 团队响应程序所需的更改。

为了探索 Defender for Endpoint 的攻击缓解功能，你将运行两次模拟攻击。

>**重要：** 请等待 WIN1 显示在“设备”页中，然后再继续。 否则，可能需要重复此任务才能查看稍后生成的警报。


### <a name="task-1-simulated-attacks"></a>任务 1：模拟攻击

在此任务中，你将运行两次模拟攻击，以探索 Microsoft Defender for Endpoint 的功能。

1. 如果尚未访问 Microsoft Edge 浏览器中的 Microsoft 365 Defender 门户，请转到 (https://security.microsoft.com) 并以租户的管理员身份登录。

1. 从菜单中的“终结点”下，选择“评估和教程”，然后从左侧选择“教程和模拟”  。

1. 选择“教程”选项卡。

1. 在“自动调查(后门)”下，你将看到一条描述方案的消息。 在此段落下，单击“阅读演练”。 此时将打开一个新的浏览器选项卡，其中包含执行模拟的说明。

1. 在新浏览器选项卡中，找到名为“运行模拟”（第 5 页，从步骤 2 开始）的部分，并按步骤运行攻击。 提示：模拟文件 RS4_WinATP-Intro-Invoice.docm 可以在门户中找到，就在上一步中选择的“阅读演练”下方，通过选择“获取模拟文件”按钮获取 。 

1. 重复最后 3 步，立即运行“自动调查(无文件攻击)”。


### <a name="task-2-investigate-the-attacks"></a>任务 2：调查攻击

1. 在 Microsoft 365 Defender 门户中，从左侧菜单栏中选择“事件和警报”，然后选择“事件” 。

1. 名为“多阶段事件...”的新事件将显示在右侧窗格中。 单击事件名称以加载其详细信息。

1. 选中“管理事件”按钮，此时将显示一个新的窗口边栏选项卡。 

1. 在“事件标记”下，键入“教程”，然后选择“教程(新建)”创建新标记 。 

1. 选择切换“分配给我”，将用户帐户添加为事件所有者。 

1. 在“分类”下，展开下拉菜单。 

1. 在“参考性预期活动”下，选择“安全测试” 。 

1. 如果需要，请添加注释，然后单击“保存”完成操作。

1. 查看“警报”、“设备”、“用户”、“调查”、“证据和响应”、“图”选项卡的内容。 提示：某些选项卡可能由于显示器的大小而被隐藏。 选择省略号选项卡 (...) 显示它们。

>**警告：** 此处的模拟和教程非常适合实践式学习。  门户中会定期添加和修改模拟和教程。  但其中部分模拟和教程可能会影响为本培训课程设计的实验室的性能。  在使用 Azure 租户提供的课程时，请仅执行为本实验室提供的说明中推荐的模拟和教程。  使用此租户完成本培训课程后，可以参与其他模拟和租户教程。

## <a name="you-have-completed-the-lab"></a>你已完成本实验室。
