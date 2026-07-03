# Mo Architecture｜MarkOrbit 核心架构白皮书

版本：Draft 1.0  
适用范围：MarkOrbit 长期架构、Lite 1.1 重规划、Mo Brain / Mo Flow / Mo Guide 后续建设  
核心定位：Mo 是 MarkOrbit 的行业能力操作系统，不是单一产品

---

## 0. 执行摘要

Mo 是 MarkOrbit 的核心架构体系。

它不是一个页面、一个 SaaS 模块，也不是单一 AI 助手，而是 MarkOrbit 面向全球商标行业建设的行业能力底座。

Mo 的长期目标是支撑：

- 全球商标数据连接；
- 全球商标知识理解；
- 行业机会发现；
- 智能客户沟通；
- 业务流程执行；
- 商标交易与推荐；
- 代理网络协作；
- 内容营销与分布式增长；
- 官网、小程序、Lite、API、MCP 等多入口调用。

Mo 的核心逻辑可以概括为：

> **Data → Brain → Intelligence → Capability → Skill → Workflow → Guide → Flow → Applications**

再压缩成一句话：

> **Mo Data 负责连接世界，Mo Brain 负责理解世界，Mo Intelligence 负责发现价值，Capability 定义行业能力，Skill 实现能力，Workflow 编排业务，Mo Guide 理解用户，Mo Flow 完成业务，Lite 等应用让用户真正使用。**

---

## 1. Mo 的总体定位

MarkOrbit 的长期目标不是只做一个商标 SaaS，也不是只做一个 AI 助理，而是构建：

> **全球商标数字基础设施｜Trademark Digital OS**

Mo 就是这个基础设施的核心操作系统。

它负责把全球商标行业中的数据、知识、主体、规则、案例、需求、流程、内容、营销、交易、服务商和用户行为统一沉淀、理解、编排和调用。

从业务上看，Mo 要服务四类用户：

1. 中国商标代理人；
2. 品牌方和跨境电商企业；
3. 全球商标律师和服务商；
4. 未来的 AI Agent、API 用户和第三方系统。

从系统上看，Mo 要支撑多个应用：

- MarkOrbit Lite；
- MarkReg；
- MGSN；
- 官网 AI 咨询；
- 小程序；
- 商标交易平台；
- AI 命名产品；
- AI 查询产品；
- AI 监测产品；
- API；
- SDK；
- MCP；
- 第三方插件。

---

## 2. Mo 的核心链路

Mo 的完整链路为：

```text
Mo Data
  ↓
Mo Brain
  ↓
Mo Intelligence
  ↓
Capability Catalog
  ↓
Skill Library
  ↓
Workflow Catalog
  ↓
Mo Guide
  ↓
Mo Flow
  ↓
Applications
```

需要注意：

- 这不是严格单向调用关系；
- Mo Guide 是面向用户的横向编排入口；
- Mo Guide 可以调用 Brain、Intelligence、Capability、Workflow 和 Flow；
- Workflow Catalog 定义流程；
- Mo Flow 负责流程运行；
- Applications 是不同用户场景的产品入口。

---

## 3. 六大核心模块

### 3.1 Mo Data｜数据底座

#### 回答的问题

> 世界上发生了什么？

Mo Data 负责持续获取、清洗、同步和关联全球商标相关数据。

它不是简单数据库，而是未来的：

> **全球商标 Entity Graph**

也就是把全球商标行业中的对象全部连接起来。

#### 数据范围

Mo Data 覆盖：

- 各国商标官方数据；
- 商标公告；
- 商标申请、驳回、复审、异议、无效、撤销、续展、转让、许可数据；
- 各国法律法规；
- 官方指南；
- 法院判决；
- 审查案例；
- 申请人；
- 代理机构；
- 律师；
- 商品服务项目；
- 企业官网；
- 电商平台；
- 社交媒体；
- 新闻资讯；
- 交易数据；
- 服务商数据。

#### Entity Graph

Mo Data 最终要形成实体图谱，关联以下对象：

- 商标；
- 申请人；
- 代理人；
- 律师；
- 国家；
- 案件；
- 商品；
- 类别；
- 企业；
- 品牌；
- 官网；
- 社媒；
- 电商店铺；
- 订单；
- 文件；
- 证据；
- 案例；
- 服务商。

#### 当前落地边界

Lite 1.1 不建设完整 Mo Data。

Lite 1.1 只做：

- 用户商标资产；
- 用户上传素材；
- 用户商机；
- 平台已有 CountryPrice；
- 内容素材库的轻量数据；
- 外部数据源字段预留。

完整 Mo Data 应在 Mo Brain / Mo Data 专项系统中逐步建设。

---

### 3.2 Mo Brain｜知识与规则中心

#### 回答的问题

> 我知道什么？这些知识意味着什么？

Mo Brain 负责把 Mo Data 和 Raw 资料编译成可被 AI、业务流程、内容生成和客户解释调用的行业知识。

#### Mo Brain 的内容层

Mo Brain 包括：

- Raw 原始资料；
- Wiki 知识页面；
- Structured Data 结构化知识；
- Rules 规则；
- Decision 决策逻辑；
- SOP 流程；
- FAQ 问答；
- Prompt；
- Content Library 内容库；
- Best Practice 实务经验；
- Risk Notes 风险提示；
- Pricing Knowledge 报价知识；
- Materials Requirement 材料要求。

#### Wiki 的定位

Mo Brain 的 Wiki 不是普通知识库，而是：

> **AI 问答、业务决策、内容生成、客户解释和流程执行的统一底稿。**

一个 Wiki 页面不只是给人看的文章，也应该能被系统解析和调用。

例如 `US Section 8.md` 不应只解释 Section 8 是什么，还应包含：

- 核心事实；
- 法律依据；
- 适用条件；
- 期限；
- 宽展期；
- 风险；
- 所需材料；
- 实务经验；
- 客户话术；
- 短视频角度；
- FAQ；
- 相关主题；
- 相关 Workflow；
- 相关 Capability；
- 来源链接；
- 更新时间。

#### Mo Brain 与 Lite 1.1 的关系

Lite 1.1 不真实接入完整 Mo Brain。

Lite 1.1 只做：

- BrainConnector disabled；
- 数据源字段预留；
- Mo Knowledge 用户私有知识库；
- 平台内置少量主题与模板；
- 未来接入 Mo Brain 的权限边界。

Mo Brain 预计在 1.2 / 1.5 后逐步接入 Lite。

---

### 3.3 Mo Intelligence｜洞察与增长中心

#### 回答的问题

> 哪里有机会？下一步应该做什么？

Mo Intelligence 负责基于 Mo Data + Mo Brain 做分析、预测、推荐和营销。

它不等待用户提问，而是主动发现价值。

#### 典型能力

Mo Intelligence 可以发现：

- 存量商标续展需求；
- Section 8 / Section 9 / Section 15 等期限需求；
- 某企业海外布局空白；
- 某代理只做美国但没有欧盟业务；
- 某申请人注册了美国但没有注册中国；
- 某品牌在跨境平台爆发但未完成商标保护；
- 某行业出现新品牌浪潮；
- 某代理客户可能需要监测服务；
- 某待售商标适合推荐给某类客户；
- 某客户有转化为订单的可能；
- 某内容主题适合某个代理今天发布。

#### 核心能力范围

Mo Intelligence 包括：

- 商机发现；
- 客户画像；
- 品牌画像；
- 代理画像；
- 商标风险预测；
- 申请趋势分析；
- 存量商标需求挖掘；
- 自动营销推荐；
- 内容分发建议；
- 成交概率预测；
- 推荐页匹配；
- 报价策略建议。

#### 与分布式自动营销体系的关系

Mo Intelligence 是未来分布式自动营销体系的基础。

它可以支撑：

- 给代理人推荐今日营销主题；
- 给代理人推荐可推广客户；
- 给代理人推荐适合转发的商标；
- 自动生成客户跟进话术；
- 根据客户画像推荐国家和服务；
- 根据商标资产生成推荐页；
- 根据官方数据触发续展、宣誓、监测等营销动作。

#### Lite 1.1 的边界

Lite 1.1 只实现局部 Intelligence：

- 简单主题推荐；
- 主题偏好记录；
- 素材推荐；
- 商机跟进建议；
- 商标推荐页建议；
- 报价方案建议。

完整 Mo Intelligence 后置。

---

### 3.4 Mo Guide｜统一智能入口

#### 回答的问题

> 用户真正想做什么？我应该怎么沟通？

Mo Guide 是整个 MarkOrbit 的统一智能入口。

它不是普通聊天机器人，而是：

> **AI 顾问 + AI 销售 + AI 业务需求采集引擎 + 能力编排器**

#### Mo Guide 的四个核心概念

Mo Guide 围绕四个核心概念工作：

1. **Intent**：用户想做什么。
2. **State**：当前已经知道什么。
3. **Checklist**：完成业务还缺什么。
4. **Next Best Question**：下一句最该问什么。

#### 示例：客户只上传 Logo

客户只上传 Logo 时，Mo Guide 应判断：

- 已有：商标图样；
- 缺少：国家、申请人、商品、类别、使用情况；
- 下一步：优先询问销售国家或销售平台；
- 可能动作：生成申请信息清单；
- 可能后续：进入报价或订单流程。

#### 示例：客户上传完整信息表

Mo Guide 应判断：

- 信息基本完整；
- 可生成申请确认表；
- 可生成 POA；
- 可生成报价；
- 可创建 Markreg 订单；
- 可进入 Mo Flow。

#### Mo Guide 的核心价值

Mo Guide 的核心不是“问固定问题”，而是：

> 根据客户输入动态判断业务完成度，并用最容易回答、最有销售转化价值的问题继续沟通。

#### Mo Guide 的调用方式

Mo Guide 不应该靠一堆 Prompt 随机工作，而应该像编排器一样调用 Capability。

例如客户说：

> 我想注册一个商标，主要做亚马逊。

Guide 的执行链可能是：

```text
UnderstandIntent
  ↓
ExtractBusinessInfo
  ↓
RecommendCountry
  ↓
RecommendClass
  ↓
CheckFilingChecklist
  ↓
NextBestQuestion
  ↓
GenerateQuotation
  ↓
GeneratePOA
```

Mo Guide 的价值是知道：

- 该调用哪个能力；
- 按什么顺序调用；
- 什么时候继续问客户；
- 什么时候进入 Mo Flow；
- 什么时候需要人工审核。

#### Mo Guide 是横向编排入口

虽然架构图中 Mo Guide 位于 Workflow 之上，但实际调用中，Mo Guide 是横向编排入口。

它可以调用：

- Mo Brain；
- Mo Intelligence；
- Capability；
- Skill；
- Workflow；
- Mo Flow；
- Mo Workspace；
- Mo Content；
- Mo Marks；
- Mo Global；
- Mo Leads。

---

### 3.5 Mo Flow｜业务执行平台

#### 回答的问题

> 这件事怎么真正办完？

Mo Flow 负责把咨询、推荐、确认转化为实际业务流程。

Mo Flow 不负责“懂知识”，而是负责执行。

#### Mo Flow 覆盖的业务

Mo Flow 覆盖：

- 商标申请；
- 商标查询；
- 商标购买；
- 商标监测；
- OA；
- 驳回复审；
- 异议；
- 无效；
- 撤销；
- 续展；
- 转让；
- 许可；
- 付款；
- 审批；
- 律师协作；
- 通知；
- 任务；
- 文件；
- 交付；
- 状态跟踪。

#### Workflow Catalog 与 Mo Flow 的关系

必须明确：

> **Workflow Catalog 是流程定义，Mo Flow 是流程运行时。**

例如：

`US Trademark Filing Workflow` 是定义。它说明美国商标申请要经过哪些步骤、调用哪些 Capability、需要哪些材料、什么时候人工审核。

`Mo Flow` 是执行。它真正创建订单、生成文件、分配任务、通知律师、记录状态、推进交付。

#### 示例：美国商标申请

```text
Guide 收集需求
  ↓
Brain 提供规则
  ↓
Capability 检查信息
  ↓
Flow 生成确认表
  ↓
Flow 生成 POA
  ↓
Flow 创建订单
  ↓
Flow 分配律师
  ↓
Flow 跟踪提交
  ↓
Flow 推送状态
  ↓
Lite 展示给代理人
```

#### Lite 1.1 的边界

Lite 1.1 只局部复用 Mo Flow：

- Markreg Order；
- Opportunity；
- MGSN CountryPrice / CountryService；
- CaseAssignment；
- QuotePlan 转 Order；
- 询盘转 Opportunity；
- 商机转报价；
- 商机转订单。

完整 Mo Flow 后置。

---

### 3.6 Applications｜应用层

#### 回答的问题

> 用户在哪里使用这些能力？

Applications 是 Mo 能力的产品入口。

#### 第一阶段核心应用：MarkOrbit Lite

第一阶段最重要的是 MarkOrbit Lite。

它面向商标代理人，是代理人的 AI 工作平台。

第一波目标用户是代理人，所以 Lite 应该优先：

- 工具化；
- 效率化；
- 内容生产化；
- 报价方案化；
- 商标推荐化；
- 商机跟进行动化。

#### 未来应用

未来 Applications 包括：

- MarkOrbit Lite；
- MarkReg 官网；
- 官网 AI 咨询；
- 小程序；
- 品牌方客户端；
- 商标交易平台；
- AI 命名产品；
- AI 查询产品；
- AI 监测产品；
- API；
- SDK；
- MCP；
- 第三方插件；
- Agent 调用入口。

#### Lite 只是一个入口

Lite 不是 Mo 的全部。

从底层看，Lite 只是 Mo 能力的一个应用入口。

但在当前阶段，Lite 是最优先落地的入口，因为它最接近现有代理人用户和现有业务收入。

---

## 4. 四张核心 Catalog

Mo 架构真正稳定的地方，不是代码，而是四张目录。

### 4.1 Entity Catalog｜对象目录

#### 回答的问题

> 世界里有什么？

Entity Catalog 定义 MarkOrbit 世界中的对象。

#### 核心对象

包括：

- 商标；
- 申请人；
- 代理机构；
- 律师；
- 案件；
- 国家；
- 商品；
- 类别；
- 品牌；
- 企业；
- 订单；
- 客户；
- 商机；
- 证据；
- 文件；
- 报价；
- 服务商；
- 内容主题；
- 素材；
- 模板；
- 推荐页；
- 询盘；
- 工作流。

#### 作用

Entity Catalog 是 Mo Data 和 Entity Graph 的基础。

它让系统知道：

- 数据属于什么对象；
- 对象之间怎么关联；
- 对象可被哪些能力调用；
- 对象在哪些流程中出现；
- 哪些对象是用户私有；
- 哪些对象是平台公共；
- 哪些对象可被 Mo Brain 读取。

---

### 4.2 Knowledge Catalog｜知识目录

#### 回答的问题

> 关于这些对象，我们知道什么？

Knowledge Catalog 定义 Mo Brain 维护的知识类型。

#### 知识范围

包括：

- 国家知识；
- 流程知识；
- 法律知识；
- 案例知识；
- 费用知识；
- 期限知识；
- 实务经验；
- 风险规则；
- 内容知识；
- 材料要求；
- 客户话术；
- 销售话术；
- 平台规则；
- 交易规则。

#### 作用

Knowledge Catalog 用于支撑：

- AI 问答；
- 客户解释；
- 风险提示；
- 报价说明；
- 内容生成；
- 视频脚本；
- 流程判断；
- POA 生成；
- OA 分析；
- Workflow 执行。

---

### 4.3 Capability Catalog｜能力目录

#### 回答的问题

> 基于这些对象和知识，我们能做什么？

Capability 是行业能力定义，不是代码。

它定义：

- 能力名称；
- 输入；
- 输出；
- 依赖对象；
- 依赖知识；
- 适用场景；
- 风险边界；
- 人工审核要求；
- 可能的 Skill 实现。

#### 典型 Capability

例如：

- 识别客户意图；
- 提取申请人信息；
- 推荐申请国家；
- 推荐类别；
- 推荐商品；
- 检查申请清单；
- 解释 OA；
- 生成 POA；
- 生成报价；
- 创建订单；
- 发现续展商机；
- 匹配在售商标；
- 生成营销内容；
- 生成客户回复；
- 生成视频脚本；
- 推荐素材；
- 生成商机跟进话术。

#### Capability 不是 Skill

Capability 是能力规范。Skill 是能力实现。

同一个 Capability 可以有多个 Skill 实现。

今天用 GPT，明天用规则引擎，后天用本地模型，Capability 不变。

---

### 4.4 Workflow Catalog｜业务编排目录

#### 回答的问题

> 这些能力如何组合成完整业务？

Workflow Catalog 定义业务流程。

#### 典型 Workflow

包括：

- 美国商标申请 Workflow；
- 欧盟商标申请 Workflow；
- Section 8 宣誓 Workflow；
- 商标购买 Workflow；
- OA 答复 Workflow；
- 商标交易 Workflow；
- 客户营销 Workflow；
- 每日内容生产 Workflow；
- 全球报价 Workflow；
- 商机跟进 Workflow。

#### Workflow 的组成

一个 Workflow 应定义：

- workflow id；
- 适用业务；
- 输入；
- 阶段列表；
- 每个阶段调用哪个 Capability；
- 每个阶段需要哪些数据；
- 输出 Artifact；
- 是否需要人工确认；
- 失败处理；
- AuditLog；
- 下一步动作。

#### Capability 与 Workflow 的关系

Capability 是积木。  
Workflow 是搭积木的方法。  
Mo Flow 是让这套积木真正跑起来的运行时。

---

## 5. Capability 与 Skill 的关系

### 5.1 层级关系

```text
Capability Spec
  ↓
Skill Implementation
  ↓
Agent / Guide / Workflow 调用
```

### 5.2 示例：RecommendCountry

#### Capability

```yaml
id: C3101
name: RecommendCountry
description: 根据客户业务、预算、销售平台和品牌阶段推荐申请国家
input:
  - business
  - budget
  - platform
  - existing_countries
output:
  - recommended_countries
  - reason
  - confidence
  - estimated_cost
depends:
  - Mo Brain
  - Mo Data
  - Mo Intelligence
review:
  - high_value_customer
  - unusual_country_combination
```

#### Skill 实现

```text
recommend_country_rules.ts
recommend_country_gpt.ts
recommend_country_fast.ts
recommend_country_brain.ts
```

### 5.3 设计价值

这种分层有三个价值：

1. 能力定义长期稳定；
2. 技术实现可以替换；
3. Mo Guide 和 Workflow 不依赖某个具体模型或工具。

---

## 6. Mo Guide 如何调用能力

### 6.1 Guide 的角色

Mo Guide 不应该靠一个大 Prompt 完成所有事情。

它应作为编排器调用 Capability、Skill 和 Workflow。

### 6.2 调用链示例

用户说：

> 我想注册一个商标，主要做亚马逊。

Guide 可能执行：

```text
UnderstandIntent()
  ↓
ExtractBusinessInfo()
  ↓
RecommendCountry()
  ↓
RecommendClass()
  ↓
CheckFilingChecklist()
  ↓
NextBestQuestion()
  ↓
GenerateQuotation()
  ↓
GeneratePOA()
```

### 6.3 Guide 的判断点

Mo Guide 要判断：

- 用户意图是什么；
- 当前信息是否完整；
- 缺哪些信息；
- 下一句最该问什么；
- 是否能直接报价；
- 是否需要人工介入；
- 是否进入 Mo Flow；
- 是否创建订单；
- 是否生成文件；
- 是否转交服务商。

---

## 7. Mo Workflow Runtime 的启发

### 7.1 Agentic Workflow 的启发

类似 OpenMontage 的智能工作流项目对 MarkOrbit 有重要启发。

它们不是依靠一个大模型直接完成复杂任务，而是通过：

- Pipeline Manifest；
- Stage Skill；
- Tool Adapter；
- Checkpoint；
- Artifact；
- Workflow Log；

将复杂任务拆解为可执行、可审计、可复用的流水线。

### 7.2 对 MarkOrbit 的意义

MarkOrbit 未来也应从“功能系统”升级为：

> **行业智能工作流系统**

用户一句自然语言需求，不应只是进入聊天，而应进入一个可编排、可审计、可人工确认、可输出业务成果的 Workflow。

### 7.3 Mo Workflow Runtime v0

未来可定义最小运行时：

```yaml
workflow: us_trademark_filing
input:
  - customer_need
  - trademark
  - applicant
  - goods
stages:
  - understand_intent
  - extract_trademark_info
  - check_filing_checklist
  - recommend_class
  - generate_quotation
  - generate_poa
  - create_order
  - human_review
  - submit_to_provider
output:
  - quote_plan
  - filing_checklist
  - poa
  - markreg_order
```

### 7.4 Lite 1.1 的边界

Lite 1.1 不必马上做完整 Workflow Runtime。

但文档和数据模型应为以下内容预留：

- WorkflowDefinition；
- WorkflowRun；
- WorkflowStepRun；
- Artifact；
- Human Approval；
- AuditLog；
- Capability Code。

---

## 8. Mo Content、Mo Graphic 与 Mo Video

### 8.1 内容生产在 Mo 中的位置

内容生产不是简单“AI 写文案”。

它是 Mo Intelligence、Mo Brain、Mo Workspace 和 Mo Asset Hub 的共同输出。

内容生产链路：

```text
Mo Topics
  ↓
Mo Workspace
  ↓
Mo Knowledge / Mo Brain
  ↓
Mo Asset Hub
  ↓
Mo Assistant
  ↓
ContentDraft / GraphicBrief / VideoBrief
```

### 8.2 Mo Content

Mo Content 负责：

- 每日选题；
- 主题卡；
- 图文文案；
- 视频脚本；
- 私聊话术；
- 邮件文案；
- 内容草稿；
- 选用记录；
- 内容偏好学习。

### 8.3 Mo Asset Hub

Mo Asset Hub 负责：

- 平台基础素材；
- 用户私有素材；
- 商标 logo；
- 驳回文书截图；
- 新闻报道图；
- 官方截图；
- 商标局 logo；
- 国家标识；
- 流程图模板；
- 风险提示图；
- 节日底图；
- 视频片头片尾；
- 转场视频；
- 字幕条；
- 模板库。

它让 AI 内容从“会写”变成“能发”。

### 8.4 Mo Graphic

Mo Graphic 应采用：

> **AI 生成图文结构和视觉建议，模板引擎负责准确排版，图像模型只负责背景和风格素材。**

建议技术路线：

- V1.1：生成 GraphicBrief；
- V1.2：模板化图文生成；
- V1.5：接入可编辑设计器和图像生成工作流。

### 8.5 Mo Video

Mo Video 应从脚本开始，不要一开始做完整成片。

建议路线：

- V1.1：视频脚本、分镜、字幕文案；
- V1.2：模板化短视频 Worker；
- V1.5：Agentic Video Pipeline。

视频生产链路：

```text
Mo Topics
  ↓
Video Script
  ↓
Voiceover Text
  ↓
Captions
  ↓
Video Template
  ↓
Media Assets
  ↓
Render Worker
  ↓
MP4 / Cover / SRT
```

---

## 9. Lite 1.1 在 Mo 架构中的位置

### 9.1 Lite 1.1 的定位

Lite 1.1 是：

> **Mo 能力的第一个可用应用层。**

它不是完整 Mo，也不是完整 Mo Brain。

它是面向商标代理人的工作台，用来验证 Mo 能力是否能真正被用户使用。

### 9.2 Lite 1.1 实现范围

| Mo 模块 | Lite 1.1 是否实现 | V1.1 做法 |
|---|---:|---|
| Mo Data | 不完整实现 | 只做用户商标、用户素材、主题素材、报价数据引用 |
| Mo Brain | 不真实接入 | BrainConnector disabled，使用内置知识与用户知识库 |
| Mo Intelligence | 局部实现 | 简单主题推荐、素材推荐、商机跟进建议 |
| Capability Catalog | 最小实现 | 定义 Lite 可用 Capability |
| Skill Library | 最小实现 | 复用 AI Skill，新增业务 Skill |
| Workflow Catalog | 轻量预留 | 先做内容、推荐、报价、商机轻流程 |
| Mo Guide | 局部实现 | 在客户答复、报价采集、商标推荐中体现 |
| Mo Flow | 局部复用 | 复用 Markreg Order、Opportunity、MGSN 价格与服务 |
| Applications | 实现 | MarkOrbit Lite 是核心入口 |

### 9.3 Lite 1.1 不做

Lite 1.1 不做：

- 完整全球商标数据平台；
- 完整行业知识图谱；
- 完整 Mo Brain；
- 全自动 Workflow Runtime；
- 真实群发；
- 真实视频成片；
- 完整小程序；
- 平台级商标交易市场；
- 全球商标状态自动同步；
- 自动爬虫采集系统；
- 真实官方递交；
- 真实支付闭环。

### 9.4 Lite 1.1 的六个核心模块

Lite 1.1 应包含：

1. **Mo Workspace｜业务空间**  
   用户资料、Persona、Knowledge、偏好、报价规则、私有素材、上下文。

2. **Mo Content｜内容生产中心**  
   选题、素材、模板、图文、视频脚本、私聊话术、草稿。

3. **Mo Marks｜商标货架**  
   商标资产、待售商标、AI 包装、销售页、推荐页、询盘。

4. **Mo Global｜全球代理中心**  
   国家服务、报价规则、报价方案、材料清单、风险提示、转订单。

5. **Mo Leads｜商机跟进台**  
   今日跟进、批量话术、推荐页关联、报价关联、跟进记录、转订单。

6. **Mo Assistant｜业务动作助手**  
   贯穿所有模块，负责写作、答复、包装、推荐、报价、跟进。

支撑层：

- **Mo Asset Hub｜内容素材库**

预留层：

- **Mo Brain Connector**

---

## 10. Lite 1.1 的五个业务闭环

### 10.1 每日内容生产闭环

```text
Mo Workspace
  ↓
Mo Content
  ↓
Mo Topics
  ↓
Mo Asset Hub
  ↓
Mo Assistant
  ↓
ContentDraft
  ↓
复制 / 下载 / 使用记录
```

用户价值：

> 今天发什么、怎么发、配什么图，系统都帮我准备好了。

### 10.2 商标包装与推荐闭环

```text
商标资产
  ↓
Mo Marks
  ↓
AI 包装
  ↓
销售页
  ↓
推荐页
  ↓
询盘
  ↓
商机
```

用户价值：

> 我的商标可以像房源一样被展示、推荐和成交。

### 10.3 全球报价与订单闭环

```text
客户需求
  ↓
Mo Guide 局部采集
  ↓
Mo Global
  ↓
QuotePlan
  ↓
QuoteProposal
  ↓
Markreg Order
```

用户价值：

> 我能快速给客户做一份专业的海外商标报价方案。

### 10.4 商机跟进闭环

```text
Opportunity
  ↓
Mo Leads
  ↓
匹配内容 / 商标 / 报价
  ↓
批量生成话术
  ↓
跟进记录
  ↓
转报价 / 转订单
```

用户价值：

> 商机不是躺在列表里，而是变成今天该做的动作。

### 10.5 用户业务空间学习闭环

```text
用户资料
  ↓
使用行为
  ↓
主题偏好
  ↓
素材偏好
  ↓
文案偏好
  ↓
推荐越来越准
```

用户价值：

> 这个系统越用越懂我。

---

## 11. Lite 1.1 的最小 Capability Catalog

Lite 1.1 应先定义一批最小 Capability，不必全部实现为复杂代码。

### 11.1 Workspace Capabilities

1. ManageBusinessProfile  
2. ManagePersona  
3. ManageKnowledge  
4. ManageContentPreference  
5. BuildWorkspaceContext  

### 11.2 Content Capabilities

6. RecommendDailyTopics  
7. CreateCustomTopic  
8. RecommendTopicAssets  
9. GenerateGraphicBrief  
10. GenerateGraphicCopy  
11. GenerateVideoScript  
12. GeneratePrivateChatCopy  
13. RecordContentUsage  

### 11.3 Asset Capabilities

14. UploadMediaAsset  
15. ClassifyMediaAsset  
16. RecommendMediaAsset  
17. RecordAssetUsage  

### 11.4 Trademark Capabilities

18. ImportTrademarkAssets  
19. ClassifyTrademarkAsset  
20. PackageTrademarkForSale  
21. GenerateTrademarkSalesPage  
22. GenerateTrademarkRecommendationPage  
23. ConvertInquiryToOpportunity  

### 11.5 Global Quote Capabilities

24. SearchCountryService  
25. ApplyUserPriceRule  
26. GenerateQuotePlan  
27. GenerateQuoteProposal  
28. ConvertQuoteToOrder  

### 11.6 Leads Capabilities

29. GenerateLeadFollowup  
30. RecordCommunication  
31. ConvertLeadToQuote  
32. ConvertLeadToOrder  

---

## 12. Mo 的完整架构图

```text
                         MarkOrbit Universe
              全球商标数字基础设施 / Trademark Digital OS
               品牌方｜代理机构｜律师｜开发者｜AI Agent
                                   │
                                   ▼
────────────────────────────────────────────────────────────
                    Applications 应用层
────────────────────────────────────────────────────────────
 MarkOrbit Lite ｜ MarkReg ｜ 官网 ｜ 小程序 ｜ API ｜ SDK ｜ MCP ｜ 第三方系统
────────────────────────────────────────────────────────────
                    Mo Guide 统一智能入口
────────────────────────────────────────────────────────────
 Intent ｜ State ｜ Checklist ｜ Next Best Question ｜ Recommendation ｜ Review
────────────────────────────────────────────────────────────
                    Workflow Catalog 业务编排目录
────────────────────────────────────────────────────────────
 Filing Workflow ｜ Renewal Workflow ｜ OA Workflow ｜ Trading Workflow ｜ Content Workflow
────────────────────────────────────────────────────────────
                    Capability Catalog 行业能力目录
────────────────────────────────────────────────────────────
 RecommendCountry ｜ GeneratePOA ｜ FindOpportunity ｜ ExplainOA ｜ GenerateContent
────────────────────────────────────────────────────────────
                    Skill Library 能力实现层
────────────────────────────────────────────────────────────
 rules skill ｜ gpt skill ｜ fast skill ｜ local model skill ｜ tool skill ｜ worker skill
────────────────────────────────────────────────────────────
                    Mo Flow 业务执行平台
────────────────────────────────────────────────────────────
 Order ｜ Payment ｜ Attorney ｜ Approval ｜ Submission ｜ Delivery ｜ Task ｜ Notice
────────────────────────────────────────────────────────────
                    Mo Intelligence 洞察增长平台
────────────────────────────────────────────────────────────
 Opportunity ｜ Prediction ｜ Marketing ｜ Growth ｜ Risk ｜ Matching ｜ Scoring
────────────────────────────────────────────────────────────
                    Mo Brain 知识规则平台
────────────────────────────────────────────────────────────
 Raw ｜ Wiki ｜ Rules ｜ Decision ｜ SOP ｜ FAQ ｜ Content Library ｜ Best Practice
────────────────────────────────────────────────────────────
                    Mo Data 数据平台
────────────────────────────────────────────────────────────
 Trademark Data ｜ Cases ｜ Laws ｜ Entities ｜ Agents ｜ Applicants ｜ Graph ｜ Events
────────────────────────────────────────────────────────────
                    Infrastructure 基础设施
────────────────────────────────────────────────────────────
 Sync ｜ Entity Graph ｜ Search ｜ Vector ｜ OCR ｜ Translation ｜ Event Bus ｜ Storage
```

---

## 13. 最重要的产品原则

以后所有 MarkOrbit 功能都必须先回答四个问题：

1. **它涉及哪个 Entity？**
2. **它依赖哪些 Knowledge？**
3. **它属于哪个 Capability？**
4. **它被哪个 Workflow 调用？**

这样系统就不会乱。

例如：

“AI 帮客户申请美国商标”不是一个功能，而是：

### Entities

- 客户；
- 商标；
- 申请人；
- 国家；
- 商品；
- 订单；
- 文件。

### Knowledge

- 美国申请规则；
- 类别规则；
- POA 要求；
- 费用规则；
- 使用证据规则。

### Capabilities

- UnderstandIntent；
- RecommendCountry；
- RecommendClass；
- CheckChecklist；
- GeneratePOA；
- GenerateQuotation；
- CreateOrder。

### Workflow

- US Trademark Filing Workflow。

---

## 14. 当前落地建议

### 14.1 第一阶段：先做 MarkOrbit Lite

第一阶段不要同时做全部 Mo。

应先做 MarkOrbit Lite，因为第一波目标客户是代理人。

Lite 1.1 重点是：

- 今日工作台；
- Mo Workspace；
- Mo Content；
- Mo Asset Hub；
- Mo Assistant；
- Mo Marks；
- Mo Global；
- Mo Leads。

### 14.2 同时建设最小 Mo Brain

但 Mo Brain 不进入 Lite 1.1 主开发。

可以在另一套系统中先覆盖：

- 美国申请；
- 美国 Section 8；
- 商标购买需求采集；
- 基础国家知识；
- 基础 POA 规则；
- 基础报价规则；
- 基础内容知识；
- 基础案例知识。

### 14.3 同时建设最小 Capability Catalog

先定义 30 个核心能力，而不是 300 个。

优先定义：

- UnderstandIntent；
- ExtractApplicant；
- ExtractGoods；
- CheckFilingChecklist；
- RecommendCountry；
- RecommendClass；
- GenerateQuotation；
- GeneratePOA；
- CreateOrder；
- GenerateEmail；
- FindRenewalOpportunity；
- RecommendDailyTopics；
- GenerateGraphicCopy；
- GenerateVideoScript；
- PackageTrademarkForSale；
- GenerateLeadFollowup。

### 14.4 同时建设最小 Workflow

先做 4 个轻闭环：

1. 内容生产 Workflow；
2. 商标推荐 Workflow；
3. 全球报价 Workflow；
4. 商机跟进 Workflow。

后续再做：

1. 美国商标申请 Workflow；
2. 美国 Section 8 宣誓 Workflow；
3. 在售商标购买需求采集 Workflow；
4. OA 答复 Workflow。

---

## 15. 路线图

### 15.1 Lite 1.1

目标：

> Mo 能力的第一个可用应用层。

重点：

- Mo Workspace；
- 今日工作台；
- Mo Content Foundation；
- Mo Asset Hub 最小版；
- Mo Assistant；
- Mo Marks；
- Mo Global；
- Mo Leads；
- BrainConnector disabled。

### 15.2 Lite 1.2

目标：

> 接入更多内容生产和轻工作流能力。

重点：

- 模板化图文生成；
- Mo Graphic Worker；
- Mo Video Worker 原型；
- Workflow Lite Runtime；
- 更多报价方案；
- 更多推荐页能力；
- 初步接入 Mo Brain 只读能力。

### 15.3 Lite 1.5

目标：

> Mo Brain 与 Lite 深度连接。

重点：

- Mo Brain 正式只读接入；
- 热点主题；
- 官方案例；
- 行业知识增强；
- 更强商机推荐；
- 视频生成流水线；
- 自动营销建议；
- 小程序基础能力。

### 15.4 V2

目标：

> MarkOrbit 成为多应用、多入口、多 Agent 的行业操作系统。

重点：

- Mo Data 扩展；
- Entity Graph；
- Mo Intelligence；
- 完整 Mo Guide；
- 完整 Mo Flow；
- Workflow Runtime；
- API / SDK / MCP；
- 平台级交易与代理网络。

---

## 16. 一句话总结

Mo 架构的本质，是用 Data 连接商标世界，用 Brain 理解商标世界，用 Intelligence 发现商业价值，用 Capability 定义行业能力，用 Skills 实现能力，用 Workflows 编排业务，用 Guide 与用户沟通，用 Flow 完成业务，最后通过 Lite、官网、小程序、API 等应用交付给不同用户。

最终目标是：

> **让全球商标行业的数据、知识、服务、交易、内容和业务流程，都能被 AI 理解、编排和执行。**
