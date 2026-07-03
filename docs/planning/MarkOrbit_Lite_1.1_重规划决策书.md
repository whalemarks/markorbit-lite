# MarkOrbit Lite 1.1 重规划决策书

版本：Draft 1.0  
关联文档：`Mo Architecture｜MarkOrbit 核心架构白皮书`  
定位：Lite 1.1 是 Mo 能力的第一个可用应用层  
开发原则：先落地代理人可用闭环，再逐步接入 Mo Brain / Mo Intelligence / Mo Flow  
Mo Brain 状态：Lite 1.1 仅预留接口，不做真实接入

---

## 0. 执行摘要

MarkOrbit Lite 1.1 需要重新规划。

此前 V1.1 的规划重点是“Mo Workspace 独立可用版”，方向正确，但在 Mo 总架构进一步明确后，Lite 1.1 不能只是一个独立 SaaS 改版，而应成为：

> **Mo 能力的第一个可用应用层。**

Lite 1.1 的核心任务，不是实现完整 Mo，也不是建设完整 Mo Brain，而是让第一批商标代理人每天能真实使用 MarkOrbit 完成：

- 今天发什么内容；
- 用什么素材和模板；
- 推什么商标；
- 跟进哪些客户；
- 生成什么报价；
- 转化什么订单。

因此，Lite 1.1 的产品定位调整为：

> **以 Mo Workspace 为底座，以 Mo Content 为日活入口，以 Mo Marks / Mo Global / Mo Leads 为成交场景，以 Mo Asset Hub 为内容生产支撑，以 Mo Assistant 为业务动作引擎的代理人工作台。**

一句用户价值表达：

> **每天有内容可发，有商标可推，有客户可跟，有报价可出，有订单可转。**

---

## 1. 重规划背景

### 1.1 V1.0 已完成的基础

MarkOrbit V1.0 已完成 Phase 0-10，并合并 main。

已有能力包括：

- 用户、权限、会员、Token；
- AI Skill Service；
- Lite AI 助理；
- 商标资产库；
- AI 标签 / AI 包装；
- Partner Center；
- Opportunity；
- Markreg 轻量订单入口；
- MGSN 内部供应链；
- Admin 总后台；
- Release readiness。

V1.0 的主要价值是：

> 底层业务模型、权限、数据结构、后台管理和关键链路已经具备。

### 1.2 V1.0 的问题

V1.0 的 Lite 端仍然存在以下问题：

1. 更像功能菜单，不像业务工作台；
2. AI 助理像普通 AI 表单，缺少 MarkOrbit 独有价值；
3. 商标资产库没有形成“包装、展示、推荐、询盘”的闭环；
4. 商机中心偏静态，没有变成行动台；
5. 全球报价能力没有变成报价方案；
6. 内容营销只有文字思路，缺素材、模板和发布半成品；
7. 用户打开系统后，不知道今天该做什么。

### 1.3 Mo 架构对 Lite 1.1 的影响

Mo 的长期架构已经明确：

```text
Mo Data → Mo Brain → Mo Intelligence → Capability → Skill → Workflow → Mo Guide → Mo Flow → Applications
```

Lite 是 Applications 层，但它不能脱离 Mo 架构单独生长。

因此 Lite 1.1 必须做到：

- 不实现完整 Mo；
- 但按 Mo 架构预留能力；
- 不接完整 Mo Brain；
- 但预留 BrainConnector；
- 不做完整 Workflow Runtime；
- 但按 Capability / Workflow 的思想设计业务动作；
- 不只做 AI 文案；
- 而要做“内容 + 素材 + 模板 + 商标 + 报价 + 商机”的可用闭环。

---

## 2. Lite 1.1 新定位

### 2.1 原定位

此前 Lite 1.1 的定位是：

> Mo Workspace 独立可用版。

这个定位仍然成立，但不够完整。

### 2.2 新定位

MarkOrbit Lite 1.1 的新定位是：

> **商标代理人的 Mo 工作台。**

更完整表达：

> **MarkOrbit Lite 1.1 是商标代理人使用 Mo 能力的第一个工作台，帮助代理人基于自己的业务空间，完成内容生产、商标推荐、报价方案、商机跟进和订单转化。**

### 2.3 产品口号

面向用户可以表达为：

> **每天有内容可发，有商标可推，有客户可跟，有报价可出，有订单可转。**

面向内部架构可以表达为：

> **Lite 1.1 是 Mo Workspace + Mo Content + Mo Asset Hub + Mo Marks + Mo Global + Mo Leads + Mo Assistant 的代理人工作台。**

---

## 3. Lite 1.1 与完整 Mo 的边界

Lite 1.1 不能试图实现完整 Mo。它只实现 Mo 的应用层、用户私有空间和少量可运行能力。

### 3.1 Lite 1.1 实现什么

| Mo 模块 | Lite 1.1 是否实现 | V1.1 做法 |
|---|---:|---|
| Mo Data | 不完整实现 | 只做用户商标、用户素材、主题素材、报价数据引用 |
| Mo Brain | 不真实接入 | BrainConnector disabled，使用内置知识与用户知识库 |
| Mo Intelligence | 局部实现 | 简单主题推荐、素材推荐、商机跟进建议、商标推荐建议 |
| Capability Catalog | 最小实现 | 定义 20-30 个 Lite 可用 Capability |
| Skill Library | 最小实现 | 复用 AI Skill，新增业务 Skill |
| Workflow Catalog | 轻量预留 | 先做内容、推荐、报价、商机 4 个轻流程 |
| Mo Guide | 局部实现 | 在客户答复、报价采集、商标推荐中体现 |
| Mo Flow | 局部复用 | 复用 Markreg Order、Opportunity、MGSN 价格与服务 |
| Applications | 实现 | MarkOrbit Lite 是核心入口 |

### 3.2 Lite 1.1 不做什么

Lite 1.1 不做：

1. 不做完整全球商标数据平台；
2. 不做完整行业知识图谱；
3. 不做完整 Mo Brain；
4. 不做 Mo Brain 真实接入；
5. 不做全自动 Workflow Runtime；
6. 不做真实邮件 / 短信 / 微信 / 企业微信群发；
7. 不做真实视频成片；
8. 不做完整小程序；
9. 不做平台级商标交易市场；
10. 不做全球商标状态自动同步；
11. 不做自动爬虫采集系统；
12. 不做真实支付；
13. 不做真实官方递交；
14. 不做复杂资金托管；
15. 不做完整服务商 marketplace。

### 3.3 数据边界

Lite 1.1 必须坚持：

- 用户 Workspace 默认私有；
- 用户素材默认私有；
- 用户商标资产默认私有；
- 用户报价规则默认私有；
- 用户商机默认私有；
- 用户内容偏好默认私有；
- 未授权不进入 Mo Brain；
- 未授权不进入平台公共池；
- 未授权不进入平台交易市场。

---

## 4. Lite 1.1 总体架构

Lite 1.1 由六个核心模块、一个支撑层、一个预留层组成。

```text
Mo Workspace
    ↓
今日工作台
    ↓
Mo Content ── Mo Asset Hub
    ↓
Mo Assistant
    ↓
Mo Marks / Mo Global / Mo Leads
    ↓
Markreg Order / Opportunity / Recommendation / Quote
```

---

## 5. 六个核心模块

### 5.1 Mo Workspace｜业务空间

回答的问题：

> 我是谁？我服务谁？我有什么资料？AI 如何像我一样工作？

Mo Workspace 是 Lite 1.1 的地基。它保存每个用户自己的业务资料、表达风格、知识资料、报价规则、素材、商标资产、商机上下文和行为偏好。

包含内容：

- 用户业务资料；
- Mo Persona；
- Mo Knowledge；
- 内容偏好；
- 报价规则；
- 用户私有素材；
- 用户商标资产摘要；
- 用户商机摘要；
- BrainConnection disabled 状态。

V1.1 目标：

> 让 AI 后续生成内容、回复客户、推荐商标、生成报价和跟进商机时，能优先参考用户自己的业务空间，而不是像普通 AI 一样泛泛回答。

---

### 5.2 Mo Content｜内容生产中心

回答的问题：

> 今天发什么？怎么写？用什么图？能不能直接发？

Mo Content 是 Lite 1.1 的日活入口。

它不只是 Mo Topics，而是“选题 + 素材 + 模板 + 文案 + 视频脚本 + 草稿”的内容生产系统。

包含内容：

- Mo Topics：每日选题；
- Content Theme：结构化主题卡；
- Content Draft：内容草稿；
- Graphic Brief：图文蓝图；
- Video Brief：视频脚本 / 分镜 / 字幕预留；
- 私聊话术；
- 邮件文案；
- 内容使用记录；
- 内容偏好学习。

V1.1 目标：

> 让代理人每天打开系统后，第一眼就知道今天可以发什么、适合发给谁、用什么素材、生成什么格式、如何复制使用。

---

### 5.3 Mo Asset Hub｜内容素材支撑层

回答的问题：

> 生成内容时，我能用哪些图片、截图、模板、logo、流程图、视频素材？

Mo Asset Hub 是 Lite 1.1 必须新增的内容生产支撑层。它让系统从“会写”升级为“能发”。

平台基础素材包括：

- 商标局 logo；
- 国家 / 地区标识；
- 基础流程图；
- 风险提示图；
- FAQ 卡片；
- 节日底图；
- 商标服务图标；
- 类别图标；
- 小红书 / 朋友圈 / 视频封面模板。

用户私有素材包括：

- 商标 logo；
- 驳回文书截图；
- 商标公告截图；
- 客户授权图；
- 产品图；
- 公司介绍图；
- 个人形象图；
- 新闻事件截图；
- 用户上传的其他图片。

视频素材预留包括：

- 片头；
- 片尾；
- 转场视频；
- 背景动效；
- 字幕条；
- CTA 片尾；
- 商标局动态标识。

V1.1 目标：

- 平台基础素材；
- 用户上传素材；
- 素材分类；
- 素材标签；
- 主题关联素材；
- 素材使用记录。

V1.1 不做复杂 DAM，不做版权自动判断，不做视频成片。

---

### 5.4 Mo Marks｜商标货架

回答的问题：

> 我有哪些商标可以管理、包装、推荐和销售？

Mo Marks 不是普通资产数据库，而是商标“货架”。它要让商标像房源一样被包装、展示、推荐和产生询盘。

包含内容：

- 自有商标；
- 客户商标；
- 待售商标；
- 平台代售预留；
- AI 标签；
- AI 包装；
- 单商标销售页；
- 多商标推荐页；
- 商标询盘；
- 询盘转商机。

V1.1 目标：

> 完成“导入 / 创建商标 → 标记待售 → AI 包装 → 销售页 → 推荐页 → 询盘 → 商机”的最小闭环。

---

### 5.5 Mo Global｜全球代理中心

回答的问题：

> 这个客户要申请哪些国家？多少钱？怎么给客户报价？

Mo Global 不是价格表，而是报价方案生成器。

包含内容：

- 国家服务；
- 平台价格；
- 用户报价规则；
- 多国家报价方案；
- 客户报价说明；
- 材料清单；
- 周期说明；
- 风险提示；
- 报价方案分享页；
- 转 Markreg 订单。

V1.1 目标：

> 让代理人能快速给客户生成一份专业的海外商标报价方案。

---

### 5.6 Mo Leads｜商机跟进台

回答的问题：

> 今天该跟进谁？怎么跟进？推商标还是推服务？能不能转订单？

Mo Leads 不是静态商机列表，而是商机跟进工作台。

包含内容：

- 今日待跟进；
- 高意向商机；
- 已推荐商标商机；
- 已报价商机；
- 批量微信话术；
- 批量邮件文案；
- 批量短信草稿；
- 推荐页关联；
- 报价方案关联；
- 跟进记录；
- 转报价；
- 转订单。

V1.1 目标：

> 让商机从“列表数据”变成“今日动作”。

V1.1 不做真实群发，只做草稿、复制、导出、标记已发送、跟进记录。

---

### 5.7 Mo Assistant｜业务动作助手

回答的问题：

> 用户要做某件事时，AI 如何调用 Workspace、Content、Marks、Global、Leads 来完成？

Mo Assistant 不再是单独的“AI 工具页”，而是所有场景的动作层。

包含动作：

- 写图文；
- 写视频脚本；
- 写私聊话术；
- 回复客户问题；
- 包装商标；
- 生成推荐理由；
- 生成报价说明；
- 生成商机跟进；
- 生成邮件；
- 生成短信草稿；
- 生成 FAQ；
- 生成风险提示。

V1.1 目标：

> Mo Assistant 贯穿所有模块，而不是孤立页面。

---

## 6. 五个业务闭环

### 6.1 每日内容生产闭环

路径：

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

用户动作：

1. 打开今日工作台；
2. 查看今日推荐主题；
3. 选择一个主题；
4. 系统推荐素材和模板；
5. 生成图文文案、视频脚本、私聊话术；
6. 用户复制或保存；
7. 系统记录偏好。

用户价值：

> 今天发什么、怎么发、配什么图，系统都帮我准备好了。

V1.1 最小交付：

- 主题推荐；
- 主题卡；
- 主题素材推荐；
- 图文文案；
- 视频脚本；
- 私聊话术；
- 内容草稿；
- 选用记录；
- 素材使用记录。

V1.1 不做：

- 真实图片渲染成品；
- 真实视频成片；
- 自动发布。

---

### 6.2 商标包装与推荐闭环

路径：

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

用户动作：

1. 导入或创建商标；
2. 标记为待售；
3. AI 生成包装；
4. 系统生成销售页；
5. 选择多个商标生成推荐页；
6. 分享给客户；
7. 客户询盘；
8. 进入商机中心。

用户价值：

> 我的商标可以像房源一样被展示、推荐和成交。

V1.1 最小交付：

- 商标分类；
- 待售商标；
- AI 包装；
- 单商标销售页；
- 多商标推荐页；
- 询盘转商机。

---

### 6.3 全球报价与订单闭环

路径：

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

用户动作：

1. 输入客户需求；
2. 系统判断缺什么信息；
3. 推荐国家或让用户选择国家；
4. 读取平台价格；
5. 应用用户报价规则；
6. 生成客户报价方案；
7. 转 Markreg 订单。

用户价值：

> 我能快速给客户做一份专业的海外商标报价方案。

V1.1 最小交付：

- 国家价格查询；
- 用户报价规则；
- 报价方案；
- 客户版说明；
- 转订单。

---

### 6.4 商机跟进闭环

路径：

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

用户动作：

1. 查看今日待跟进；
2. 批量选择商机；
3. 选择跟进目标；
4. 生成微信 / 邮件 / 短信草稿；
5. 关联推荐页或报价方案；
6. 标记已跟进；
7. 推进状态。

用户价值：

> 商机不是躺在列表里，而是变成今天该做的动作。

V1.1 最小交付：

- 今日待跟进；
- 批量生成话术；
- 关联推荐页；
- 关联报价；
- 记录跟进；
- 转订单。

---

### 6.5 用户业务空间持续学习闭环

路径：

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

系统记录：

- 用户选择了什么主题；
- 用户喜欢什么风格；
- 用户用了什么素材；
- 哪些内容被复制；
- 哪类商标被推荐；
- 哪类商机推进成功；
- 哪类报价方案被使用。

用户价值：

> 这个系统越用越懂我。

V1.1 最小交付：

- 用户内容偏好；
- 主题使用记录；
- 素材使用记录；
- 内容草稿记录；
- Workspace 完整度。

---

## 7. 今日工作台设计原则

Lite 首页应重新设计为“5 个今日”。

### 7.1 今日发什么

来自 Mo Content：

- 今日推荐主题；
- 推荐素材；
- 生成图文；
- 生成视频脚本；
- 生成私聊话术。

### 7.2 今日推什么

来自 Mo Marks：

- 可推广商标；
- 待包装商标；
- 推荐页待完善；
- 新询盘。

### 7.3 今日跟谁

来自 Mo Leads：

- 待跟进商机；
- 已报价未回复；
- 已推荐商标未回复；
- 高意向商机。

### 7.4 今日报什么

来自 Mo Global：

- 可生成报价；
- 最近报价方案；
- 待转订单报价。

### 7.5 今日完善什么

来自 Mo Workspace：

- 业务资料完整度；
- Persona 完整度；
- Knowledge 完整度；
- 素材库完整度。

---

## 8. 新 Sprint 规划

### Sprint 0：Mo Workspace + 今日工作台

目标：

> 让 Lite 首页变成“每天做什么”的行动台，并建立用户业务空间。

交付：

- `/lite/dashboard` 今日工作台；
- `/lite/workspace`；
- 用户业务资料；
- Mo Persona；
- Mo Knowledge；
- 内容偏好；
- BrainConnection disabled；
- Lite 导航产品化；
- Workspace 完整度；
- 今日行动卡片占位；
- Mo Content / Mo Asset Hub 入口预留。

不做：

- 真实 Mo Topics；
- 素材库；
- 图文生成；
- 商标销售页；
- 报价方案；
- 商机批量营销。

---

### Sprint 1：Mo Content Foundation｜选题 + 素材 + 草稿

目标：

> 让用户每天看到主题、素材和内容动作，而不仅是选题标题。

交付：

#### 1. Mo Topics

- 内置常青主题；
- 节假日主题；
- 商标冷知识；
- 指南类主题；
- 朋友圈观点类主题；
- 用户自建主题；
- 每日推荐；
- 主题卡；
- 主题使用记录。

#### 2. Mo Asset Hub 最小版

- 平台基础素材；
- 用户上传素材；
- 素材分类；
- 素材标签；
- 主题关联素材；
- 素材使用记录。

#### 3. ContentDraft 结构化

ContentDraft 不只保存纯文本，还要保存：

- title；
- platform；
- outputType；
- headline；
- subheadline；
- bulletPoints；
- cta；
- visualStyle；
- imagePrompt；
- templateType；
- recommendedAssetIds；
- scenePlan；
- captionText；
- legalDisclaimer；
- contactBlock。

#### 4. 主题详情页

主题详情页应显示：

- 主题说明；
- 推荐理由；
- 适用对象；
- 适用平台；
- 推荐素材；
- 推荐模板；
- 生成图文按钮；
- 生成视频脚本按钮；
- 生成私聊话术按钮。

---

### Sprint 2：Mo Assistant 业务动作

目标：

> 让 AI 从普通输入框升级为场景动作。

交付：

- 主题生成图文；
- 主题生成视频脚本；
- 主题生成私聊话术；
- 客户问题互动式答复；
- 追问 1-3 个问题；
- 专业分析；
- 风险提示；
- 成交引导；
- 文案评分；
- FAQ 侧边栏；
- 保存 ContentDraft；
- 关联素材；
- 关联主题。

---

### Sprint 3：Mo Marks 基础｜资产导入与商标分类

目标：

> 让用户快速把商标放入系统，并区分用途。

交付：

- CSV / Excel 导入；
- 粘贴导入；
- 批量输入；
- 导入预览；
- 错误行提示；
- 自有商标；
- 客户商标；
- 待售商标；
- 平台代售预留；
- 商标 logo / 图片关联到素材库；
- TrademarkDataProvider 预留。

关键要求：

> 用户上传的商标 logo 应同时进入 Mo Asset Hub，成为可用于图文、销售页、推荐页的素材。

---

### Sprint 4：Mo Marks 销售页与推荐页

目标：

> 让商标像房源一样展示和推荐。

交付：

#### 1. 单商标销售页

- 商标基础信息；
- logo；
- AI 卖点；
- 推荐行业；
- 推荐客户画像；
- 品牌故事；
- 交易说明；
- 风险提示；
- 咨询入口；
- 分享链接。

#### 2. 多商标推荐页基础版

- 选择多个商标；
- AI 推荐理由；
- 推荐页说明；
- 分享链接；
- 询盘表单；
- 询盘转商机。

---

### Sprint 5：Mo Global 全球报价中心

目标：

> 把国家价格表升级成客户报价方案。

交付：

- 国家服务查询；
- 平台价格；
- 用户报价规则；
- 多国家报价方案；
- 客户版报价文案；
- 材料清单；
- 周期说明；
- 风险提示；
- 报价方案分享页；
- 转 Markreg 订单。

优先原因：

> 现有 400 家代理伙伴最容易用起来的是报价，因此 Mo Global 应比 Mo Leads 更早进入可用状态。

---

### Sprint 6：Mo Leads 商机跟进台

目标：

> 让商机变成每天的营销动作。

交付：

- 今日待跟进；
- 高意向商机；
- 已推荐商标；
- 已报价；
- 批量生成微信话术；
- 批量生成邮件文案；
- 批量生成短信草稿；
- 关联推荐页；
- 关联报价方案；
- 跟进记录；
- 转订单。

不做：

- 真实邮件发送；
- 真实短信发送；
- 真实微信 / 企业微信发送。

---

### Sprint 7：Mo Workflow Lite Runtime 最小版

目标：

> 把内容生产、商标推荐、报价、商机跟进抽象成可记录的轻工作流。

交付：

- WorkflowDefinition 最小模型；
- WorkflowRun 最小模型；
- WorkflowStepRun 最小模型；
- 支持 4 个内置 workflow：
  - `content_marketing_workflow`
  - `trademark_recommendation_workflow`
  - `quote_plan_workflow`
  - `lead_followup_workflow`
- 记录每次用户从主题到内容、从推荐页到询盘、从报价到订单的步骤。

说明：

> 该 Sprint 可作为 Lite 1.1 后段或 Lite 1.2 前置，不强制放在 V1.1 前半段。

---

## 9. 页面结构规划

Lite 左侧导航建议调整为：

1. 今日工作台；
2. Mo Workspace；
3. Mo Content；
   - 今日选题；
   - 内容草稿；
   - 素材库；
   - 模板库；
4. Mo Assistant；
   - 写图文；
   - 写视频脚本；
   - 回客户；
5. Mo Marks；
   - 商标资产；
   - 待售商标；
   - 推荐页；
   - 询盘；
6. Mo Global；
   - 国家服务；
   - 报价规则；
   - 报价方案；
7. Mo Leads；
   - 今日跟进；
   - 商机列表；
   - 营销草稿；
8. 订单中心；
9. Partner Center；
10. Token 中心；
11. 设置。

兼容要求：

- `/lite/assets` 可以继续存在，但产品名逐步迁移到 Mo Marks；
- `/lite/opportunities` 可以逐步迁移到 Mo Leads；
- `/lite/ai` 可以逐步升级为 Mo Assistant；
- 不要一次删除旧路由；
- 先做重定向或兼容入口。

---

## 10. 数据模型调整方向

此前 V1.1 数据模型需要新增三类能力。

### 10.1 Mo Asset Hub 模型

#### MediaAsset

用于平台和用户素材。

核心字段：

- id；
- ownerUserId；
- organizationId；
- title；
- assetType；
- mediaCategory；
- sourceType；
- fileUrl；
- thumbnailUrl；
- previewUrl；
- description；
- tags；
- jurisdiction；
- language；
- relatedScenario；
- visibility；
- rightsNote；
- sourceUrl；
- sourceName；
- status；
- metadata；
- createdAt；
- updatedAt。

#### TemplateAsset

用于模板。

核心字段：

- id；
- ownerUserId；
- templateType；
- title；
- configJson；
- styleTags；
- colorTheme；
- editableFields；
- outputRatio；
- isBuiltIn；
- status；
- createdAt；
- updatedAt。

#### TopicAssetMapping

主题与素材关联。

核心字段：

- themeId；
- assetId；
- usageType；
- priority；
- metadata。

#### AssetUsageLog

素材使用记录。

核心字段：

- userId；
- assetId；
- module；
- objectType；
- objectId；
- action；
- createdAt。

---

### 10.2 ContentDraft 结构升级

ContentDraft 不应只保存 `content` 字段。

应支持：

- outputType；
- platform；
- headline；
- subheadline；
- mainCopy；
- bulletPoints；
- cta；
- graphicBrief；
- videoBrief；
- scenePlan；
- captionText；
- recommendedAssetIds；
- templateType；
- visualStyle；
- legalDisclaimer；
- contactBlock；
- aiSkillRunId；
- status。

这样 Lite 1.2 做图文和视频时不用重构。

---

### 10.3 Workflow Lite Runtime 预留模型

不一定 Sprint 0 建表，但架构要写入。

#### WorkflowDefinition

核心字段：

- id；
- code；
- name；
- description；
- triggerType；
- definitionJson；
- status。

#### WorkflowRun

核心字段：

- id；
- workflowDefinitionId；
- userId；
- objectType；
- objectId；
- status；
- startedAt；
- completedAt；
- metadata。

#### WorkflowStepRun

核心字段：

- id；
- workflowRunId；
- stepCode；
- capabilityCode；
- status；
- inputJson；
- outputJson；
- errorMessage；
- startedAt；
- completedAt。

这是未来 Mo Flow 的种子。

---

## 11. Lite 1.1 最小 Capability Catalog

Lite 1.1 应定义第一批 Lite Capability，而不是直接写散乱功能。

### A. Workspace Capabilities

1. ManageBusinessProfile  
2. ManagePersona  
3. ManageKnowledge  
4. ManageContentPreference  
5. BuildWorkspaceContext  

### B. Content Capabilities

6. RecommendDailyTopics  
7. CreateCustomTopic  
8. RecommendTopicAssets  
9. GenerateGraphicBrief  
10. GenerateGraphicCopy  
11. GenerateVideoScript  
12. GeneratePrivateChatCopy  
13. RecordContentUsage  

### C. Asset Capabilities

14. UploadMediaAsset  
15. ClassifyMediaAsset  
16. RecommendMediaAsset  
17. RecordAssetUsage  

### D. Trademark Capabilities

18. ImportTrademarkAssets  
19. ClassifyTrademarkAsset  
20. PackageTrademarkForSale  
21. GenerateTrademarkSalesPage  
22. GenerateTrademarkRecommendationPage  
23. ConvertInquiryToOpportunity  

### E. Global Quote Capabilities

24. SearchCountryService  
25. ApplyUserPriceRule  
26. GenerateQuotePlan  
27. GenerateQuoteProposal  
28. ConvertQuoteToOrder  

### F. Leads Capabilities

29. GenerateLeadFollowup  
30. RecordCommunication  
31. ConvertLeadToQuote  
32. ConvertLeadToOrder  

V1.1 不要求全部做成复杂独立代码模块，但文档、目录、Skill 命名、AI run 记录应尽量按 Capability 管理。

---

## 12. 技术开发原则

### 12.1 保持 V1.0 兼容

不得破坏 V1.0 已完成能力：

- 用户权限；
- 会员与 Token；
- AI Skill Run；
- 用户记忆；
- 商标资产；
- AI 标签 / AI 包装；
- Partner Center；
- Referral；
- Commission；
- Opportunity；
- Markreg Order；
- MGSN CaseAssignment；
- Admin 总后台；
- AuditLog；
- Local-ready placeholder。

### 12.2 不修改历史 migration

禁止修改：

- Phase 8 migration；
- Phase 9 migration；
- 任何已合并 main 的 migration。

如需 schema 变更，只能新增当前 Sprint migration。

### 12.3 不创建平行系统

禁止创建：

- duplicate users；
- duplicate customers；
- duplicate orders；
- duplicate opportunities；
- duplicate commissions；
- markreg_orders；
- mgsn_orders；
- lead_v2；
- asset_v2。

### 12.4 AI 生成必须可记录

所有 AI 生成应记录：

- AISkillRun；
- TokenLog；
- ContentDraft / MessageDraft / QuoteProposal 等业务结果；
- AuditLog。

### 12.5 用户数据默认私有

默认不共享、不公开、不上传到 Mo Brain。

### 12.6 真实发送后置

V1.1 不做真实群发，只做：

- 草稿；
- 复制；
- 导出；
- 标记已发送。

---

## 13. 商业化判断

Lite 1.1 的商业化不应只是卖 Token。

应围绕代理人的业务结果收费：

### 免费版

- 少量今日选题；
- 基础内容草稿；
- 少量素材上传；
- 少量商标资产；
- 基础报价查看。

### 单项付费

- 月度营销计划；
- 批量图文草稿；
- 批量视频脚本；
- 商标销售页；
- 多商标推荐页；
- 全球报价方案；
- 批量商机跟进草稿。

### 套餐升级

- 更多主题；
- 更多 AI 生成次数；
- 更多素材容量；
- 更多商标资产；
- 更多推荐页；
- 更多报价方案；
- 更多商机处理；
- 更高级 Persona；
- 更高级 Knowledge；
- 未来 Mo Brain 增强。

核心售卖点：

> 更高效获客、更专业推荐、更快报价、更好成交。

---

## 14. 成功标准

Lite 1.1 是否成功，不看页面数量，而看用户是否愿意每天使用。

### 产品指标

1. 用户每日打开率；
2. 今日主题点击率；
3. 主题选用率；
4. 素材使用率；
5. 内容生成次数；
6. 内容复制次数；
7. 商标销售页生成数量；
8. 推荐页生成数量；
9. 询盘数量；
10. 报价方案生成数量；
11. 商机跟进内容生成数量；
12. 商机转订单数量；
13. Markreg 订单转化数量。

### 体验指标

用户应能清楚感受到：

- 今天发什么；
- 用什么图；
- 推什么商标；
- 给谁报价；
- 跟进谁；
- 下一步做什么。

---

## 15. 对旧 V1.1 规划的处理

### 15.1 保留内容

保留：

- Mo Workspace；
- 今日行动台；
- Mo Persona；
- Mo Knowledge；
- BrainConnection disabled；
- Mo Topics；
- Mo Assistant；
- Mo Marks；
- Mo Global；
- Mo Leads；
- 商标销售页；
- 多商标推荐页；
- 报价方案；
- 商机批量跟进。

### 15.2 调整内容

调整：

- Mo Topics 升级为 Mo Content Foundation；
- 新增 Mo Asset Hub；
- ContentDraft 从纯文本升级为结构化内容草稿；
- 首页从行动卡片升级为“5 个今日”；
- Sprint 顺序调整为：
  1. Workspace + 今日工作台；
  2. Content Foundation；
  3. Assistant 业务动作；
  4. Marks 基础；
  5. Marks 销售页与推荐页；
  6. Global 报价；
  7. Leads 跟进；
  8. Workflow Lite Runtime。

### 15.3 暂停内容

暂停：

- 继续按旧 Sprint 1 做单纯选题系统；
- 直接开发视频生成成片；
- 直接接 OpenMontage 类系统；
- 直接接真实素材爬取；
- 直接接 Mo Brain；
- 直接做小程序。

---

## 16. 最终决策

MarkOrbit Lite 1.1 正式重规划为：

> **Mo 能力的第一个可用应用层。**

其核心结构为：

> **Mo Workspace 为底座，Mo Content 为日活入口，Mo Asset Hub 为内容支撑，Mo Assistant 为动作引擎，Mo Marks / Mo Global / Mo Leads 为成交场景。**

最终目标不是“更多功能”，而是：

> **让商标代理人每天打开 Lite，就能生产内容、使用素材、包装商标、推荐客户、生成报价、跟进商机、推进订单。**

---

## 17. 下一步

本决策书确认后，应继续重写以下文档：

1. `MarkOrbit Lite 1.1 PRD`
2. `MarkOrbit Lite 1.1 数据模型与架构设计`
3. `MarkOrbit Lite 1.1 Sprint 0 Codex 开发提示词`
4. `MarkOrbit Lite 1.1 Sprint 1 Codex 开发提示词：Mo Content Foundation`

其中 Sprint 0 仍然可以基本保留，只需补充：

- Lite 1.1 是 Mo 应用层落地；
- 首页预留 Mo Content / Mo Asset Hub；
- Workspace 完整度增加素材库维度；
- 不开发素材库，仅预留入口。
