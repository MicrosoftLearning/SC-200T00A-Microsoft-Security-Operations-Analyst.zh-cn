---
lab:
  title: 练习 11 - 在 Microsoft Sentinel 中使用存储库
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
ms.openlocfilehash: 9c585236134c162def5c5f24ba06a762b10a2314
ms.sourcegitcommit: f8918eddeaa7a7a480e92d0e5f2f71143c729d60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2022
ms.locfileid: "147038023"
---
# <a name="module-7---lab-1---exercise-11---use-repositories-in-microsoft-sentinel"></a>模块 7 - 实验室 1 - 练习 11 - 在 Microsoft Sentinel 中使用存储库

## <a name="lab-scenario"></a>实验室方案

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你已创建“计划”规则和“Microsoft 安全分析”规则。  需要在 Azure DevOps 存储库中集中分析规则。  然后将 Sentinel 连接到 Azure DevOps 存储库并导入内容。 


### <a name="task-1-create-and-export-an-analytical-rule"></a>任务 1：创建并导出分析规则

在此任务中，将在 Microsoft Sentinel 中启用实体行为分析。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 从“配置”区域选择“分析”。

1. 选择“+ 创建”按钮，然后选择“计划查询规则” 。

1. 在“分析规则”向导中的“常规”选项卡上，键入名称“来自 Azure DevOps 的规则”。

1. 对于“策略”，请选择“持久性”。

1. 对于“严重性”，选择“低”。

1. 选择“下一页:设置规则逻辑 >”按钮：

1. 对于规则查询，粘贴以下 KQL 语句：

    >**警告：** 使用粘贴功能时，可以向虚拟机添加额外（管道）字符。 请确保先使用记事本粘贴以下查询。

    ```KQL
    SecurityEvent | where EventID == 4732
    ```

1. 选择“查看查询结果”。 不应收到任何结果或任何错误。 如果收到错误，请查看查询是否与上一个 KQL 语句一样。 通过选择右上方的 X 关闭“日志”窗口，然后选择“确定”以放弃保存更改，并返回到向导 。


1. 向下滚动并在“查询计划”下设置以下项：

    |设置|值|
    |---|---|
    |运行查询的时间间隔|5 分钟|
    |查看最近多久的数据|1 天|

    >**注意：** 我们特意针对同一数据生成了多个事件。 这样，实验室就可使用这些警报。

1. 在“警报阈值”区域下，保留值不变，因为我们希望警报注册每个事件。

1. 在“事件分组”区域下，将“将所有事件分组到一个警报中”保留为所选选项，因为我们希望在每次运行时生成单个警报，只要查询返回的结果多于上述指定的警报阈值。

1. 选择底部的“下一步: 事件设置 >”按钮。 

1. 选择底部的“下一步: 自动响应 >”按钮。

1. 选择底部的“下一步: 查看 >”按钮。
 
1. 选择“创建”。

1. 选择刚刚创建的规则，然后从工具栏中选择“导出”。

1. 选择刚刚创建的规则，然后选择“删除”

### <a name="task-2-create-our-azure-devops-environment"></a>任务 2：创建 Azure DevOps 环境

在此任务中，你将测试创建并填充 Azure DevOps 存储库。

1. 在浏览器中打开另一个选项卡
1. 导航到 https://devops.azure.com
1. 选择“登录到 Azure DevOps”链接
1. 在“我们需要更多详细信息”页上，选择“继续” 。
1. 在“Azure DevOps 入门”页上，选择“继续”。
1. 在“几乎完成”页面上，输入 DevOps 组织的名称。  使用将来不想使用的名称。  

1. 输入看到的字符，然后继续。
1. 在“创建项目以开始”页上，输入“我的 Sentinel 内容”。 选择“创建项目”。
1. 导航到“存储库”。
1. 在该区域的页面底部“使用 README 或 gitignore 初始化主分支”，选择“初始化”。
1. 页面应显示存储库的文件。  唯一的文件是 README.me
1. 在“文件”（页面右侧）边栏选项卡上，工具栏包括“设置生成”、“克隆”和“:”选项。  选择“:”显示更多选项。
1. 选择“上传文件”
1. 选择“浏览”，然后从“下载”目录中选择“Azure_Sentinel_analytic_rule.json”文件。 
1. 选择“提交”。
1. 
1. 选择页面左上角的“Azure DevOps”。  这将显示你的组织和项目。
1. 选择左下角的“组织设置”。
1. 在“安全”区域中选择“策略”。
1. 在“应用程序连接策略”区域中，启用“通过 OAuth 的第三方应用程序访问”。 


### <a name="task-3-connect-sentinel-to-azure-devops"></a>任务 3：将 Sentinel 连接到 Azure DevOps。

1. 在浏览器中选择“Azure 门户”/“Microsoft Sentinel”选项卡。
1. 在 Microsoft Sentinel 中，选择“内容管理”部分中的“存储库”。
1. 在工具栏中选择“新增”。
1. 对于名称，请输入“我的内容”。
1. 对于源代码管理，选择“Azure DevOps”。
1. 选择“授权”。  然后选择“接受”。
1. 选择之前创建的组织。
1. 选择之前创建的项目。
1. 选择之前创建的存储库。
1. 选择主分支。
1. 选择所有内容类型。
1. 然后选择“创建”。


1. 在“存储库”页，选择“刷新”。  等到“上次部署状态”变为“失败”。  

>**重要提示：** “失败”状态是由托管实验室环境中的限制造成的。 通常会看到“成功”。 然后，可以在“分析”中看到导入规则“来自 Azure DevOps 的规则”。


## <a name="you-have-completed-the-lab"></a>你已完成本实验室。
