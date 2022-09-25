---
lab:
  title: 练习 10 - 创建工作簿
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-10---create-workbooks"></a>模块 7 - 实验室 1 - 练习 10 - 创建工作簿

## <a name="lab-scenario"></a>实验室方案

![实验室概述。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex8.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. Once you have connected your data sources to Microsoft Sentinel, you can visualize and monitor the data using the Microsoft Sentinel adoption of Azure Monitor Workbooks, which provides versatility in creating custom dashboards. 

Microsoft Sentinel 可让你跨数据创建自定义工作簿，并且还附带了内置的工作簿模板，使你可以在连接数据源后快速获得对数据的见解。


### <a name="task-1-explore-workbook-templates"></a>任务 1：探索工作簿模板

在此任务中，你将探索 Microsoft Sentinel 工作簿模板。

1. 使用以下密码以管理员身份登录到 WIN1 虚拟机：**Pa55w.rd**。  

1. 在 Microsoft Edge 浏览器中，导航到 Azure 门户 (https://portal.azure.com )。

1. 在“登录”对话框中，复制粘贴实验室托管提供者提供的租户电子邮件帐户，然后选择“下一步”  。

1. 在“输入密码”对话框中，复制粘贴实验室托管提供者提供的租户密码，然后选择“登录”  。

1. 在 Azure 门户的搜索栏中，键入“Sentinel”，然后选择“Microsoft Sentinel”。

1. 选择 Microsoft Sentinel 工作区。

1. Select <bpt id="p1">**</bpt>Workbooks<ept id="p1">**</ept>. The <bpt id="p1">*</bpt>Templates<ept id="p1">*</ept> tab is selected by default.

1. Search for and select the <bpt id="p1">**</bpt>Identity &amp; Access<ept id="p1">**</ept> template workbook. In the right pane, scroll down and select the <bpt id="p1">**</bpt>View template<ept id="p1">**</ept> button.

1. Review the contents of the workbook. It shows insights into Identity and access operations by collecting and analyzing security logs, using the audit and sign-in logs to gather insights into use of Microsoft products.

1. 选择右上角的“X”关闭工作簿。


### <a name="task-2-save-and-modify-a-workbook-template"></a>任务 2：保存并修改工作簿模板

在此任务中，你将保存并修改工作簿模板。

1. 应返回“Microsoft Sentinel - 工作簿 - 模板”选项卡。搜索并选择“Azure AD 审核日志”，然后在右侧窗格中，向下滚动选择“保存”按钮 。 

1. 将“区域”的默认值保留为“美国东部”，然后选择“确定”。

1. 选择“查看保存的工作簿”按钮。

1. 在命令栏中选择“编辑”以对工作簿进行更改。

1. Read the banner that informs you of a new feature to compare workbooks. Dismiss the message by selecting the banner.

1. 你是一位安全运营分析师，你所在公司已实现 Microsoft Sentinel。

1. 将数据源连接到 Microsoft Sentinel 后，可以使用采用 Microsoft Sentinel 的 Azure Monitor 工作簿来可视化和监视数据，这在创建自定义仪表板方面提供了多样性。

1. 在显示的“编辑列设置”边栏选项卡中，选择“列”中的“操作计数(热度地图 + 已设置格式)” 。

1. Review the settings, in particular the options for <bpt id="p1">*</bpt>Column renderer<ept id="p1">*</ept>. For <bpt id="p1">*</bpt>Color palette<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>32-color categorical<ept id="p2">**</ept>.

1. 在“列”中，选择“趋势(迷你图 + 已设置格式)”。

1. 查看设置，对于“列呈现器”，选择“迷你图区域”，然后在“调色板”中选择你所选的颜色。

1. Select <bpt id="p1">**</bpt>Save and Close<ept id="p1">**</ept>. Now we are going to review how one tile/grid control can be used to filter the results in another tile/grid.

1. 选择“编辑查询项: 查询 - 2”的命令栏中的“高级设置”按钮。

1. Review the <bpt id="p1">*</bpt>When items are selected, export parameters<ept id="p1">*</ept> setting. Notice the <bpt id="p1">*</bpt>UserInfo<ept id="p1">*</ept> field is selected.

1. Scroll down and select <bpt id="p1">**</bpt>Done Editing<ept id="p1">**</ept> at the bottom of the query (not the top menu). Look at the changed colors for <bpt id="p1">*</bpt>Operations count<ept id="p1">*</ept> and <bpt id="p2">*</bpt>Trend<ept id="p2">*</ept>.

1. 选择屏幕右侧的“最活跃的用户”饼图下的“编辑”。  

1. In the <bpt id="p1">*</bpt>Logs query<ept id="p1">*</ept>, locate <bpt id="p2">*</bpt>UserInfo<ept id="p2">*</ept>. The query is using the parameter exported from the other query to filter results.

1. 向下滚动并选择查询底部（不是顶部菜单）的“完成编辑”。

1. Scroll up and select <bpt id="p1">**</bpt>Done Editing<ept id="p1">**</ept> at the top menu and select the <bpt id="p2">**</bpt>Save<ept id="p2">**</ept> icon. Close the workbook by selecting the <bpt id="p1">**</bpt>X<ept id="p1">**</ept> in the top-right corner.


### <a name="task-3-create-a-workbook"></a>任务 3：创建工作簿

在此任务中，你将新建一个带有高级可视化的工作簿。

1. 应返回 Microsoft Sentinel 门户的“工作簿”区域。

1. 选择“+ 添加工作簿”，从头开始创建新工作簿。 

    >**注意：** 尽管它是一个新工作簿，但使用的是启动模板。

1. 要编辑工作簿，请选择“编辑”。

1. 选择工作簿第一段下面的“编辑”按钮 

1. 在“## 新建工作簿”顶部键入“# 我的工作簿” 。

1. Select <bpt id="p1">**</bpt>Done Editing<ept id="p1">**</ept> on the bottom menu, for the <bpt id="p2">*</bpt>Editing text item: text - 2<ept id="p2">*</ept>. Notice that your header increased size and name changed.

1. 在唯一可见的条形图下，选择“编辑”。

1. 查看可提供所有表的联合计数语句的 KQL 语句。

1. 对于“编辑查询项: 查询 - 2”，向下滚动并选择底部菜单中的“完成编辑”。

1. 选择条形图的“编辑”按钮旁边的省略号“...”，再选择“+ 添加”，然后选择“添加查询” 。

1. 在“查询”框中键入“SecurityEvent”。

1. 将时间范围更改为“过去 4 小时”。

1. 将可视化效果更改为“时间图表”。

1. 从查询的命令栏中选择“样式”。

1. 选择“将此项设置为自定义宽度”框。

1. 将宽度百分数设置为 25，将最大宽度设置为 25。

1. 现在从查询的命令栏中选择“高级设置”。

1. 选择“未进行编辑时显示刷新图标”框。 

1. 对于新的“编辑查询项: 查询 - 2”，向下滚动并选择底部菜单中的“完成编辑”。

1. 向下滚动并选择工作簿底部的“+ 添加”，然后选择“添加查询” 。

1. 在“查询”框中键入“SecurityEvent”。

1. 将时间范围更改为“过去 4 小时”。

1. 将可视化效果更改为“网格”。

1. 从查询的命令栏中选择“样式”。

1. 选择“将此项设置为自定义宽度”框。

1. 将宽度百分数设置为 75，将最大宽度设置为 75。

1. 对于新的“编辑查询项: 查询 - 3”，向下滚动并选择底部菜单中的“完成编辑”。

1. 在工作簿的命令栏中选择“完成编辑”。

1. Select the <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> icon, change the <bpt id="p2">*</bpt>Title<ept id="p2">*</ept> to <bpt id="p3">**</bpt>My Workbook<ept id="p3">**</ept> and leave other values as default. Select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> again to commit the changes. 

1. 选择右上角的“X”关闭工作簿，也可在 Microsoft Sentinel 门户中选择“工作簿”来关闭 。

1. 返回“工作簿”页面，选择我的工作簿”选项卡。

1. 选择刚创建的工作簿“我的工作簿”。

1. 在右侧窗格中，选择“查看保存的工作簿”以查看工作簿。

## <a name="proceed-to-exercise-11"></a>继续完成练习 11
