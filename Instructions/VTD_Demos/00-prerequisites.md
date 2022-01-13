
# Microsoft 安全操作分析师
培训师准备指南

## 目的 

本文档适用于准备在 Microsoft 安全虚拟培训日讲授“现代化安全和防御威胁”的演示者。本文档是“SC-200： Microsoft 安全操作分析师”认证课程的一部分。

## 演示先决条件

本课程的实验室需要 Microsoft 365 E5 许可的租户以及 Azure 订阅。
* 你可以为自己申请 Microsoft Learning Azure Pass
* 确保至少在进行演示前两周申请上述 Azure Pass。收到 Pass 后，需要激活它。 
* Azure Pass 的实际功能与公开可用的 Microsoft Azure 试用版订阅相同。这意味着 Pass 的功能有限。
* 实验室说明在 [SC-200 Microsoft Learning GitHub 存储库](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/)中。
* 确保将用于演示的计算机安装了新的 Microsoft Edge 浏览器。

## 激活 Azure Pass

## 部署 Defender for Endpoint

### 获取 Microsoft 365 凭据

启动实验室后，Microsoft 虚拟实验室环境中将提供一个免费试用租户可供你访问。系统会自动向该租户分配一个唯一用户名和密码。你需要检索此用户名和密码，以便在 Microsoft 虚拟实验室环境中登录 Azure 和 Microsoft 365。 

由于此课程可能由学习合作伙伴使用几个授权实验室托管提供者中的任何一个提供，因此，检索与租户关联的租户 ID 的相关实际步骤可能会因实验室托管提供者而有所不同。因此，讲师将在课程中为你提供有关如何检索此信息的必要说明。你应该记录以供稍后使用的信息包括：

	- **租户后缀 ID。** 此 ID 适用于将在整个实验室中用于登录 Microsoft 365 的 onmicrosoft.com 帐户。其格式为 **{username}@M365xZZZZZZ.onmicrosoft.com**，其中 ZZZZZZ 是实验室托管提供者提供的唯一租户后缀 ID。记录此 ZZZZZZ 值以供稍后使用。当有任何实验室步骤指示你登录 Microsoft 365 门户时，都必须输入在此处获取的 ZZZZZZ 值。
	- **租户密码。** 这是由实验室托管提供者提供的管理员帐户的密码。
	

### 初始化 Microsoft Defender for Endpoint。

在此任务中，你将执行 Microsoft Defender for Endpoint 门户的初始化。


1.  使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2.  打开 Microsoft Edge 浏览器，搜索“Edge 浏览器更新”，然后下载并安装新版 Microsoft Edge 浏览器。必须执行此操作，以确保在托管虚拟机中运行最新版本的 Microsoft Edge。启动新的 Edge 浏览器。

3.  在 Edge 浏览器中，转到 Microsoft Defender 安全中心 (https://securitycenter.microsoft.com)。

4. 在 **“登录”** 对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择 **“下一步”**。

5. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择 **“登录”**。

**备注**：如果你收到消息“你无法访问此会话。”，请等待 5 分钟，然后重试。  有时，访问规则需要传播租户。  

6. 在 **“Microsoft 安全中心”** 设置的步骤 2 中，选择 **“下一步”**。

7. 在步骤 3 **“设置首选项”** 中，选择适用于此培训租户的管理位置的数据存储位置。  你可能需要向课程讲师进行确认。

8. 确认已启用预览**功能**。

9. 选择 **“下一步”**。  

10. 在 **“创建云实例”** 中选择“继续”

11. 在 **“创建 Microsoft Defender for Endpoint 帐户”** 进度栏显示创建过程完成后，步骤 4 的选项随即显示。  选择 **“开始使用 Microsoft Defender for Endpoint”**。

12. 在“设置未完成”对话框中选择 **“仍然继续”**。

**备注**： 已**完成**设置。  在下一个任务中，你将加入设备。  

### 加入设备。

在此任务中，你需要将设备加入 Microsoft Defender for Endpoint。

1. 转到 Microsoft Defender 安全中心 (https://securitycenter.microsoft.com)，并使用 **租户电子** 邮件凭据登录（如果当前不在该门户中）。

2. 从左侧菜单栏中选择 **“设置”**。

3. 在“设备管理”部分选择 **“加入”**。

4. 在“加入设备”区域中选择 **“下载包”** 按钮。

5. 将下载的 zip 文件解压缩到本地文件夹（如 Documents 文件夹）。

6. 右键单击解压缩的文件 WindowsDefenderATPLocalOnboardingScript.cmd，然后选择 **“以管理员身份运行”**。  如果出现 Windows SmartScreen，请选择“仍然运行”。

**备注**：默认情况下，该文件应位于 c:\users\admin\downloads 目录中。
    
7. 对于脚本呈现的问题回答 **Y**。完成后，命令屏幕中应该会出现一条消息，显示类似“已成功加入计算机…”的内容 

8. 从门户的“加入”页面中，复制检测测试脚本，并在一个打开的命令窗口中运行该脚本。  你可能需要通过在 Windows 搜索栏中键入 *CMD*，然后选择 **“以管理员身份运行”** 来打开新的 **“管理员: 命令提示符”** 窗口。

9. 在 Microsoft Defender 安全中心门户的菜单中，选择 **“设备清单”**。该列表中现在应列出了你的设备。

**备注**：可能需要多达 5 分钟，设备才会显示在门户中。


### 配置角色

在此任务中，你将配置用于设备组的角色。

1. 在 Microsoft Defender 安全中心门户中，从左侧菜单栏中选择 **“设置”**。 

2. 在“权限”区域中选择 **“角色”**。

3. 选择 **“启用角色”** 按钮。

4. 选择 **“添加项”**。

5. 在“添加角色”对话框中输入以下内容：
    角色名称：层级
    实时响应功能：选中复选框
    高级：选择。

6. 选择 **“下一步”**。

7. 在“分配的用户组”选项卡中，选择 **“sg-IT”**，然后选择 **“添加所选组”**。

8. 选择 **“保存”**。


### 配置设备组

在此任务中，你将配置允许访问控制和自动化配置的设备组。

1. 从左侧菜单栏中选择 **“设置”**。 

2. 在“权限”区域中，选择 **“设备组”**。

3. 选择 **“添加设备组”**。

4. 在“常规”选项卡中输入以下信息：

- 设备组名称：常规
- 自动化级别：全面 - 自动修正威胁
- 成员：名称 = TESTLAB

5. 选择 **“下一步”**。

6. 在“用户访问权限”选项卡中，依次选择 **“sg-IT”** 和 **“添加所选组”**

7. 选择 **“完成”**。

8. 设备组配置已更改。应用更改，以检查匹配项并重新计算分组。


## 为模块 2 中的演示部署示例警报

在此任务中，你将加载示例安全警报并查看警报详细信息。

2. 在 Edge 浏览器中，通过 https://portal.azure.com 打开 Azure 门户。

3. 在 **“登录”** 对话框中，复制粘贴实验室托管提供者提供的**租户电子**邮件帐户，然后选择 **“下一步”**。

4. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者提供的**租户密码**，然后选择 **“登录”**。

5. 在 Azure 门户的搜索栏中，键入 *“安全”*，然后选择 **“安全中心”**。

1. 如果提示升级安全中心，请单击底部的 **“跳过”**。

6. 在门户菜单中选择 **“安全警报”**。

7. 从命令栏选择 **“示例警报”**。

8. 在“创建示例警报(预览)”窗格中，确保已选择你的订阅。  确保已选择所有示例警报，然后选择 **“创建示例警报”**。  

**备注**：此操作可能需要几分钟才能完成。

## 为模块 4 中的演示部署 Azure Sentinel 工作区

在此任务中，你将创建 Azure Sentinel 工作区。

3.  在 Edge 浏览器中，通过 https://portal.azure.com 导航到 Azure 门户。

4. 在 **“登录”** 对话框中，复制粘贴实验室托管提供者提供的**租户电子**邮件帐户，然后选择 **“下一步”**。

5. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者提供的**租户密码**，然后选择 **“登录”**。

6. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择 **“Azure Sentinel”**。

7. 选择 **“+ 创建”**。

8. 接下来，选择 **“新建工作区”**。

**备注**：首先，创建新的 Log Analytics 工作区。

9. 选择合适的订阅。

10. 选择资源组的 **“新建”** 链接，然后输入所选的新资源组名称。

11. 在“实例”详细信息下的“名称”字段中，为所选的 Log Analytics 工作区输入名称。

**备注：** 此名称也将是 Azure Sentinel 工作区名称。

12. 选择适合你的区域。  适当的区域可采用默认区域，或者讲师可能会对选择哪个区域提供具体建议。  

13. 选择 **“查看 + 创建”**。

14. 选择 **“创建”**。等待新 Log Analytics 工作区出现在“将 Azure Sentinel 添加到工作区”页面上的列表中。  这可能需要一分钟时间。

16. 在新建的工作区出现时将其选中，然后选择 **“添加”**。

## 为 Azure Sentinel 创建数据连接器

### 任务 1：访问 Azure Sentinel 工作区。

在此任务中，你将访问 Azure Sentinel 工作区。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 打开浏览器，搜索、下载并安装新的 Microsoft Edge 浏览器。启动新的 Edge 浏览器。

3. 在 Edge 浏览器中，通过 https://portal.azure.com 导航到 Azure 门户。

4. 在 **“登录”** 对话框中，复制粘贴实验室托管提供者提供的**租户电子**邮件帐户，然后选择 **“下一步”**。

5. 在 **“输入密码”** 对话框中，复制粘贴实验室托管提供者提供的**租户密码**，然后选择 **“登录”**。

6. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择 **“Azure Sentinel”**。

7. 选择你在上一个实验室中创建的 Azure Sentinel 工作区。

### 任务 2：连接 Azure Active Directory 连接器。

在此任务中，你将连接 Azure Active Directory 连接器。

1. 在“配置”区域，选择 **“数据连接器”**。  在“数据连接器”页面中，从列表中选择 **“Azure Active Directory”** 连接器。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 从“配置”区域中选择 **“登录日志”** 和 **“审核日志”** 选项，然后选择 **“应用更改”**。

### 任务 3：连接 Azure Active Directory 标识保护连接器。

在此任务中，你将连接 Azure Active Directory 标识保护连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Azure Active Directory 标识保护”** 连接器。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 选择 **“连接”** 按钮。

### 任务 4：连接 Azure Defender 连接器。

在此任务中，你将连接 Azure Defender 连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Azure Defender”** 连接器。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 查看连接选项。请不要连接。这仅用于了解信息。

### 任务 5：连接 Microsoft Cloud App Security 连接器。

在此任务中，你将连接 Microsoft Cloud App Security 连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Microsoft Cloud App Security”** 连接器。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 选择 **“警报”**，然后选择 **“应用更改”**。

### 任务 6：连接 Microsoft Defender for Office 365 连接器。

在此任务中，你将连接 Microsoft Defender for Office 365 连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Microsoft Defender for Office 365”** 连接器。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 选择 **“连接”**。

### 任务 7：连接 Microsoft Defender for Identity 连接器。

在此任务中，你将连接 Microsoft Defender for Identity 连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Microsoft Defender for Identity”** 连接器。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 查看连接选项。请不要连接。这仅用于了解信息。

### 任务 8：连接 Microsoft Defender for Endpoint 连接器。

在此任务中，你将连接 Microsoft Defender for Endpoint 连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Microsoft Defender for Endpoint”** 连接器。

2. 在连接器信息边栏选项卡上选择“打开连接器页面”。

3. 选择 **“连接”**。

### 任务 9：连接 Microsoft 365 Defender 连接器。

在此任务中，你将连接 Microsoft 365 Defender 连接器。

1. 在“数据连接器”选项卡中，从列表中选择 **“Microsoft 365 Defender”**。

2. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

3. 选中 Microsoft Defender for Endpoint 的所有复选框。

4. 选择 **“应用更改”**。

### 任务 3：连接非 Azure Windows 计算机。

在此任务中，你要将非 Azure Windows 虚拟机连接到 Azure Sentinel。

1. 以管理员身份使用密码登录到 WIN2 虚拟机：**Pa55w.rd**。  

2. 打开浏览器，搜索、下载并安装新的 Microsoft Edge 浏览器。启动新的 Edge 浏览器。

3. 打开浏览器并使用你的凭据登录到 Azure 门户 (https://portal.azure.com)。

4. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择 **“Azure Sentinel”**。

5. 选择 Azure Sentinel 工作区。

6. 从“数据连接器”选项卡，从列表中选择 **“安全事件”** 连接器。

7. 在连接器信息边栏选项卡上选择 **“打开连接器页面”**。

8. 在“选择要流式传输的事件”区域，选择 **“所有事件”**，然后选择 **“应用更改”**。

9. 选择 **“在非 Azure Windows 虚拟机上安装代理”**。

**备注：** 在 Windows 虚拟机上安装代理和在非 Azure Windows 计算机上安装代理的说明可能相反。即使显示的文字相反，链接也可指向适当的位置。

10. 选择 **“为非 Azure Windows 虚拟机下载和安装代理”**。

11. 选择 **“下载 Windows 代理(64 位)”** 的链接。

12. 运行下载的 .exe 文件，并在出现“用户帐户控制”提示时确认。

13. 在“欢迎”对话上，选择 **“下一步”**。

14. 在 “Microsoft 软件许可条款”页面上选择 **“我同意”**。  在“目标”提示上选择 **“下一步”**。

15. 在“代理安装选项”提示上，选择 **“将代理连接到 Azure Log Analytics (OMS)”** 选项，然后选择 **“下一步”**。

16. 在浏览器中，从代理管理页面复制 **“工作区 ID”**，然后在对话中粘贴到“工作区 ID”。

17. 在浏览器中，从代理管理页面复制 **“主键”**，然后在对话中粘贴到“主键”。

18. 选择 **“下一步”**。

19. 在“Microsoft 更新”页上选择 **“下一步”**。

20. 然后选择 **“安装”**。

### 任务 4： 安装并收集 Sysmon 日志。

在此任务中，你将安装并收集 Sysmon 日志。

此时应仍连接到 WIN2 虚拟机。  以下说明将使用默认配置安装 Sysmon。  应研究基于社区的配置，以便在生产计算机上使用 Sysmon。

1. 在浏览器中，转到 https://docs.microsoft.com/sysinternals/downloads/sysmon

2. 从页面上选择 **“下载 Sysmon”** 以下载 Sysmon。

3. 打开下载文件并将文件提取到新目录 c:\sysmon

4. 在适用于 WIN2 的 Windows 任务栏搜索框中，输入 *“命令”*。  搜索结果将显示命令提示符应用。  右键单击命令提示符应用并选择 **“以管理员身份运行”**。  确认显示的任何用户帐户控制提示。

5. 输入 *cd \sysmon*

6. 加入 *notepad sysmon.xml* 以创建新文件。

7. 在浏览器中打开选项卡，并导航到 https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

8. 将该文件的内容从 Github 复制到你刚创建的 sysmon.xml 记事本文件，并保存文件。

9. 在命令提示符中键入以下命令，并按 Enter：
    sysmon.exe -accepteula -i sysmon.xml

10. 在浏览器中，导航到 Azure 门户 (https://portal.azure.com) 

11. 在 Azure 门户的搜索栏中，键入 *Sentinel*，然后选择 **“Azure Sentinel”**。

12. 在 Azure Sentinel 中，从“配置”区域选择 **“设置”**，然后选择 **“工作区设置”** 选项卡。

13. 确保选择你的 Azure Sentinel 工作区。

14. 在“设置”中选择 **“代理配置”**。

15. 选择 **“Windows 事件日志”** 选项卡。

16. 选择 **“添加 Windows 事件日志”** 按钮。

17. 在“日志名称”字段输入 **Microsoft-Windows-Sysmon/Operational**。

18. 选择“**应用**”。

## 进行攻击

### 任务 1：攻击配置了 Defender for Endpoint 的 Windows。

在此任务中，你将在配置了 Microsoft Defender for Endpoint 的主机执行攻击。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

2. 在任务栏的搜索框中，输入 *“Command”*。  命令提示符将显示在搜索结果中。  右键单击命令提示符，并选择 **“以管理员身份运行”**。确认显示的任何用户帐户控制提示。

3. 在命令提示符中，在每一行中输入命令，并在每一行后按 Enter 键：
```
cd \
mkdir temp
cd temp
```
4. 攻击 1 - 复制并运行此命令：

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 攻击 3 - 复制并运行此命令：

```
notepad c2.ps1
```
选择 **“是”** 以创建新文件并将以下 PowerShell 脚本复制到 c2.ps1，然后选择 **“保存”**。

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
**备注：** 你将看到解析错误。这在预料之中。
让此命令/powershell 脚本在后台运行。不要关闭窗口。  该命令需要在数小时内生成日志条目。  在此脚本运行期间，你可以继续进行下一项任务和下一个练习。  此任务创建的数据稍后将在威胁搜寻中使用。  此过程不会创造大量的数据或处理。

### 任务 2：攻击配置了 Sysmon 的 Windows

在此任务中，你将在配置了安全事件连接器和 Sysmon 的主机上执行攻击。

1. 以管理员身份使用密码登录到 WIN2 虚拟机：**Pa55w.rd**。  

2. 在任务栏的搜索框中，输入 *“CMD”*。  命令提示符将显示在搜索结果中。  右键单击命令提示符，并选择 **“以管理员身份运行”**。

3. 在命令提示符中，在每一行中输入命令，并在每一行后按 Enter 键：
```
cd \
mkdir temp
cd \temp
```

4. 攻击 1 - 复制并运行此命令：

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 攻击 2 - 复制并运行此命令，在每一行中输入命令，并在每一行后按 Enter 键：

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```