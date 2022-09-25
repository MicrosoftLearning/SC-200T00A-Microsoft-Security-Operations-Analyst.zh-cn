---
lab:
  title: 练习 11 - 在 Microsoft Sentinel 中使用存储库
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-11---use-repositories-in-microsoft-sentinel"></a>模块 7 - 实验室 1 - 练习 11 - 在 Microsoft Sentinel 中使用存储库

## <a name="lab-scenario"></a>实验室方案

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules.  You need to centralize analytical rules in an Azure DevOps repository.  Then connect Sentinel to the Azure DevOps repository and import the content. 


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

    ><bpt id="p1">**</bpt>Warning:<ept id="p1">**</ept> When using the Paste function to the virtual machine extra (pipe) characters could be added. Make sure you use Notepad first to paste the following query.

    ```KQL
    SecurityEvent | where EventID == 4732
    ```

1. Select <bpt id="p1">**</bpt>View query results<ept id="p1">**</ept>. You should not receive any results nor any errors. If you receive an error, please review that the query appears just like the previous KQL statement. Close the <bpt id="p1">*</bpt>Logs<ept id="p1">*</ept> window by selecting the upper right <bpt id="p2">**</bpt>X<ept id="p2">**</ept> and select <bpt id="p3">**</bpt>OK<ept id="p3">**</ept> to discard to save changes to go back to the wizard.


1. 向下滚动并在“查询计划”下设置以下项：

    |设置|值|
    |---|---|
    |运行查询的时间间隔|5 分钟|
    |查看最近多久的数据|1 天|

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

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
1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。  

1. 输入看到的字符，然后继续。
1. 你已创建“计划”规则和“Microsoft 安全分析”规则。
1. 导航到“存储库”。
1. 在该区域的页面底部“使用 README 或 gitignore 初始化主分支”，选择“初始化”。
1. 需要在 Azure DevOps 存储库中集中分析规则。
1. 然后将 Sentinel 连接到 Azure DevOps 存储库并导入内容。
1. 选择“上传文件”
1. 选择“浏览”，然后从“下载”目录中选择“Azure_Sentinel_analytic_rule.json”文件。 
1. 选择“提交”。
1. 
1. Select <bpt id="p1">**</bpt>Azure DevOps<ept id="p1">**</ept> on the top left corner of the page.  This display your organization and projects.
1. 选择左下角的“组织设置”。
1. 在“安全”区域中选择“策略”。
1. 在“应用程序连接策略”区域中，启用“通过 OAuth 的第三方应用程序访问”。 


### <a name="task-3-connect-sentinel-to-azure-devops"></a>任务 3：将 Sentinel 连接到 Azure DevOps。

1. 在浏览器中选择“Azure 门户”/“Microsoft Sentinel”选项卡。
1. 在 Microsoft Sentinel 中，选择“内容管理”部分中的“存储库”。
1. 在工具栏中选择“新增”。
1. 对于名称，请输入“我的内容”。
1. 对于源代码管理，选择“Azure DevOps”。
1. Select <bpt id="p1">**</bpt>Authorize<ept id="p1">**</ept>.  Then <bpt id="p1">**</bpt>Accept<ept id="p1">**</ept>.
1. 选择之前创建的组织。
1. 选择之前创建的项目。
1. 选择之前创建的存储库。
1. 选择主分支。
1. 选择所有内容类型。
1. 然后选择“创建”。


1. On the Repositories page, select <bpt id="p1">**</bpt>Refresh<ept id="p1">**</ept>.  Wait until <bpt id="p1">*</bpt>Last deployment status<ept id="p1">*</ept> is <bpt id="p2">*</bpt>Failed<ept id="p2">*</ept>.  

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The <bpt id="p2">*</bpt>Failed<ept id="p2">*</ept> status is due to limitations in the hosted lab environment. You would normally see <bpt id="p1">*</bpt>Succeeded<ept id="p1">*</ept>. Then you can see in the <bpt id="p1">*</bpt>Analytics<ept id="p1">*</ept> the imported rule <bpt id="p2">*</bpt>Rule from Azure DevOps<ept id="p2">*</ept>.


## <a name="you-have-completed-the-lab"></a>你已完成本实验室。
