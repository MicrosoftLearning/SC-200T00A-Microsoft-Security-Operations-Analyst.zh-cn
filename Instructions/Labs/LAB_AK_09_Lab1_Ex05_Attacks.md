---
lab:
  title: 练习 5：准备执行模拟攻击
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 9 - 实验室 1 - 练习 5 - 准备执行模拟攻击

## 实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod9_L1_Ex5.png)

### 完成本实验室的估计时间：30 分钟

### 任务 1：连接到本地服务器

在此任务中，将把本地服务器连接到 Azure 订阅。 Azure Arc 已在此服务器上预安装。 服务器将在接下来的练习中用于运行模拟攻击，随后将在 Microsoft Sentinel 中检测和调查这些攻击。

>**备注**：学习路径 #9 的实验室练习是在*独立*环境中进行的。 如果在完成实验室前退出，则需要重新运行配置。

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

1. 在“*登录*”对话框中，输入实验室托管提供商提供的“**租户电子邮件**”和“**租户密码**”，然后选择“**登录**”。 等待“*身份验证完成*”消息，关闭浏览器选项卡并返回到“*命令提示符*”窗口。

1. 命令运行完成后，将“*命令提示符*”窗口保持打开状态，并键入以下命令以确认连接是否成功：

    ```cmd
    azcmagent show
    ```

1. 在命令输出中，验证“*代理状态*”是否为“**已连接**”。

## 任务 2：连接非 Azure Windows 计算机

在此任务中，将向 Microsoft Sentinel 添加一台已连接 Azure Arc 的本地计算机。  

>**备注：** 已在你的 Azure 订阅中使用名称 **defenderWorkspace** 预先部署了 Microsoft Sentinel，并且已安装所需的*内容中心*解决方案。

1. 使用密码 Pa55w.rd 以管理员身份登录到 WIN1 虚拟机 。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (<https://portal.azure.com> )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的“搜索”栏中，键入 Sentinel，然后选择 Microsoft Sentinel。

1. 选择 Microsoft Sentinel **defenderWorkspace**。

1. 在 Microsoft Sentinel 左侧导航菜单中，向下滚动到“*配置*”部分，然后选择“**数据连接器**”。

1. 在“*数据连接器*”中，搜索“**通过 AMA 的 Windows 安全事件**”解决方案，然后从列表中选择它。

1. 在“*通过 AMA 的 Windows 安全事件*”详细内容窗格中，选择“**打开连接器页面**”。

    >注意：“Windows 安全事件”解决方案安装“通过 AMA 收集的 Windows 安全事件”和“通过旧版代理程序的安全事件”数据连接器。 外加 2 个工作簿、20 个分析规则和 43 个搜寻查询。

1. 在“说明”选项卡下的“配置”部分，选择“创建数据收集规则”。

1. 为“规则名称”输入“AZWINDCR”，然后选择“下一步: 资源”。

1. 在“*资源*”选项卡上的“*范围*”下，展开“*订阅*”。

    >提示****：可选择“范围”列前面的“>”来展开整个范围层次结构。****

1. 展开 **defender-RG** 资源组，然后选择 **WINServer**。

1. 选择“**下一步: 收集**”，并保留选中的“*所有安全事件*”。

1. 在完成时选择“下一步:  查看 + 创建”。

1. 显示“验证通过”后，选择“创建”。

### 任务 3：了解攻击

>**重要说明：在此练习中你不会执行任何操作。**  这些指令只说明了在后续练习中将执行的攻击。 请仔细阅读本页。

攻击模式基于开源项目： <https://github.com/redcanaryco/atomic-red-team>

#### 攻击 1 - 通过注册表项添加实现的持久性攻击

攻击者会在运行注册表项中添加一个程序。 这通过使程序在用户每次登录时都能运行来实现持久性。

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

#### 攻击 2 - 用户添加和特权提升

攻击将添加新建用户并将新用户提升到管理员组。 这会让攻击者能够使用有特权的其他帐户登录。

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

#### 攻击 3 - DNS / C2

攻击者会向命令发送大量 DNS 查询，并控制 (C2) 服务器。 目的是对来自单个源系统或发往单个目标域的 DNS 查询的数目触发基于阈值的检测。

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

### 任务 4：了解检测建模

本实验室中使用的攻击检测配置循环代表所有数据源，虽然你仅专注于两个特定数据源。

要构建检测，从构建 KQL 语句开始。 你将开始攻击主机，因此将使用代表数据开始构建 KQL 语句。

有 KQL 语句后，即可创建分析规则。

触发规则并创建警报和事件后，调查以确定你是否提供了可帮助安全运营分析师进行调查的字段。

接下来，你将对分析规则进行其他更改。

>**注意：** 为了方便演示实验室，某些警报触发的时间期限较短。

## 继续完成练习 6
