# ServiceNow CSA 认证考试真题整理笔记

说明：本文档汇总上周全部 CSA 考试原题，按核心模块分类整理，标注**正确答案**、考点解析及易错提醒，适配考前快速背诵与查漏补缺，所有术语采用官方标准译法，贴合考试出题逻辑。

# 一、更新集（Update Set）模块

## 题目1：更新集应用到目标实例步骤

**题干**：Which sequence of actions applies an update set to an instance?

**选项翻译**：

- A、B、C为干扰步骤（略）
- **D、Retrieve → Preview → Commit**

**正确答案**：D

**核心考点**：更新集标准部署流程，**严禁跳过Preview直接Commit**，Preview用于检查冲突，Commit用于正式生效变更，Retrieve是先将更新集拉取到目标实例。

**考试提醒**：固定三步顺序，是高频必考题，顺序不可颠倒。

## 题目2：更新集追加变更场景

**核心考点**：需追加新配置到现有更新集，先切换该更新集为**当前更新集**，后续操作自动捕获变更，无需重新创建。

# 二、CMDB/CSDM/ITIL 核心概念区分

## 题目1：基础设施与业务服务依赖追踪

**题干**：What enables you to trace from an infrastructure item to the Services dependent on it?

**正确答案**：B（Relationships / 关系）

**考点解析**：CMDB中通过关系（Depends On/Used By）链接配置项与服务，是依赖追踪核心，Automapping是工具而非核心机制。

## 题目2：跨产品标准服务与CMDB框架

**正确答案**：A（Common Services Data Model / CSDM）

## 概念速记（必背）

- **ITIL**：服务管理**方法论/最佳实践**，指导流程规范
- **CMDB**：存储配置项（CI）及关系的**数据库**
- **CSDM**：统一CMDB数据结构的**标准模型**，解决数据混乱问题

# 三、服务目录（Service Catalog）模块

## 题目1：80个目录项公共字段复用

**题干**：80个目录项共享4个必填公共字段，其余字段独有，如何设计表单？

**正确答案**：B（为4个变量创建Variable Set，添加到所有目录项）

**考点解析**：Variable Set（变量集）是公共字段复用核心功能，无代码、一次配置多处生效；Order Guide用于多项目订购，Record Producer用于生成业务记录，均不适用。

## 题目2：创建新目录项模块

**正确答案**：Maintain Items（标准创建编辑模块，Catalog Items仅为列表视图）

# 四、ACL 权限控制模块（高频易错）

## 题目1：ACL控制的数据库对象

**题干**：ACL rules control access to database objects，指什么？

**正确答案**：B（特定行、列、表格）

**考点解析**：数据库对象=表（整体）、列（字段）、行（单条记录）；角色/组是权限授予对象，并非数据库对象。

## 题目2：ACL规则评估逻辑

**正确答案**：C（行级+字段级规则同时生效，才允许操作）

**核心规则**：优先级：字段级 > 行级 > 表级；多规则共存需全部满足，默认无允许则拒绝。

## 题目3：表全字段ACL通配符

**正确答案**：incident.*（表名.*代表该表所有字段，字段级ACL）

# 五、用户认证与账户字段

## 题目1：ServiceNow支持的认证方式

**正确答案**：B（本地数据库）、C（LDAP）、D（SSO）

**排除项**：XML、FTP不属于认证方式

## 题目2：核心用户字段释义

- **locked_out**：sys_user表字段，账户锁定（多次输错密码触发，值为true），管理员可改false解锁
- **hashed_user_id**：哈希加密用户ID，用于隐私合规，不可逆加密
- **inactive**：账户禁用，区别于锁定

# 六、业务规则（Business Rule）模块

## 题目：创建Business Rule必填配置

**正确答案**：Table（作用表）、Timing（触发时机）、Condition（执行条件）、Script to run（执行脚本）

**考点提醒**：业务规则默认系统权限运行，无需指定执行用户；UI Action与业务规则无关。

# 七、报表与绩效分析（Reporting vs PA）

## 题目：两者核心区别

**正确答案**：A

**核心区分**：

- Reporting：实时查询，仅展示当前数据，无历史快照
- Performance Analytics（PA）：定时采集数据快照，可做历史趋势与KPI对比

# 八、Flow Designer 模块

## 题目：使用应用触发器前置操作

**正确答案**：C（激活对应应用辐条+所需插件）

**考点解析**：Spoke（辐条）封装第三方应用能力，仅激活插件无法使用触发器。

# 九、数据导入模块

## 题目1：支持的导入数据源

**正确答案**：本地文件（CSV/Excel/XML）、JDBC、Network Server、LDAP

## 题目2：表格数据标准导入步骤

**流程**：Load Data → Create Transform Map → Run Transform

# 十、UI控制类（UI Policy/Client Script）

## 题目：无代码控制字段必填/只读

**正确答案**：UI Policy

**考点区分**：

- UI Policy：纯无代码，前端界面控制
- Client Script：需JS代码，属于编码实现，不符合题干无代码要求
- ACL：后端权限控制，不控制界面状态

# 十一、知识库模块

## 题目：控制文章发布/下架流程

**正确答案**：Workflows（工作流）

**考点解析**：Workflow是流程引擎，驱动审批、状态变更、通知全生命周期；State Lifecycle仅定义状态，不执行动作。

**备考小贴士**：CSA考试侧重场景应用与概念区分，易混点（ACL/UI Policy、CMDB/CSDM、Reporting/PA）重点记忆，固定流程类题目记死顺序，正确率更高。

# 十二、表单展示与UI组件模块

## 题目1：表单活动与历史记录展示

**题干**：Which displays the list of activities, or history, on a form?

**选项翻译**：

- A、Formatter
- B、ACL
- C、UI Policy
- D、Client Script

**正确答案**：A

**考点解析**：Activity Formatter是表单专用格式化组件，专门用于展示操作历史、字段变更、备注、审批记录等动态内容，属于前端展示组件。ACL负责权限管控，UI Policy和Client Script控制字段状态，均不负责历史内容展示，这是考试高频易错题，切记区分组件功能。

## 题目2：过滤条件固定选择列表组件

**题干**：在ServiceNow过滤条件中，哪一项始终以选择列表形式呈现，无法手动输入？

**选项翻译**：

- A、Operator（操作符）
- B、Filter Criteria（过滤标准）
- C、Operation
- D、Match Criteria（匹配标准）

**正确答案**：A

**考点解析**：Operator即操作符（=、≠、>、<、contains等），是系统预设固定选项，只能下拉选择，无法自定义输入；字段值会随字段类型变化，可能是输入框、日期选择器，并非固定选择列表，考试常考组件形态，牢记此点即可快速得分。

# 十三、系统核心表名与基础术语模块

## 题目1：Group表平台标准名称

**题干**：What is the platform name for the Group table?

**正确答案**：C（sys_user_group）

**考点解析**：ServiceNow系统核心表均以sys_开头，用户组表标准名称为sys_user_group，用于存储用户组信息、组管理员及成员关系，是用户权限与审批配置的核心表，考试常考系统表原名，需牢记高频表名。

## 题目2：Data Pill Picker快捷点走操作

**题干**：When using the Data Pill Picker, use which keys to dot-walking to fields in other tables?

**正确答案**：C（Arrows 箭头键）

**考点解析**：在Flow Designer和报表配置的Data Pill Picker中，使用箭头键可展开关联表，实现跨表点走（Dot-Walking），快速导航到关联表字段，属于操作类基础考点，记忆对应快捷键即可。

# 十四、高频易混概念对比表（考前必看）

| **易混概念**  | **核心功能**                         | **考试关键词**             | **易错提醒**                       |
| :------------ | :----------------------------------- | :------------------------- | :--------------------------------- |
| UI Policy     | 无代码前端控制，字段显隐、必填、只读 | 无代码、界面控制、表单字段 | 不具备后端权限，可被绕过           |
| Client Script | JS代码前端控制，灵活实现复杂交互逻辑 | 编码、JS、前端脚本         | 需要写代码，不符合无代码需求       |
| ACL           | 后端权限管控，控制数据访问权限       | 权限、拒绝访问、表/行/字段 | 默认拒绝，优先级高于前端控制       |
| Variable Set  | 服务目录公共变量复用                 | 多目录项、共享字段、无代码 | 和Order Guide、Record Producer区分 |
| Workflow      | 流程自动化，驱动审批、状态流转       | 生命周期、审批、自动通知   | 和状态生命周期（State）区分        |

# 十五、CSA考试速记口诀（高频考点）

- 更新集三步曲：检索、预览再提交，跳过预览必出错
- ACL管控对象：表行列，角色组是授权方
- 概念区分：ITIL是方法，CMDB是数据库，CSDM是标准
- 前端控制：无代码选UI Policy，要编码选Client Script
- 报表区别：报表看实时，PA看快照趋势

**补充说明**：本次新增内容均为CSA考试高频原题，贴合真题出题思路，和原有模块无缝衔接，整体覆盖权限、组件、系统表、操作快捷键全考点，可直接用于考前完整复盘，重点背诵加粗内容和口诀即可快速提分。