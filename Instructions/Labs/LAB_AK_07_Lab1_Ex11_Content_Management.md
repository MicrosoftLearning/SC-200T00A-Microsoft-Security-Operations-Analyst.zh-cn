---
lab:
  title: 练习 11 - 在 Microsoft Sentinel 中使用存储库
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 学习路径 7 - 实验室 1 - 练习 11 - 在 Microsoft Sentinel 中使用存储库

## 实验室方案

你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。 你已创建“计划”规则和“Microsoft 安全分析”规则。  需要在 Azure DevOps 存储库中集中分析规则。  然后将 Sentinel 连接到 Azure DevOps 存储库并导入内容。 

>**注意：** 我们提供 **[交互式实验室模拟](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Use%20repositories%20in%20Microsoft%20Sentinel)** ，让你能以自己的节奏点击浏览实验室。 你可能会发现交互式模拟与托管实验室之间存在细微差异，但演示的核心概念和思想是相同的。 


### 任务 1：创建并导出分析规则

在此任务中，将在 Microsoft Sentinel 中启用实体行为分析。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. 在左侧边栏选项卡的“配置”区域下，选择 Analytics。

1. 选择之前创建的 Startup RegKey 规则。

1. 在工具栏中选择“导出”。 提示：可能需要选择省略号图标 (...) 才能看到它 。

1. 规则将导出到名为 Azure_Sentinel_analytic_rule.json 的文本文件。

1. 在下载的文件的名称下方选择“打开文件”，然后选择“更多应用” 。

1. 选择“记事本”，然后选择“确定” 。

1. 查看 Azure 资源管理器模板并在完成后将其关闭。


### 任务 2：创建 Azure DevOps 环境

在此任务中，你将创建 Azure DevOps 存储库。

1. 在浏览器中打开另一个标签页，然后导航到 (https://aexprodcus1.vsaex.visualstudio.com/me?mkt=en-US) 。

1. 在“我们需要更多详细信息”页上，选择“继续” 。

1. 在“Azure DevOps 入门”页面上，选择“创建新组织”，然后选择“继续” 。

1. 在“即将完成...”页面上，为 DevOps 组织输入一个将来不想使用的名称，例如你的租户前缀。 提示：可以在实验室的“资源”选项卡中找到它。

1. 输入看到的字符，然后继续。

1. 在“创建项目以开始”页上，输入“我的 Sentinel 内容”，然后选择“创建项目” 。

1. 导航到左窗格中的“存储库”。

1. 在该区域的页面底部“使用 README 或 gitignore 初始化主分支”，选择“初始化”。

1. 页面应显示存储库的文件。  唯一的文件是 README.me。

1. 在“文件”（页面右侧）边栏选项卡上，工具栏包含“设置生成”、“克隆”等选项，选择冒号图标 (:) 可显示更多选项 。

1. 选择“上传文件”。

1. 选择“浏览”，然后从“下载”目录中选择“Azure_Sentinel_analytic_rule.json”文件。

1. 选择“提交”。

1. 选择页面左上角的“Azure DevOps”。  这将显示你的组织和项目。

1. 选择左下角的“组织设置”。

1. 在左侧边栏选项卡的“安全”区域下选择“策略”。

1. 在“应用程序连接策略”区域下，启用“通过 OAuth 进行第三方应用程序访问” 。


### 任务 3：将 Sentinel 连接到 Azure DevOps。

1. 在浏览器中选择“Azure 门户”/“Microsoft Sentinel”选项卡。

1. 在 Microsoft Sentinel 中，选择“内容管理”部分中的“存储库(预览版)”。

1. 在工具栏中选择“+ 新增”按钮。

1. 对于名称，请输入“我的内容”。

1. 对于源代码管理，选择“Azure DevOps”。

1. 选择“授权”。**** 向下滚动权限请求，然后选择“接受”。

1. 选择之前创建的组织（如 WWLx...）。

1. 选择之前创建的项目“我的 Sentinel 内容”。

1. 选择之前创建的存储库“我的 Sentinel 内容”。 提示：可能需要在下拉列表中向下滚动才能看到该存储库。

1. 选择“主”分支。 提示：可能需要在下拉列表中向下滚动才能看到该分支。

1. 选择所有内容类型。

1. 然后选择“创建”。

1. 如果需要，返回到 Microsoft Sentinel 工作区

1. 转到“存储库(预览版)”页，选择“刷新”。 等到“上次部署状态”变为“失败”。  

    >注意：“失败”状态是由托管实验室环境中的限制造成的。 通常会看到“成功”。 然后，可以在“分析”中看到导入规则“来自 Azure DevOps 的规则”。


## 你已完成本实验室。
