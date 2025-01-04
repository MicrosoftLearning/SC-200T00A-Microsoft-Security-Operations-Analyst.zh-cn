---
lab:
  title: 练习 1 - 探索 Microsoft Security Copilot 中的用例
  module: Learning Path 2 - Mitigate threats using Microsoft Security Copilot
---

# 学习路径 2 - 实验室 1 - 练习 1 - 探索 Microsoft Security Copilot

## 实验室方案

你所在的组织希望提高其安全分析员的效率和能力，并改善安全结果。 为了实现这一目标，CISO 办公室确定部署 Microsoft Security Copilot 是实现该目标的关键一步。 作为组织的安全管理员，你负责设置 Copilot。

在本练习中，你将完成 Microsoft Security Copilot 的*第一次运行体验*，以便为 Copilot 预配一个安全计算单位 (SCU)。

>**备注：** 本练习的环境是由产品生成的模拟。 由于是有限的模拟，因此页面上的链接可能未启用，并且不支持超出指定脚本范围的文本输入。 将显示弹出消息，指出“此功能在模拟中不可用。” 发生这种情况时，请选择“确定”并继续执行练习步骤。  
> :::image type="content" source="../media/simulation-pop-up-error.png" alt-text="弹出屏幕的屏幕截图，指示此功能在模拟中不可用。":::

### 完成本实验室的预计时间：45 分钟

### 任务 1：预配 Microsoft Security Copilot

在本练习中，你将以 Avery Howard 身份登录，并具有 Microsoft Entra 中的全局管理员角色。 你将使用 Azure 门户和 Microsoft Security Copilot。

完成此练习大约需要 15 分钟****。

>**备注：** 当实验室说明要求打开模拟环境的链接时，通常建议在新浏览器窗口中打开该链接，这样就可以同时查看说明和练习环境。 为此，请选择鼠标右键，然后选择该选项。

在用户开始使用 Copilot 之前，管理员需要预配和分配容量。 要预配容量：

- 必须具有 Azure 订阅。
- 你需要至少是资源组级别的 Azure 所有者或 Azure 参与者。

在此任务中，你将完成确保你拥有适当角色权限的过程。 首先，启用 Azure 资源的访问管理。

在 Azure 中分配用户访问管理员角色后，可以向用户分配必要的访问权限来为 Copilot 预配 SCU。  你将为自己分配必要的权限，但这仅出于本练习向你展示所涉及步骤的目的。  以下步骤将指导你完成该过程。

1. 通过选择此链接打开模拟环境：[Azure 门户](https://app.highlights.guide/start/6373500f-1f10-4584-a14e-ca0b4aa7399f?link=1&token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)****。

1. 首先，启用 Azure 资源的访问管理。 若要访问此设置，请执行以下操作：
    1. 在 Azure 门户中，选择“Microsoft Entra ID”****。
    1. 在左侧导航面板中，展开“管理”。****
    1. 在左侧导航面板中，向下滚动并选择“属性”****。
    1. 打开“Azure 资源的访问管理”切换开关，然后选择“保存”********。

1. 现在，可以查看所有资源并分配目录的任何订阅或管理组中的访问权限，为自己分配 Azure 订阅的“所有者”角色。
    1. 在页面顶部的蓝色横幅中选择“Microsoft Azure”，返回到 Azure 门户的登陆页面****。
    1. 选择“订阅”，然后选择“Woodgrove - GTP 演示(外部/赞助)”列出的订阅********。
    1. 选择“访问控制(IAM)”。
    1. 依次选择“添加”、“添加角色分配”。
    1. 在“角色”选项卡中，选择“特权管理员角色”****。
    1. 选择“所有者”，然后选择“下一步”********。
    1. 选择“+ 选择成员”。
    1. Avery Howard 是此列表上的名字，请选择该姓名右侧的 **+**。  Avery Howard 现在列在所选成员下。 选择“选择”按钮，然后选择“下一步”********。
    1. 选择“允许用户分配除特权管理员角色、所有者、UAA、RBAC 之外的所有角色(推荐)”****。
    1. 选择“查看 + 分配”，然后再最后选择一次“查看 + 分配”********。

作为 Azure 订阅的所有者，你现在可以在 Copilot 中预配容量。

#### 子任务 1：预配容量

在此任务中，你将完成为组织预配容量的步骤。 预配容量有两个选项：

- 在 Security Copilot 中预配容量（建议）
- 通过 Azure 预配容量

在本练习中，你将通过 Security Copilot 预配容量。 首次打开 Security Copilot 时，向导会指导你完成为组织设置容量的步骤。

1. 通过选择此链接打开模拟环境：****[Microsoft Security Copilot](https://app.highlights.guide/start/6373500f-1f10-4584-a14e-ca0b4aa7399f?link=0&token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)。

1. 按照向导中的步骤操作，选择“开始”****。
1. 在此页上，设置安全容量。 对于下面列出的任何字段，可以选择信息图标来了解详细信息。
    1. Azure 订阅：从下拉列表中选择“Woodgrove - GTP 演示（外部/赞助）”。****
    1. 资源组：从下拉列表中选择“RG-1”。****
    1. 容量名称：输入容量名称。
    1. 提示评估位置 [地理位置]：从下拉列表中选择你的区域。
    1. 可以选择是否要选择以下选项：“如果此位置的流量太大，则允许 Copilot 评估世界任何地方的提示(为获得最佳性能建议这样做)”。
    1. 容量区域是根据所选位置设置的。
    1. 安全计算：此字段会自动填充为所需的最小 SCU 单位，即 1。 保留值为“**1**”的字段。
    1. 选中“我确认我已阅读、理解并同意条款和条件”复选框。****
    1. 选择页面右下角的“继续”。****

1. 该向导会显示有关客户数据的存储位置的信息。 显示的区域基于你在“提示评估”字段中选择的区域。 选择“继续”。

1. 可以选择有助于改进 Copilot 的选项。 可以根据自己的偏好选择切换。  选择“继续”。

1. 作为初始设置的一部分，Copilot 默认为每个人提供参与者访问权限，并添加全局管理员和安全管理员作为 Copilot 所有者。 在生产环境中，完成初始设置后，可以更改权访问 Copilot 的人员。 选择“继续”。
1. 你已完成所有设置！ 选择“完成”。
1. 关闭浏览器选项卡，因为下一个练习将使用指向类似实验室的环境的单独链接。

### 任务 2：探索 Microsoft Security Copilot 的独立体验。

组织的安全管理员已预配 Copilot。 由于你是团队的高级分析员，管理员将你添加为 Copilot 所有者，并要求你熟悉解决方案。

在本练习中，你将探索 Microsoft Security Copilot 独立体验登陆页面中的所有重要功能。

你以 Avery Howard 的身份登录，拥有 Copilot 所有者角色。 你将使用 Microsoft Security Copilot 的独立体验。

完成此练习大约需要 15 分钟****。

#### 子任务 1：浏览菜单选项

在此任务中，你将开始在主菜单中进行浏览。

1. 通过选择此链接打开模拟环境：**[Microsoft Security Copilot](https://app.highlights.guide/start/2cac767e-42c4-4058-afbb-a9413aac461d?link=0&token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)**。

1. 选择“**菜单**”图标 ![主菜单图标](../media/home-menu-icon.png)，有时称为汉堡图标。

1. 选择“我的会话”并记下可用选项****。
    1. 选择“最近”以查看最新会话
    1. 选择筛选器并记下可用选项，然后关闭筛选器。
    1. 选择主菜单图标以打开主菜单。

1. 选择“提示本库”****。
    1. 选择“我的提示本”。 后续任务将深入探讨提示本。
    1. 选择“Woodgrove”。
    1. 选择 Microsoft 。
    1. 选择筛选器以查看可用选项，然后选择 X 关闭。
    1. 选择主菜单图标以打开主菜单。

1. 选择“所有者设置”****。 作为 Copilot 所有者，你可以使用这些设置。 Copilot 参与者无法访问这些菜单选项。
    1. 对于 Security Copilot 的插件，选择“谁可以添加和管理自定义插件”的下拉菜单，以查看可用选项。
    1. 为组织中的每个人选择“谁可以添加和管理自定义插件”的下拉菜单，以查看可用选项。 请注意，如果“谁可以添加和管理自定义插件”设置为“仅所有者”，则此选项将为灰显状态。
    1. 选择“允许 Security Copilot 访问 Microsoft 365 服务中的数据”旁边的信息图标。  如果要使用 Microsoft Purview 插件，则必须启用此设置。 在后面的练习中，你将使用此设置。
    1. 选择“谁可以添加和管理自定义插件”的下拉菜单，查看可用选项。
    1. 选择主菜单图标以打开主菜单。

1. 选择“角色分配”****。
    1. 选择“添加成员”，然后关闭。
    1. 展开所有者。
    1. 展开参与者。
    1. 选择主菜单图标以打开主菜单。

1. 选择“使用情况监视”****。
    1. 选择日期筛选器以查看可用选项。
    1. 选择主菜单图标以打开主菜单。

1. 选择“设置”。
    1. 选择“首选项”。 向下滚动以查看可用选项。
    1. 选择“数据和隐私”。
    1. 选择关于。
    1. 选择 X 以关闭“首选项”窗口。

1. 选择主菜单左下角显示**Woodgrove**的位置。
    1. 选择此选项时，会看到租户。 这称为租户切换器。 在这种情况下，Woodgrove 是唯一可用的租户。
    1. 选择“主页”以返回到登陆页面****。

#### 子任务 2：浏览对最新会话的访问权限

在登陆页面的中心，有表示最新会话的卡片。

1. 最大的卡片是最后一个会话。 选择任何会话卡片的标题会使你进入该会话。
1. 选择“查看所有会话”以转到“我的会话”页面****。
1. 在主菜单图标旁边选择“Microsoft Copilot for Security”，以返回到登陆页面****。

#### 子任务 3：浏览对提示本的访问权限

Copilot 登陆页面的下一部分围绕提示本展开。 登陆页面显示某些 Microsoft 安全提示本的磁贴。 在这里，你将浏览对提示本和提示本库的访问权限。 在后续练习中，你将了解如何创建和运行提示本。

1. “开始使用这些提示本”的右侧是向左和向右箭头键，可用于滚动浏览 Microsoft 安全提示本的磁贴。 选择**向右键 >**

1. 每个磁贴显示提示本的标题、简要描述、提示数量和运行图标。 选择任何提示本磁贴的标题以打开该提示本。 例如，选择“漏洞影响评估”****。
    1. 所选提示本的窗口将提供信息，包括提示本的创建者、标记、简要描述、运行提示本所需的输入以及提示列表。
    2. 记下有关提示本和可用选项的信息。 对于此模拟，你无法启动新会话，你将在后续练习中执行此操作。 
    1. 选择“X”关闭窗口****。

1. 选择“查看提示本库”****。
    1. 若要查看你拥有的提示本，请选择“我的提示本”。
    1. 选择“Woodgrove”，查看 Woodgrove（一个虚构组织的名称）拥有的提示本列表。
    1. 若要查看内置的、Microsoft 拥有/开发的提示本，请选择“Microsoft”。
    1. 选择“筛选”图标。 可以在此处根据分配给工作簿的标记进行筛选。 通过选择“新建筛选器”选项卡中的 X 关闭筛选器窗口。
    1. 在主菜单图标旁边选择“Microsoft Copilot for Security”，以返回到登陆页面****。

#### 子任务 4：浏览提示栏中的提示和源图标

提示栏位于页面底部的中心。 提示栏包含你在此任务中浏览的提示和源图标。 在后续练习中，你将直接在提示栏中输入输入。

1. 在提示栏中，可以选择提示图标以选择内置提示或提示本。 选择**提示图标**![提示图标](../media/prompt-icon.png)。
    1. 选择“查看所有提示本”****
        1. 滚动以查看所有可用的提示本。
        1. 选择搜索栏旁边的后退箭头以返回****。
    1. 选择“**查看所有系统功能**”。 该列表显示所有可用的系统功能（这些功能实际上是你可以运行的提示）。 许多系统功能与特定插件相关，因此只有启用相应的插件才会列出此类功能。
        1. 滚动以查看所有可用的提示本。
        1. 选择搜索栏旁边的后退箭头以返回****。

1. 选择**源图标**![源图标](../media/sources-icon.png)。
    1. 选择源图标将打开“管理源”窗口。 你可以在此处访问“插件”或“文件”。 默认情况下，选择“插件”选项卡****。
        1. 选择是否要查看所有插件、已启用（打开）的插件，或已禁用（关闭）的插件。
        1. 展开/折叠 Microsoft、非 Microsoft 和自定义插件的列表。
        1. 某些插件需要配置参数。 选择 Microsoft Sentinel 插件的“设置”图标以查看设置窗口****。 选择“取消”可关闭“设置”窗口****。 你将在单独的练习中配置插件。
    1. 你仍应位于“管理源”窗口中。 选择“文件”。
        1. 查看说明。
        1. 文件可以上传并用作 Copilot 的知识库。 在后续练习中，你将使用文件上传。
        1. 选择“X”关闭“管理源”窗口****。

#### 子任务 5：浏览帮助功能

窗口右下角是帮助图标，可以通过它轻松查看文档并找到常见问题的解决方案。 如果具有适当的角色权限，还可以通过帮助图标向 Microsoft 支持团队提交支持案例。

1. 选择“帮助(?)”图标****。
    1. 选择**文档**。 此选择将打开 Microsoft Security Copilot 文档的新浏览器选项卡。 返回到 Microsoft Security Copilot 浏览器选项卡。
    1. 选择“帮助”****。
        1. 有权访问 Security Copilot 的任何人都可以通过选择帮助图标并选择“帮助”选项卡来访问自助小组件。可以在此处输入有关问题的一些信息来找到常见问题的解决方案。
        1. 具有服务支持管理员或帮助台管理员角色的最低角色的用户可以向 Microsoft 支持团队提交支持案例。 如果具有此角色，将显示耳机图标。 关闭联系支持人员页面。

### 任务 3：探索 Microsoft Security Copilot 的嵌入式体验。

在本练习中，你将调查 Microsoft Defender XDR 中的事件。 在调查过程中，你将探索 Microsoft Defender XDR 中 Microsoft Copilot 的主要功能，包括事件摘要、设备摘要、脚本分析等。 还可以将调查转向独立体验，并使用图钉板与同事共享调查详细信息。

你以 Avery Howard 的身份登录，拥有 Copilot 所有者角色。 你将在 Microsoft Defender 中使用新的统一安全运营平台来访问 Microsoft Defender XDR 中的嵌入式 Copilot 功能。 在本练习结束时，转向 Microsoft Security Copilot 的独立体验。

完成此练习大约需要 30 分钟。

#### 子任务 1：探索事件摘要和引导式响应

1. 通过选择此链接打开模拟环境：**[Microsoft Defender 门户](https://app.highlights.guide/start/f4f590f6-8937-40f9-91ec-632de546ab98?token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)**。

1. 来自 Microsoft Defender 门户：
    1. 展开调查**** 和响应。
    1. 展开“**事件和警报**”。
    1. 选择“事件”。

1. 选择列表中的第一个事件，**** 事件 ID：30342，名为“人为操作的勒索软件攻击从被盗用资产发起(攻击中断)”。

1. 这是一个复杂事件。 Defender XDR 提供了大量信息，但有 72 个警报，难以确定重点。 在事件页面的右侧，Copilot 会自动生成一个“事件摘要”，可帮助指导如何抓住重点和进行应对****。 选择**查看更多**。
    1. Copilot 的摘要描述了此事件是如何演变的，包括初始访问、横向移动、收集、凭据访问和外泄。 它可标识特定设备，指示 PsExec 工具用于启动可执行文件等。
    1. 这些都是可用于进一步调查的项目。 在接下来的任务中，你将对其中的一些项目进行探索。

1. 向下滚动 Copilot 面板，摘要下方就是“引导式响应”****。 引导式响应会提出一些支持会审、遏制、调查和修正的操作建议。
    1. 会审类别中的第一项就是“对此事件进行分类”。 选择“分类”以查看选项****。 查看其他类别中的引导式响应。
    1. 选择引导式响应部分顶部的“状态”**** 按钮，并筛选“已完成”****。 两个已完成的活动显示标记为“攻击中断”。 自动攻击中断旨在遏制正在进行的攻击，限制对组织资产的影响，并为安全团队提供更多时间来全面修正攻击。
1. 使事件页面保持打开状态，因为在下一个任务中会用到。

#### 子任务 2：探索设备和标识摘要

1. 在事件页面中，选择第一个警报“点击了可疑的 URL”****。

1. Copilot 会自动生成“**警报摘要**”，以提供大量信息来进行进一步分析。 例如，摘要会标识可疑活动，还会标识数据收集活动、凭据访问、恶意软件、发现活动等。

1. 该页面上有很多信息，因此若要更好地了解此警报，请选择“打开警报页面”****。 它位于警报页面的第三个面板上，靠近事件图，在警报标题下方。

1. 页面顶部是设备 parkcity-win10v 的卡片。 选择省略号并注意相关选项。 选择“汇总”****。 Copilot 可生成设备摘要。**** 值得注意的是，访问设备摘要有多种方法，而这只是其中一种方便的方法。 摘要显示了设备是一个 VM，标识了设备的所有者，还显示了其针对 Intune 策略的合规性状态等。

1. 设备卡片旁边是设备所有者的卡片。 选择“parkcity\jonaw”****。 页面上的第三个面板将从显示警报详细信息更新为提供用户 Jonathan Wolcott 的信息，该用户为客户主管，其 Microsoft Entra ID 风险和内部风险严重性分类为高。 从在 Copilot 事件和警报摘要中了解到的情况来看，这些并不奇怪。 选择省略号，然后选择“**汇总**”，获取 Copilot 生成的标识摘要。

1. 使警报页面保持打开状态，因为在下一个任务中会用到。

#### 子任务 3：探索脚本分析

1. 让我们重点介绍警报案例。 选择“**最大化![最大化图标](../media/maximize-icon.png)**”（位于警报的主面板上，标记为“partycity\jonaw”的卡片下方），以便更好地了解进程树。 在最大化视图中，可以更清楚地了解此事件是如何发生的。 许多行项都指示 powershell.exe 执行了脚本。 由于用户 Jonathan Wolcott 是一名客户主管，因此我们有理由认为该用户不可能经常执行 PowerShell 脚本。

1. 展开“powershell.exe 执行脚本”的第一个实例，该实例显示的时间戳是凌晨 4:57:11****。 Copilot 能够分析脚本。 选择“分析”。
    1. Copilot 会生成脚本分析，并提示这可能是网络钓鱼尝试或用于发动基于 Web 的攻击。
    1. 选择“显示代码”****。 该代码显示了一个已经过安全处理的 URL。

1. 还有其他几个项指示 powershell.exe 执行了脚本。 展开标记了“powershell.exe -EncodedCommand...”且时间戳为凌晨 5:00:47 的项****。 原始脚本是 Base64 编码的，但 Defender 已为你解码了此脚本。 对于解码的版本，请选择“分析”****。 分析突出显示了此攻击所使用的脚本的复杂性。

1. 选择“X”（Copilot 面板左侧的 X）关闭警报案例页面****。 现在，使用痕迹导航返回事件。 选择“人为操作的勒索软件攻击从被盗用资产发起(攻击中断)”****。

#### 子任务 4：探索文件分析

1. 你回到了事件页面。 在警报摘要中，Copilot 标识了与“Kekeo”恶意软件关联的文件 Rubeus.exe。 可以使用 Defender XDR 中的文件分析功能看看还能获得哪些其他见解。 可通过多种方式访问文件。 在页面顶部，选择“证据和响应”选项卡****。

1. 在屏幕左侧选择“文件”****。
1. 从带有名为 Rubeus.exe**** 实体的列表中选择第一项。
1. 在打开的窗口中，选择“分析”。**** Copilot 会生成摘要。
1. 查看 Copilot 生成的详细文件分析。
1. 关闭文件分析窗口。

#### 子任务 5：转到独立体验

这项任务很复杂，需要更多高级分析师的参与。 在此任务中，你将转移调查方向并运行 Defender 事件提示本，以便其他分析师在调查时有个好的开始。 将响应固定到图钉板，并生成指向此调查的链接，你可以与团队中更高级的成员共享此链接以帮助调查。

1. 从页面顶部选择“攻击案例”选项卡，返回到事件页面****。

1. 选择 Copilot 事件摘要旁边的省略号，然后选择“在安全 Copilot 中打开”****。

1. Copilot 会在独立体验中打开，并显示事件摘要。 还可以运行更多提示。 在这种情况下，要运行事件提示本。 选择**提示图标**![提示图标](../media/prompt-icon.png)。 
    1. 选择“查看所有提示本”****。
    1. 选择“Microsoft 365 Defender 事件调查”****。
    1. 此时会打开提示本页面并要求输入 Defender 事件 ID。 输入“30342”，然后选择“运行”********。
    1. 查看所提供的信息。 通过转向独立体验并运行提示本，调查能够基于已启用的插件，从更广泛的安全解决方案调用功能，而不仅仅是从 Defender XDR。

1. 选择图钉图标旁边的**方框图标![方框图标](../media/box-icon.png)**，以选择所有提示和相应的响应，然后选择**图钉图标![图钉图标](../media/pin-icon.png)**，将这些响应保存到图钉板。

1. 图钉板会自动打开。 图钉板会存储你保存的提示和响应，以及每个提示和响应的摘要。 可以通过选择**图钉板图标![图钉板图标](../media/pinboard-icon.png)**来打开和关闭图钉板。

1. 在页面顶部，选择“共享”，查看相关选项****。 通过链接或电子邮件共享事件，组织中具有 Copilot 访问权限的人员就可以查看此会话。 选择“x”关闭窗口****。

1. 现在可以关闭浏览器标签页以退出模拟。

## 摘要及其他资源

在本练习中，你探索了Microsoft Security Copilot、预配容量的第一次运行体验，并探索了 Copilot 的独立和嵌入式体验。 你在 Microsoft Defender XDR 中调查了事件，浏览了事件摘要、设备摘要、脚本分析等。 还可以将调查转向独立体验，并将图钉板作为与同事共享调查详细信息的一种方式。

若要运行其他 Microsoft Security Copilot 用例模拟，请转到“[浏览 Microsoft Security Copilot 用例模拟](/training/modules/security-copilot-exercises/)”