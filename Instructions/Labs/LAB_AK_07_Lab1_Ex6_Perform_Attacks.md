---
lab:
  title: 练习 6 - 进行攻击
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="learning-path-7---lab-1---exercise-6---conduct-attacks"></a>学习路径 7 - 实验室 1 - 练习 6 - 进行攻击

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex5.png)

你将模拟稍后将用于在 Microsoft Sentinel 中检测和调查的攻击。


### <a name="task-1-attack-windows-configured-with-defender-for-endpoint"></a>任务 1：攻击配置了 Defender for Endpoint 的 Windows

在此任务中，你将在配置了 Microsoft Defender for Endpoint 的主机执行攻击。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在任务栏的搜索框中，输入“Command”。 命令提示符将显示在搜索结果中。 右键单击命令提示符，并选择“以管理员身份运行”。 在出现的“用户帐户控制”窗口中选择“是”以允许应用运行。

1. 在命令提示符的根目录中创建 Temp 文件夹。 请记住，在上一行后按 Enter 键：

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

#### <a name="attack-1---persistence-with-registry-key-add"></a>攻击 1 - 通过注册表项添加实现的持久性攻击

1. 复制并运行以下命令以模拟程序持久性：

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```

#### <a name="attack-3---dns--c2"></a>攻击 3 - DNS / C2 

1. 复制并运行以下命令以创建一个脚本，用于模拟对 C2 服务器的 DNS 查询：

    ```CommandPrompt
    notepad c2.ps1
    ```

1. 选择“是”以创建新文件并将以下 PowerShell 脚本复制到 c2.ps1。

    >**注意：** 粘贴到虚拟机中的长度可能有限。 确保脚本在 c2.ps1 文件中的外观与在这些说明中一致。

    ```PowerShell
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

1. 在“记事本”菜单中，选择“文件”，然后选择“保存” 。 

1. 返回命令提示符窗口，输入以下命令并按 Enter 键。 

    >**注意：** 系统将打开一个新的 PowerShell 窗口，你将看到解决错误。 这是正常情况。

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

>**重要提示：** 请勿关闭这些窗口。 让此 PowerShell 脚本在后台运行。 该命令需要在数小时内生成日志条目。 在此脚本运行期间，你可以继续进行下一项任务和下一个练习。 此任务创建的数据稍后将在威胁搜寻中使用。 此过程不会创造大量的数据或处理。


### <a name="task-2-attack-windows-configured-with-microsoft-sentinel-connector"></a>任务 2：攻击配置了 Microsoft Sentinel 连接器的 Windows

在此任务中，你将通过 Microsoft Sentinel 攻击配置了安全事件连接器的主机。

>**重要提示：** 接下来的步骤将在另一台计算机上完成，而不是你之前使用的计算机。 查找虚拟机名称引用。

1. 以管理员身份使用密码登录到 WIN2 虚拟机：**Pa55w.rd**。  

>**重要提示：** 实验室的 SAVE 功能会导致 Win2 与 Azure Arc 断开连接。重启可以解决这个问题。  

1. 在 Windows 中选择“开始”。 然后依次选择“电源”和“重启” 。

1. 按照说明再次登录到 WIN2。

1. 在任务栏的搜索框中，输入“Command”。 命令提示符将显示在搜索结果中。 右键单击命令提示符，并选择“以管理员身份运行”。 在出现的“用户帐户控制”窗口中选择“是”以允许应用运行。

1. 在命令提示符的根目录中创建 Temp 文件夹。 请记住，在上一行后按 Enter 键：

    ```CommandPrompt
    cd \
    mkdir temp
    cd \temp
    ```

#### <a name="attack-2---user-add-and-elevate-privilege"></a>攻击 2 - 用户添加和特权提升

1. 复制并运行此命令以模拟管理员帐户的创建。 请记住，在上一行后按 Enter 键：

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

## <a name="proceed-to-exercise-7"></a>转到练习 7
