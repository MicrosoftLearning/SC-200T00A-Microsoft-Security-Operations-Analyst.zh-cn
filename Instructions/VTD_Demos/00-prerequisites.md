
# Microsoft 安全运营分析师
培训师准备指南

## 目的

本文档适用于准备在 Microsoft 安全虚拟培训日讲授 `Defend Against Threats with Extended Detection and Response` 和 `Configure Security Operations Using Microsoft Sentinel` 的演示者。 本文档是“SC-200：Microsoft 安全操作分析师”认证课程的一部分。

## 演示先决条件

本课程的实验室需要 Microsoft 365 E5 许可的租户以及 Azure 订阅。

* 你可以为自己申请 Microsoft Learning Azure Pass。
* 确保至少在进行演示前两周申请上述 Azure Pass。 收到 Pass 后，需要激活它。 
* Azure Pass 的实际功能与公开可用的 Microsoft Azure 试用版订阅相同。 这意味着通行证的功能有限。
* 实验室说明在 [SC-200 Microsoft Learning GitHub 存储库](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/)中。
* 确保将用于演示的计算机安装了新的 Microsoft Edge 浏览器。

## 激活 Azure Pass

## 部署 Defender for Endpoint

### 获取 Microsoft 365 凭据

启动实验室后，Microsoft 虚拟实验室环境中将提供一个免费试用租户可供你访问。 系统会自动向该租户分配一个唯一用户名和密码。 你需要检索此用户名和密码，以便在 Microsoft 虚拟实验室环境中登录 Azure 和 Microsoft 365。

由于此课程可能由学习合作伙伴使用几个授权实验室托管提供者中的任何一个提供，因此，检索与租户关联的租户 ID 的相关实际步骤可能会因实验室托管提供者而有所不同。 因此，讲师将在课程中为你提供有关如何检索此信息的必要说明。 你应该记录以供稍后使用的信息包括：

    - 租户后缀 ID。 此 ID 适用于将在整个实验室中用于登录 Microsoft 365 的 onmicrosoft.com 帐户。 其格式为 {username}@M365xZZZZZZ.onmicrosoft.com，其中 ZZZZZZ 是实验室托管提供者提供的唯一租户后缀 ID。 记录此 ZZZZZZ 值以供稍后使用。 当有任何实验室步骤指示你登录 Microsoft 365 门户时，都必须输入在此处获取的 ZZZZZZ 值。
    - 租户密码。 这是由实验室托管提供者提供的管理员帐户的密码。
    

### 初始化 Microsoft Defender for Endpoint

在此任务中，你将执行 Microsoft Defender for Endpoint 的初始化。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，转到 Microsoft 365 Defender 门户 (https://security.microsoft.com) )。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

在 Microsoft 365 Defender 门户的左侧导航菜单中，选择“主页” 。

    >**Note:** You may need to scroll all the way to the menu top.

1. 在门户“主页”上，会显示“欢迎使用 Microsoft 365 Defender” 。

1. 向下滚动图块，直到找到标记为“Microsoft 365 Defender”并显示“启用 Microsoft 365 Defender”消息的图块 。

    >提示：它应位于图块的右下角。

1. 选择显示“启用新功能”的按钮。

1. 你将在页面顶部看到简要显示了“正在加载和初始化”消息，然后你将咖啡杯的图像和一条消息，内容如下：“请稍等！我们正在为你的数据准备新的空间并将它们连接起来”。 大约需要 5 分钟才能完成。 使页面保持打开状态并确保它已完成，因为下一个实验室需要它。

    >**注意：** 如果未显示消息“请稍候！ 我们正在为你的数据准备新空间并连接它们”，或者虽然“设置”>“Microsoft 365 Defender”>“帐户”页已打开，但你看到消息“无法加载数据存储位置。 请稍后重试”，请从”常规“菜单中选择”警报服务设置“，或转到导航菜单，向下滚动到“资产”部分并选择”设备”。

1. 新空间成功完成后，你将看到 Microsoft 365 Defender 的帐户、电子邮件通知、警报服务设置、权限和角色以及流式处理 API 等常规设置。 你还将看到“预览功能”已打开。

注意：在托管实验室环境中，系统应已为你选择数据存储位置。 它应位于适当的地理位置，用于管理此培训租户。 你仍可以选择数据保留长度，但这不是必需的。

1. 在“设置”中，选择“终结点”。

1. 在“设备管理”部分选择“加入”。

    >注意：还可以从左侧菜单栏的“资产”部分执行设备载入。 展开“资产”，然后选择“设备”。 在“设备清单”页上，选中“计算机和移动设备”，向下滚动到“载入设备”。 此操作会将你转到“设置”>“终结点”页。

1. 在“1. 加入设备”区域中，确保“部署方法”下拉列表中包含“本地脚本(用于最多 10 台设备)”，然后选择“下载加入包”按钮。

1. 将下载的 zip 文件解压缩到本地文件夹（如 Documents 文件夹）。

1. 右键单击解压缩的文件 WindowsDefenderATPLocalOnboardingScript.cmd，然后选择“以管理员身份运行”。  如果出现 Windows SmartScreen，请选择“仍然运行”。

备注：默认情况下，该文件应位于 c:\users\admin\downloads 目录中。
    
1. 对于脚本呈现的问题回答 Y。 完成后，命令屏幕中应该会出现一条消息，显示类似“已成功加入计算机…”的内容 

1. 从门户的“加入”页面中，复制检测测试脚本，并在一个打开的命令窗口中运行该脚本。  你可能需要通过在 Windows 搜索栏中键入**CMD，然后选择“以管理员身份运行”来打开新的“管理员: 命令提示符”** 窗口。

1. 在 Microsoft 365 Defender 门户菜单中，选择“设备库存”。 该列表中现在应列出了你的设备。

备注：可能需要多达 5 分钟，设备才会显示在门户中。


### 配置角色

在此任务中，你将配置用于设备组的角色。

1. 在 Microsoft 365 Defender 门户的左侧菜单栏中，选择“设置”。 

1. 选择“终结点”，然后选择权限区域中的“角色”。

1. 选择“启用角色”按钮。

1. 选择“添加项”。

1. 在“添加角色”对话框中输入以下内容：

    |常规设置|值|
    |---|---|
    |角色名称|**第 1 层支持**|
    |权限|实时响应功能 - 高级|

1. 选择“**下一步**”。

1. 在“分配的用户组”选项卡中，选择“sg-IT”，然后选择“添加所选组”。

1. 选择“保存”  。

### 配置设备组

在此任务中，你将配置允许访问控制和自动化配置的设备组。

1. 从左侧菜单栏中选择“设置”。 

1. 选择“终结点”，然后在权限区域中选择“设备组”。

1. 选择“添加设备组”。

1. 在“常规”选项卡中输入以下信息：

    |常规设置|值|
    |---|---|
    |设备组名称|**常规**|
    |自动化级别|全面 - 自动修正威胁|

1. 选择“下一步”  。

1. 。 在“设备”选项卡中，对操作系统条件选择“Windows 10”，然后选择“下一步” 。

1. 在“预览设备”选项卡上，选择“显示预览”以查看 WIN1 虚拟机。 选择“下一步”  。 
提示：如果没有在预览列表中看到虚拟机，请返回并同时为操作系统条件选择“无”。 尚未填充 VM 的数据。

1. 在“用户访问权限”选项卡中，依次选择“sg-IT”和“添加所选组”

1. 选择“完成”。

1. 设备组配置已更改。 选择“应用更改”，检查匹配项并重新计算分组。

1. 现在，你将有两个设备组；刚创建的“常规”设备组和具有相同修正级别的“未分组的设备（默认）”设备组。

<!--- 
## Deploy sample alerts for Demo in Module 3

In this task, you will load sample security alerts and review the alert details.

1. In the Edge browser, open the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Defender*, then select **Microsoft Defender for Cloud**.

1. In the **Getting Started** menu the default selection is **Upgrade**, select or **Skip** for now.

1. Select **Security alerts** in the portal menu.

1. Select **Sample Alerts** from the command bar.

1. In the Create sample alerts (Preview) pane make sure your subscription is selected.  Make sure all sample alerts are selected and select **Create sample alerts**.  

**Note** This may take a few minutes to complete. --->

## 为模块 4 中的演示部署 Microsoft Sentinel 工作区

在此任务中，你将创建 Microsoft Sentinel 工作区。

 >注：在以下演示中，需要有效的 Azure Pass 或其他 Azure 订阅。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择“+ 新建”。

1. 接下来，选择“新建工作区”。

备注：首先，创建新的 Log Analytics 工作区。

1. 选择合适的订阅。

1. 选择资源组的“新建”链接，然后输入所选的新资源组名称。

1. 在“实例”详细信息下的“名称”字段中，为所选的 Log Analytics 工作区输入名称。

注意：此名称应是唯一的，也是 Microsoft Sentinel 工作区名称。

1. 选择适合你的区域。  适当的区域可采用默认区域，或者讲师可能会对选择哪个区域提供具体建议。  

1. 选择“查看 + 创建”  。

1. 选择“创建”。 等待“将 Microsoft Sentinel 添加到工作区”页面上的列表中显示新的 Log Analytics 工作区。  这可能需要一点时间。

1. 在新建的工作区出现时将其选中，然后选择“添加”。

## 部署适用于 Microsoft Sentinel 的内容中心解决方案和数据连接器

### 任务 1：访问 Microsoft Sentinel 工作区

在此任务中，你将访问 Microsoft Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 打开浏览器，搜索、下载并安装新的 Microsoft Edge 浏览器。 启动新的 Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择你在上一个实验室中创建的 Microsoft Sentinel 工作区。

### 任务 2：连接 Azure 活动数据连接器。

在此任务中，你将连接“Azure 活动”数据连接器。

1. 在 Microsoft Sentinel 左侧菜单中，向下滚动到“内容管理”部分，然后选择“内容中心”。

1. 在“内容中心”，搜索“Azure 活动”解决方案并从列表中选择它。

1. 在“Microsoft Defender for Cloud”解决方案页面上，选择“安装”******。

1. 安装完成后，选择“管理”

    >注意：“Azure 活动”解决方案会安装“Azure 活动”数据连接器、12 个分析规则、14 个搜寻查询和 1 个工作簿。

1. 选择“Azure 活动”数据连接器，然后选择“打开连接器页面”。

1. 在“说明”选项卡下的“配置”区域中，向下滚动到“2. 连接订阅...”，并选择“启动 Azure Policy 分配向导>”。

1. 在“基本信息”选项卡中，选择“范围”下的省略号按钮 (...)，然后从下拉列表中选择你的“Azure Pass - 赞助”订阅，然后单击“选择”  。

1. 选择“参数”选项卡，从“主要 Log Analytics 工作区”下拉列表中选择你的工作区********。 此操作将应用订阅配置，以将信息发送到 Log Analytics 工作区。

1. 选择“修正”选项卡，然后选择“创建修正任务”复选框 。 此操作会将策略分配应用于现有的 Azure 资源。

1. 选择“查看 + 创建”按钮，检查配置。

1. 选择“创建”以完成操作。

### 任务 3：在 Azure 中创建 Windows 虚拟机

在本任务中，你将在 Azure 中创建 Windows 虚拟机。

1. 使用密码 Pa55w.rd 以管理员身份登录到 WIN1 虚拟机 。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 选择“+ 创建资源”。 提示：如果已在 Azure 门户中，则可能需要从顶部栏中选择 Microsoft Azure 以返回主页。

1. 在“搜索服务和市场”框中，输入“Windows 10”并从下拉列表中选择“Microsoft Window 10”。

1. 选中 Microsoft Window 10 对应的框。

1. 打开“计划”下拉列表，然后选择“Windows 10 企业版，版本 22H2”。

1. 选择“开始使用预设置配置”以继续。

1. 选择“开发/测试”，然后选择“继续创建 VM” 。

1. 为“资源组”选择“新建”，输入 `RG-AZWIN01` 作为名称，然后选择“确定”。

    >**注意：** 该资源组将是用于跟踪的新资源组。 

1. 在“虚拟机名称”中输入 `AZWIN01`。

1. 将“区域”的默认值保留为“(US) 美国东部”。

1. 向下滚动，查看虚拟机的“映像”。 如果显示为空，请选择“Windows 10 企业版，版本 22H2”。

1. 查看虚拟机的“大小”。 如果它显示为空，请选择“查看所有大小”，在“Azure 用户最常用的大小”下选择第一个 VM 大小，然后选择“选择”。

    >注意：如果看到消息“Azure Automanage 不支持此映像。若要禁用此功能，请导航到“管理”选项卡。否则，请选择受支持的映像******。” 转到“管理”选项卡并禁用“Automanage”。 之后创建过程便会成功。

1. 向下滚动，输入你选择的用户名。 提示：避免使用保留字，如 admin 或 root。

1. 输入你选择的密码。 提示：重新使用你的租户密码可能更简单。 可以在“资源”选项卡中找到它。

1. 向下滚动到页面底部，选中“许可”下面的复选框，以确认你具有符合条件的许可证。

1. 选择“查看 + 创建”，然后等待验证通过。

    >注意：如果网络验证失败，请选择该选项卡，查看其内容，然后再次选择“查看 + 创建”。

1. 选择“创建”。 等待创建资源，这可能需要几分钟的时间。

### 任务 4：连接 Azure Windows 虚拟机

在此任务中，需要将 Azure Windows 虚拟机连接到 Microsoft Sentinel。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择之前创建的 Microsoft Sentinel 工作区。

1. 1. 在 Microsoft Sentinel 左侧菜单中，向下滚动到“内容管理”部分，然后选择“内容中心”。

1. 在“内容中心”，搜索“Windows 安全事件”解决方案，并从列表中选择它。

1. 在“Windows 安全事件”解决方案页上，选择“安装”。

1. 安装完成后，选择“管理”

    >注意：“Windows 安全事件”解决方案安装“通过 AMA 收集的 Windows 安全事件”和“通过旧版代理程序的安全事件”数据连接器。 外加 2 个工作簿、20 个分析规则和 43 个搜寻查询。

1. 选择“通过 AMA 收集的 Windows 安全事件”数据连接器，然后在连接器信息窗格上选择“打开连接器页面”。

1. 在“说明”选项卡下的“配置”部分，选择“创建数据收集规则”。

1. 为“规则名称”输入“AZWINDCR”，然后选择“下一步: 资源”。

1. 选择“+ 添加资源”，以选择我们创建的虚拟机。

1. 展开“RG-AZWIN01”，然后选择“AZWIN01” 。

1. 选择“应用”，然后选择“下一步: 收集” 。

1. 查看不同的安全事件收集选项。 保留所有安全事件，然后选择“下一步: 查看 + 创建”。

1. 选择“创建”，保存数据收集规则。

1. 等待几分钟，然后选择“刷新”以查看列出的新数据收集规则。

### 任务 5：安装 Azure Arc 并连接本地服务器

在此任务中，你将在本地服务器上安装 Azure Arc，以便更轻松地加入。

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 查找虚拟机名称引用。

1. 使用以下密码以管理员身份登录到 WINServer 虚拟机：Passw0rd! （如果需要）。  

1. 打开 Microsoft Edge 浏览器并导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Arc”，然后选择“Azure Arc”。

1. 在“**基础结构**”下的导航窗格中，选择“**计算机**”

1. 选择“**+ 添加/创建**”，然后选择“**添加计算机**”。

1. 在“添加单个服务器”部分选择“生成脚本”。

1. 通读“先决条件”选项卡，然后选择“下一步”以继续。

1. 在“使用 Azure Arc 添加服务器”页面中，在“项目详细信息”下选择之前创建的资源组 。 提示：RG-Defender

    >**注意：** 如果尚未创建资源组，请打开另一个选项卡并创建资源组，然后重新开始。

1. 查看“服务器详细信息”和“连接方法”选项 。 保留默认值并选择“下一步”，以转到“标记”选项卡。

1. 查看默认可用的标记。 选择“下一步”，转到“下载并运行脚本”选项卡。

1. 向下滚动并选择“下载”按钮。 提示：如果浏览器阻止下载，请在浏览器中执行操作以允许下载。 在 Microsoft Edge 浏览器中，根据需要选择省略号按钮 (...)，然后选择“保留”。

1. 右键单击 Windows 的“开始”按钮，然后选择“Windows PowerShell (管理员)”。

1. 在“用户名”中输入“Administrator”，在“密码”中输入“Passw0rd!” （如果收到 UAC 提示）。

1. 输入：cd C:\Users\Administrator\Downloads

    >重要提示：如果没有此目录，最有可能意味着你使用的是错误的计算机。 返回任务 4 的开头，更改为 WINServer 并重新启动。

1. 键入“Set-ExecutionPolicy -ExecutionPolicy Unrestricted”，然后按 Enter。

1. 输入“A”，表示全部接受，然后按 Enter。

1. 键入“.\OnboardingScript.ps1”，然后按 Enter。  

    >**重要提示：** 如果收到错误“无法识别术语 .\OnboardingScript.ps1...”，请确保是在 WINServer 虚拟机中执行任务 4 的步骤。 其他问题可能是由于多次下载导致文件名称更改，请在运行目录中搜索“.\OnboardingScript (1).ps1”或其他文件编号。

1. 输入 R 以运行一次，然后按 Enter（这可能需要几分钟时间）。

1. 安装过程将打开新的 Edge 浏览器标签页，以对 Azure Arc 代理进行身份验证。 选择管理员帐户，等待消息“身份验证完成”，然后返回到 Windows PowerShell 窗口。

1. 安装完成后，返回到下载脚本的 Azure 门户页面，然后选择“关闭”。 关闭“**使用 Azure Arc 添加服务器**”，以返回到 Azure Arc“**计算机**”页面。

1. 选择“刷新”，直到显示 WINServer 服务器名称，且状态为“已连接”。

    >注意：这可能需要几分钟。


### 任务 6：保护本地服务器

在此任务中，需要将连接到 Azure Arc 的非 Azure Windows 虚拟机添加到 Microsoft Sentinel。  

   >注意：“通过 AMA 的 Windows 安全中心事件”需要针对非 Azure 设备的 Azure Arc。

1. 确保你位于 Microsoft Sentinel 工作区中的“通过 AMA 数据连接器收集的 Windows 安全事件”配置中。

1. 在“说明”选项卡中的“配置”部分下，通过选择铅笔图标编辑“AZWINDCR”数据收集规则。

1. 选择“下一步: 资源”和“+ 添加资源”。

1. 展开你创建的资源组，然后选择“WINServer”****。

    >重要说明：如果未看到 WINServer，请参阅在此服务器中安装 Azure Arc 的学习路径 3 练习 1 任务 4。

1. 选择“应用”。

1. 依次选择“下一步: 收集”、“下一步: 查看 + 创建” 。

1. 显示“验证通过”后，选择“创建”。


<!--- ### Task 4: Connect the Microsoft Defender for Cloud connector.

In this task, you will connect the Microsoft Defender for Cloud connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Cloud** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 5: Connect the Microsoft Defender for Cloud Apps connector.

In this task, you will connect theMicrosoft Defender for Cloud Apps connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Cloud Apps** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the **Instructions** tab in the **Configuration** section, select **Alerts** and then select **Apply Changes**.

### Task 6: Connect the Microsoft Defender for Office 365 connector.

In this task, you will connect the Microsoft Defender for Office 365 connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Office 365** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select **Connect**.

### Task 7: Connect the Microsoft Defender for Identity connector.

In this task, you will connect the Microsoft Defender for Identity connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Identity** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 8: Connect the Microsoft Defender for Endpoint connector.

In this task, you will connect the Microsoft Defender for Endpoint connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Endpoint** connector from the list.

1. Select Open connector page on the connector information blade.

1. Select **Connect**.

### Task 9: Connect the Microsoft 365 Defender connector.

In this task, you will connect the Microsoft 365 Defender connector.

1. From the Data Connectors Tab, select the **Microsoft 365 Defender** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select all the checkboxes for Microsoft Defender for Endpoint.

1. Select **Apply Changes**. 

### Task 3: Connect a non-Azure Windows Machine.

In this task, you will connect a non-Azure Windows virtual machine to Microsoft Sentinel.

1. Login to WIN2 virtual machine as Admin with the password: **Pa55w.rd**.  

1. Open the browser, search for, download, and install the new Microsoft Edge browser. Start the new Edge browser.

1. Open a browser and log into the Azure Portal at https://portal.azure.com with your credentials.

1. In the Search bar of the Azure Portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace.

1. From the Data Connectors tab, select the **Security Events via Legacy Agent** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the Select which events to stream area, select **All Events**, then select **Apply Changes**.

1. Select the **Install agent on a non-Azure Windows  Machine**.

**Note:** The instructions for Install agent on a Windows Virtual Machine and Install agent on a non-Azure Windows Machine may be reversed. The links take you to the proper location even with the reversed text.

1. Select **Download & install agent for non-Azure Windows machines**. 

1. Select the link for **Download Windows Agent (64 bit)**.

1. Run the .exe file that is downloaded and confirm and User Account Control prompt that may appear.

1. Select **Next** on the Welcome dialog.

1. Select **I Agree** on the Microsoft Software License Terms page.  On the Destination prompt select **Next**.

1. On the Agent Setup Options prompt, select **Connect the agent to Azure Log Analytics (OMS)** option, then select **Next**.

1. In the browser, copy the **Workspace ID** from the Agents Management page and paste into the Workspace ID in the dialog. 

1. In the browser, copy the **Primary key** from the Agents Management page and paste into the Primary key in the dialog. 

1. Select **Next**.

1. Select **Next** on the Microsoft Update page.

2. Then select **Install**.

### Task 4: Install and collect Sysmon logs.

In this task, you will install and collect Sysmon logs.

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. In the browser, go to https://docs.microsoft.com/sysinternals/downloads/sysmon

1. Download Sysmon from the page by select **Download Sysmon**.

1. Open the downloaded file and extract the files to a new directory c:\sysmon

1. In the Windows Taskbar for WIN2 search box, enter *command*.  The search results will show command prompt app.  Right-click on the command prompt app and select **Run as Administrator**.  Confirm any User Account Control prompts that appear.

1. Enter *cd \sysmon*

1. type *notepad sysmon.xml* to create a new file.

1. Open a tab in the browser and navigate to: https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

1. Copy the contents of that file from Github to the sysmon.xml notepad file you just created and save the file.

1. In the command prompt type the following and press enter:
    sysmon.exe -accepteula -i sysmon.xml

1. In the browser, navigate to the Azure portal at https://portal.azure.com 

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. In Microsoft Sentinel, select **Settings** from the Configuration area and then select **Workspace settings** tab.

1. Make sure your Microsoft Sentinel Workspace is selected.

1. Select **Agents configuration** in Settings.

1. Select the **Windows Event logs** tab.

1. Select **Add windows event log** button.

1. Enter **Microsoft-Windows-Sysmon/Operational** in the Log name field.

1. Select **Apply**. --->

## 进行攻击

### 任务 1：攻击配置了 Defender for Endpoint 的 Windows

在此任务中，你将在配置了 Microsoft Defender for Endpoint 的主机执行攻击。

1. 使用密码“Pa55w.rd”以管理员身份登录到 `WIN1` 虚拟机。  

1. 在任务栏的搜索框中，输入“Command”。  命令提示符将显示在搜索结果中。  右键单击命令提示符，并选择“以管理员身份运行”。 确认显示的任何用户帐户控制提示。

1. 在命令提示符中，在每一行中输入命令，并在每一行后按 Enter 键：
```
cd \
mkdir temp
cd temp
```

1. 复制并运行此命令：

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

### 任务 2：创建 C2（命令和控制）攻击

1. 使用密码“Pa55w.rd”以管理员身份登录到 `WIN1` 虚拟机。  

1. 在任务栏的搜索框中，输入“Command”。  命令提示符将显示在搜索结果中。  右键单击命令提示符，并选择“以管理员身份运行”。 确认显示的任何用户帐户控制提示。
1. 
1. 
1. 攻击 2 - 复制并运行此命令：

```
notepad c2.ps1
```
选择“是”以创建新文件并将以下 PowerShell 脚本复制到 c2.ps1，然后选择“保存”。

**备注** 粘贴到虚拟机可能有长度限制。  将此脚本分为三部分进行粘贴，以便将所有脚本粘贴到虚拟机中。  确保脚本在记事本 c2.ps1 文件中的外观与在这些说明中一致。

```


param(
    [string]$Domain = "microsoft.com",
    [string]$Subdomain = "subdomain",
    [string]$Sub2domain = "sub2domain",
    [string]$Sub3domain = "sub3domain",
    [string]$QueryType = "TXT",
        [int]$C2Interval = 8,
        [int]$C2Jitter = 20,
        [int]$RunTime = 240
)


$RunStart = Get-Date
$RunEnd = $RunStart.addminutes($RunTime)

$x2 = 1
$x3 = 1 
Do {
    $TimeNow = Get-Date
    Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout

    if ($x2 -eq 3 )
    {
        Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
        
        $x2 = 1

    }
    else
    {
        $x2 = $x2 + 1
    }
    
    if ($x3 -eq 7 )
    {

        Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout

        $x3 = 1
        
    }
    else
    {
        $x3 = $x3 + 1
    }


    $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
    Start-Sleep -Seconds $Jitter
}
Until ($TimeNow -ge $RunEnd)

```

在命令提示符中输入以下内容，在每一行中输入命令，并在每一行后按 Enter 键：
```
powershell
.\c2.ps1
```
**注意：** 你将看到解析错误。 这是预期会出现的。
让此命令/powershell 脚本在后台运行。 不要关闭窗口。  该命令需要在数小时内生成日志条目。  在此脚本运行期间，你可以继续进行下一项任务和下一个练习。  此任务创建的数据稍后将在威胁搜寻中使用。  此过程不会创造大量的数据或处理。

### 任务 2：攻击配置了 Azure Monitor 代理 (AMA) 的 Windows

在此任务中，你将在配置了安全事件连接器和 Sysmon 的主机上执行攻击。

1. 选择之前创建的 `AZWIN01` 虚拟网络。  

1. 在左侧菜单中，向下滚动到“操作”，选择“运行命令”

1. 在“运行命令”窗格中，选择“RunPowerShellScript”

1. 将以下用于模拟管理员帐户创建的命令复制到 `PowerShell Script` 窗体中，然后选择“运行”

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

>注：请确保每行只有一个命令，并且可以通过更改用户名重新运行命令。

1. 在 `Output` 窗口中，应会看到 `The command completed successfully` 三次
