---
lab:
  title: 练习 1 - 部署 Microsoft Defender for Endpoint
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
ms.openlocfilehash: 55d34a12be8028af19201a113d23ffbbd870a150
ms.sourcegitcommit: 175df7de88c9a609f8caf39840664bf992c5b6dc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2022
ms.locfileid: "138025420"
---
# <a name="module-2---lab-1---exercise-1---deploy-microsoft-defender-for-endpoint"></a>模块 2 - 实验室 1 - 练习 1 - 部署 Microsoft Defender for Endpoint

## <a name="lab-scenario"></a>实验室方案

你是一家公司的安全操作分析师，你的公司正在实施 Microsoft Defender for Endpoint。 你的主管计划加入一些设备，以深入了解安全运营 (SecOps) 团队响应程序所需的更改。

首先初始化 Defender for Endpoint 环境。 接下来，通过对初始设备运行加入脚本，为你的部署加入这些设备。 配置环境的安全性。 最后，创建设备组并分配适当的设备。

>**重要提示：** 通过不同的模块使用实验室虚拟机。 请保存你的虚拟机。 如果在不保存的情况下退出实验室，将需要再次重新运行某些配置。

>**注意：** 请确保已成功完成前一模块的最后 3 个步骤。


### <a name="task-1-initialize-microsoft-defender-for-endpoint"></a>任务 1：初始化 Microsoft Defender for Endpoint

在此任务中，你将执行 Microsoft Defender for Endpoint 门户的初始化。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 如果尚未处于 Microsoft 365 Defender 门户，请启动 Microsoft Edge 浏览器。

1. 在 Microsoft Edge 浏览器中，转到 Microsoft 365 Defender 门户 (https://security.microsoft.com) )。

1. 在“登录”对话框中，复制并粘贴实验室托管提供者为管理员用户名提供的租户电子邮件帐户，然后选择“下一步” 。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的管理员的租户密码，然后选择“登录” 。

1. 在 Microsoft 365 Defender 门户中，从左侧“导航”菜单中选择“设置” 。

1. 在“设置”页面上，选择“设备发现” 。 

    >**注意：** 如果“设置”下面没有显示“设备发现”选项，可通过选择右上角包含帐户首字母缩写的圆圈，然后选择“注销”进行注销  。可能想尝试的其他选项是使用 Ctrl+F5 刷新页面或打开页面 InPrivate。 使用“租户电子邮件”凭据重新登录。

1. 在“发现”设置中，确保选中“标准发现(推荐)”。 提示：如果看不到该选项，请刷新页面。


### <a name="task-2-onboard-a-device"></a>任务 2：加入设备。

在此任务中，你需要使用加入脚本将设备加入 Microsoft Defender for Endpoint。

1. 如果你在浏览器中尚未处于 Microsoft 365 Defender 门户上，请启动 Microsoft Edge 浏览器并转到 (https://security.microsoft.com) 并使用“租户电子邮件”凭据登录。

1. 从左侧菜单栏中选择“设置”，然后从“设置”页面中选择“终结点” 。

1. 在“设备管理”部分选择“加入”。

1. 在“1. 加入设备”区域中，确保“部署方法”下拉列表中包含“本地脚本(用于最多 10 台设备)”，然后选择“下载加入包”按钮。 用鼠标突出显示“WindowsDefenderATPOnboardingPackage.zip”文件，然后选择文件夹图标“在文件夹中显示”。 提示：默认情况下，该文件应位于 c:\users\admin\downloads 目录中。

1. 右键单击已下载的 zip 文件，然后选择“全部提取...”，确保选中“完成时显示提取的文件”，然后选择“提取”。

1. 右键单击解压缩的文件 WindowsDefenderATPLocalOnboardingScript.cmd，然后选择“属性”。 选择“属性”窗口右下角的“解除阻止”复选框，然后选择“确定” 。

1. 再次右键单击解压缩文件“WindowsDefenderATPLocalOnboardingScript.cmd”，然后选择“以管理员身份运行”。  提示：如果遇到 Windows SmartScreen 窗口，请选择“详细信息”，然后选择“仍要运行” 。 
    
1. 显示“用户帐户控制”窗口时，请选择“是”以允许脚本运行，并对脚本提供的问题回答“Y”，然后按 Enter 键  。 完成后，命令屏幕上会显示一条“已成功将计算机加入 Microsoft Defender for Endpoint”的消息。

1. 按任意键继续。 这将关闭命令提示符窗口。

1. 从 Microsoft 365 Defender 门户返回到“加入”页面，在“2. 运行检测测试”部分下，通过选择“复制”按钮复制检测测试脚本。  

1. 在 WIN1 虚拟机的 Windows 搜索栏中，键入“CMD”，然后在命令提示符应用的右窗格上，选择“以管理员身份运行” 。 

1. 显示“用户帐户控制”窗口时，选择“是”以允许应用运行。 

1. 粘贴脚本的方法是右键单击“管理员:**命令提示符”窗口，并按 Enter 键运行** 。 **注意：** 窗口在运行脚本后自动关闭。

1. 在 Microsoft 365 Defender 门户的左侧菜单中，在“终结点”区域下，选择“设备清单”。 该列表中现在应列出了你的设备。

    >**注意：** 可能需要多达 5 分钟，设备才会显示在门户中。 如果设备未显示，请完成下一任务，稍后再回来查看。


### <a name="task-3-configure-roles"></a>任务 3：配置角色

在此任务中，你将配置用于设备组的角色。

1. 在 Microsoft 365 Defender 门户中，从左侧菜单栏中选择“设置”，然后选择“终结点” 。 

1. 在“权限”区域下选择“角色”。

1. 选择“启用角色”按钮。

1. 选择“+ 添加项”。

1. 在“添加角色”对话框中，输入以下内容：

    |常规设置|值|
    |---|---|
    |角色名称|**第 1 层支持**|
    |权限|实时响应功能 - 高级|

1. 选择顶部的“分配的用户组”选项卡。 选择“sg-IT”，然后选择“添加所选组”。 请确保它显示在“Azure AD 具有此角色的用户组”下。

1. 选择“保存”。


### <a name="task-4-configure-device-groups"></a>任务 4：配置设备组

在此任务中，你将配置允许访问控制和自动化配置的设备组。

1. 在 Microsoft 365 Defender 门户中，从左侧菜单栏中选择“设置”，然后选择“终结点” 。 

1. 在“权限”区域中，选择“设备组”。

1. 选择“+ 添加设备组”图标。

1. 在“常规”选项卡中输入以下信息：

    |常规设置|值|
    |---|---|
    |设备组名称|**常规**|
    |自动化级别|全面 - 自动修正威胁|

1. 选择“下一步”  。

1. 在“设备”选项卡中，对操作系统条件选择“Windows 10”，然后选择“下一步” 。

1. 在“预览设备”选项卡上，选择“显示预览”以查看 WIN1 虚拟机。  选择“下一步”  。

1. 对于“用户访问”选项卡，选择“sg-IT”，然后选择“添加所选组”按钮 。 请确保它显示在“Azure AD 可访问此设备组的用户组”下。

1. 选择“完成”  。

1. 设备组配置已更改。 选择“应用更改”，检查匹配项并重新计算分组。

1. 现在，你将有两个设备组；刚创建的“常规”设备组和具有相同修正级别的“未分组的设备（默认）”设备组。

## <a name="proceed-to-exercise-2"></a>继续进行练习 2
