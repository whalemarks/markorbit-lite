# MarkOrbit Lite 1.1 PRD

版本：Draft 1.0  
关联上位文档：  
- `Mo Architecture｜MarkOrbit 核心架构白皮书`
- `MarkOrbit Lite 1.1 重规划决策书`

产品定位：Mo 能力的第一个可用应用层  
目标用户：中国商标代理人、知识产权顾问、商标代理机构销售/流程人员  
Mo Brain 状态：Lite 1.1 仅预留接口，不做真实接入  
开发原则：PC 端优先，分享页移动端友好，小程序后置

---

## 0. PRD 摘要

MarkOrbit Lite 1.1 是面向商标代理人的 Mo 工作台。

它不是完整 Mo，也不是完整 Mo Brain，而是 Mo 能力在代理人场景中的第一个可用应用层。

Lite 1.1 的核心目标是让代理人每天打开系统后，可以围绕五件事行动：

1. 今天发什么内容；
2. 今天用什么素材；
3. 今天推什么商标；
4. 今天给谁报价；
5. 今天跟进哪些客户。

最终形成五个业务闭环：

- 每日内容生产闭环；
- 商标包装与推荐闭环；
- 全球报价与订单闭环；
- 商机跟进闭环；
- 用户业务空间持续学习闭环。

Lite 1.1 的核心产品结构为：

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

## 1. 产品背景

### 1.1 V1.0 当前基础

MarkOrbit V1.0 已完成 Phase 0-10，并合并 main。

已具备：

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

V1.0 是底盘型系统，解决了底层模型、权限、业务基础和后台管理问题。

### 1.2 V1.0 Lite 的主要问题

Lite 端仍存在：

1. 更像功能菜单，不像业务工作台；
2. AI 功能像普通表单，缺少业务动作感；
3. 商标资产没有转化成商标货架；
4. 商机没有转化成跟进动作；
5. 全球报价没有转化成客户报价方案；
6. 内容生产只有文案，没有素材、模板和半成品；
7. 用户没有每天打开系统的理由。

### 1.3 Lite 1.1 的重规划原因

随着 Mo Architecture 明确，Lite 1.1 不应只是“AI 工具升级”，而应成为：

> **Mo 能力的第一个可用应用层。**

因此 Lite 1.1 必须按 Mo 的长期架构组织，但不能被完整 Mo Brain / Mo Data / Mo Flow 拖慢。

---

## 2. 产品目标

### 2.1 总目标

让商标代理人每天打开 MarkOrbit Lite 后，可以完成：

- 生成可发布内容；
- 使用素材和模板；
- 包装待售商标；
- 生成商标销售页；
- 生成多商标推荐页；
- 生成海外商标报价方案；
- 批量生成商机跟进话术；
- 推进商机到报价或订单。

### 2.2 用户价值目标

Lite 1.1 面向用户的核心价值：

> **每天有内容可发，有商标可推，有客户可跟，有报价可出，有订单可转。**

### 2.3 产品体验目标

用户进入首页后，应在 3 秒内理解：

- 今天可以发什么；
- 用什么图；
- 推什么商标；
- 跟进谁；
- 给谁报价；
- 下一步应该点哪里。

### 2.4 商业目标

Lite 1.1 的商业化重点不是卖 Token，而是围绕代理人的业务结果收费：

- 内容获客；
- 商标推荐；
- 全球报价；
- 商机跟进；
- 订单转化。

---

## 3. 用户角色

### 3.1 Lite 普通用户

主要是商标代理人、知识产权顾问、代理机构销售人员。

需求：

- 每天找内容发；
- 快速写朋友圈/小红书/视频脚本；
- 包装待售商标；
- 给客户推荐商标；
- 快速生成报价；
- 批量跟进商机；
- 转订单。

### 3.2 Lite 机构管理员

代理机构负责人或团队管理员。

需求：

- 管理成员；
- 查看团队内容生产；
- 查看商机推进；
- 查看订单；
- 管理机构资料和部分素材；
- 查看套餐和 Token。

Lite 1.1 可先保留 V1.0 组织权限，不做复杂团队内容协作。

### 3.3 平台 Admin

MarkOrbit 平台运营人员。

需求：

- 管理内置主题；
- 管理平台素材；
- 管理模板；
- 管理国家服务与价格；
- 查看 AuditLog；
- 查看平台数据概览。

Lite 1.1 中 Admin 增强可分 Sprint 推进，不作为 Sprint 0 核心。

### 3.4 外部客户

不是后台用户，但会访问：

- 商标销售页；
- 多商标推荐页；
- 报价方案分享页；
- 询盘表单。

要求：

- 移动端友好；
- 信息清晰；
- 不暴露内部成本、报价规则和私有备注。

---

## 4. 产品模块总览

Lite 1.1 包含六个核心模块、一个支撑层和一个预留层。

### 4.1 核心模块

1. Mo Workspace｜业务空间；
2. Mo Content｜内容生产中心；
3. Mo Assistant｜业务动作助手；
4. Mo Marks｜商标货架；
5. Mo Global｜全球代理中心；
6. Mo Leads｜商机跟进台。

### 4.2 支撑层

- Mo Asset Hub｜内容素材库。

### 4.3 预留层

- Mo Brain Connector｜Mo Brain 连接预留。

---

## 5. Lite 今日工作台

### 5.1 页面定位

`/lite/dashboard`

首页从“功能入口页”升级为“今日工作台”。

核心结构为“五个今日”：

1. 今日发什么；
2. 今日推什么；
3. 今日跟谁；
4. 今日报什么；
5. 今日完善什么。

### 5.2 今日发什么

数据来源：

- Mo Content；
- Mo Topics；
- ContentDraft；
- Mo Asset Hub。

展示：

- 今日推荐主题；
- 推荐素材；
- 生成图文按钮；
- 生成视频脚本按钮；
- 生成私聊话术按钮。

Sprint 0 可显示占位和入口；Sprint 1 后显示真实主题和素材。

### 5.3 今日推什么

数据来源：

- Mo Marks；
- TrademarkAsset；
- TrademarkListing；
- RecommendationPage；
- TrademarkInquiry。

展示：

- 可推广商标；
- 待包装商标；
- 推荐页待完善；
- 新询盘。

Sprint 0 可显示占位；Sprint 3/4 后接入真实数据。

### 5.4 今日跟谁

数据来源：

- Opportunity；
- OpportunityFollowup；
- Mo Leads；
- MessageDraft；
- CommunicationLog。

展示：

- 待跟进商机；
- 高意向商机；
- 已报价未回复；
- 已推荐商标未回复。

Sprint 0 可显示现有 Opportunity 摘要；Sprint 6 后完整。

### 5.5 今日报什么

数据来源：

- CountryService；
- CountryPrice；
- UserPriceRule；
- QuotePlan；
- Order。

展示：

- 可生成报价；
- 最近报价方案；
- 待转订单报价。

Sprint 0 可显示入口；Sprint 5 后完整。

### 5.6 今日完善什么

数据来源：

- UserBusinessProfile；
- UserPersona；
- UserKnowledgeBase；
- UserContentPreference；
- MediaAsset；
- BrainConnection。

展示：

- 业务资料完整度；
- Persona 完整度；
- Knowledge 完整度；
- 素材库完整度；
- Mo Brain 连接状态。

### 5.7 快速行动按钮

至少包括：

- 完善 Mo Workspace；
- 设置 Mo Persona；
- 添加知识资料；
- 上传素材；
- 查看今日选题；
- 写图文；
- 回客户；
- 查看商标资产；
- 生成报价；
- 查看商机；
- 创建 Markreg 订单。

### 5.8 验收标准

- 用户进入 `/lite/dashboard` 后能看到“五个今日”；
- 不再以 Phase 或技术模块为主；
- 首页有明确下一步动作；
- 空状态有业务引导；
- 已有 V1.0 数据摘要不丢失；
- 不破坏旧 Lite 页面入口。

---

## 6. Mo Workspace｜业务空间

### 6.1 页面路径

- `/lite/workspace`
- `/lite/workspace/profile`
- `/lite/workspace/persona`
- `/lite/workspace/knowledge`
- `/lite/workspace/preferences`
- `/lite/workspace/brain-connection`

### 6.2 功能定位

Mo Workspace 是 Lite 1.1 的用户上下文基础。

它让 AI 知道：

- 用户是谁；
- 用户服务谁；
- 用户擅长什么；
- 用户怎么表达；
- 用户有什么知识；
- 用户有什么素材；
- 用户有哪些商标和商机；
- 用户怎么报价。

### 6.3 业务资料

字段建议：

- 公司名称；
- 显示名称；
- 职务；
- 城市；
- 服务国家；
- 服务领域；
- 客户类型；
- 服务优势；
- 默认语气；
- 默认平台；
- 邮箱；
- 电话；
- 微信；
- 网站。

### 6.4 Mo Persona

字段建议：

- 分身名称；
- 角色定位；
- 定位说明；
- 语气；
- 风格；
- 常用开头；
- 常用结尾；
- 禁用表达；
- 常用 CTA；
- 视觉形象描述；
- 头像 URL；
- 是否默认。

V1.1 只做基础配置，不做真实数字人生成。

### 6.5 Mo Knowledge

支持知识条目：

- 服务介绍；
- FAQ；
- 成功案例；
- 报价说明；
- 商标交易流程；
- 国际申请材料说明；
- 客户答复模板；
- 其他笔记。

V1.1 只做纯文本知识库，不做向量知识库。

### 6.6 内容偏好

字段建议：

- 常用平台；
- 偏好语气；
- 偏好长度；
- 偏好主题分类；
- 不喜欢的主题分类；
- 最近主题使用时间。

### 6.7 Brain Connection

页面显示：

- Mo Brain 当前未连接；
- 当前使用 Mo Workspace、平台内置模板和已有平台数据；
- 未来连接后可增强全球商标数据、行业知识、热点主题和报价。

V1.1 不提供真实连接按钮。

### 6.8 Workspace 完整度

建议计算：

- 业务资料 25 分；
- Persona 20 分；
- Knowledge 20 分；
- 内容偏好 15 分；
- 素材库 20 分。

总分 100。

### 6.9 验收标准

- 用户可以编辑业务资料；
- 用户可以编辑默认 Persona；
- 用户可以新增/编辑/删除 Knowledge；
- 用户可以编辑内容偏好；
- 用户可以看到 BrainConnection disabled；
- 用户只能访问自己的 Workspace；
- 操作写 AuditLog。

---

## 7. Mo Content｜内容生产中心

### 7.1 页面路径

- `/lite/content`
- `/lite/content/topics`
- `/lite/content/topics/today`
- `/lite/content/topics/[id]`
- `/lite/content/topics/new`
- `/lite/content/drafts`
- `/lite/content/drafts/[id]`

可兼容旧入口：

- `/lite/ai/graphic-content`
- `/lite/ai/video-script`
- `/lite/ai/marketing-plan`

### 7.2 功能定位

Mo Content 是 Lite 1.1 的日活入口。

它不只是选题，而是完整内容生产前半段：

> 主题 → 素材 → 模板 → 文案 → 视频脚本 → 内容草稿 → 使用记录。

### 7.3 主题来源

V1.1 支持：

1. 内置常青主题；
2. 节假日主题；
3. 商标冷知识；
4. 指南类主题；
5. 朋友圈观点 / 鸡汤类主题；
6. 用户自建主题；
7. 平台运营手动热点主题。

V1.1 不做：

- 抖音/微信/小红书真实热点爬取；
- 官方数据自动采集；
- 同行文章自动采集；
- Mo Brain 真实主题同步。

### 7.4 主题卡字段

每个主题必须是结构化卡片。

字段建议：

- 标题；
- 分类；
- 来源；
- 适用时间；
- 适用对象；
- 适用平台；
- 适用营销目标；
- 基本事实；
- 核心观点；
- 可选行文角度；
- 推荐内容形式；
- 风险提示；
- 关联服务；
- 关联商标类型；
- 推荐素材；
- 推荐模板；
- 推荐 CTA；
- 推荐分；
- 是否长期有效；
- 是否节假日相关；
- 是否热点相关。

### 7.5 每日推荐

推荐逻辑 V1.1 先采用简单规则：

推荐分 = 时间匹配 + 用户业务匹配 + 内容偏好匹配 + 主题新鲜度 + 素材可用度 - 重复惩罚。

### 7.6 主题详情页

主题详情页必须展示：

- 主题说明；
- 推荐理由；
- 适用对象；
- 适用时间；
- 适用平台；
- 基本事实；
- 核心观点；
- 推荐素材；
- 推荐模板；
- 可生成内容类型；
- 使用记录。

操作按钮：

- 生成图文；
- 生成视频脚本；
- 生成私聊话术；
- 保存为我的主题；
- 忽略。

### 7.7 用户自建主题

AI 引导流程：

1. 选择内容类型；
2. 选择目标客户；
3. 选择营销目标；
4. 选择表达风格；
5. 填写补充信息；
6. 生成主题卡；
7. 保存主题。

### 7.8 ContentDraft

ContentDraft 不应只保存纯文本。

应保存结构化内容：

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

### 7.9 内容使用记录

记录：

- 展示；
- 点击；
- 选用；
- 生成；
- 复制；
- 导出；
- 忽略；
- 关联素材；
- 关联商机；
- 关联商标。

### 7.10 验收标准

- 用户能看到每日主题；
- 主题不是纯标题，而是结构化卡片；
- 主题详情页能显示推荐素材和内容动作；
- 用户能生成并保存 ContentDraft；
- 用户行为被记录；
- 普通用户只能看到自己的主题使用和草稿。

---

## 8. Mo Asset Hub｜内容素材库

### 8.1 页面路径

- `/lite/content/assets`
- `/lite/content/assets/upload`
- `/lite/content/assets/[id]`
- `/lite/content/templates`

### 8.2 功能定位

Mo Asset Hub 是内容生产支撑层。

它解决：

> AI 写好了，但用户还缺图、截图、模板和素材的问题。

### 8.3 素材分类

#### 平台素材

- 商标局 logo；
- 国家标识；
- 流程图；
- 风险提示图；
- 节日底图；
- FAQ 卡片；
- 类别图标；
- 服务图标；
- 封面模板。

#### 用户素材

- 商标 logo；
- 驳回文书截图；
- 商标公告截图；
- 产品图；
- 新闻截图；
- 客户授权图；
- 公司素材；
- 个人形象图；
- 其他上传图片。

#### 视频素材预留

- 片头；
- 片尾；
- 转场；
- 背景动效；
- 字幕条；
- CTA 片尾。

V1.1 只管理，不做成片渲染。

### 8.4 素材字段

建议：

- 标题；
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
- status。

### 8.5 用户上传

支持：

- 图片上传；
- 截图上传；
- logo 上传；
- 基础文件信息编辑；
- 标签；
- 可见性选择，默认 private。

V1.1 不做复杂文件 OCR。

### 8.6 主题关联素材

主题详情页可推荐素材。

素材可用于：

- 图文；
- 视频脚本；
- 商标销售页；
- 推荐页；
- 报价方案；
- 商机跟进。

### 8.7 模板库

V1.1 先做模板配置预留：

- 朋友圈图；
- 小红书封面；
- 私聊解释图；
- 商标推荐卡；
- 报价封面；
- 视频封面。

V1.1 不必须真实渲染图片，但需为 V1.2 的 Mo Graphic 预留数据结构。

### 8.8 权利与合规

素材必须支持：

- 来源说明；
- 权利备注；
- 是否平台内置；
- 是否用户上传；
- 是否仅内部参考；
- 是否可用于公开发布。

用户上传素材默认由用户自行保证权利。

### 8.9 验收标准

- 用户可以上传素材；
- 用户可以管理自己的素材；
- 用户素材默认私有；
- 平台素材可被推荐；
- 主题可关联推荐素材；
- 素材使用有记录；
- 不暴露其他用户素材。

---

## 9. Mo Assistant｜业务动作助手

### 9.1 页面路径

- `/lite/assistant`
- `/lite/assistant/write`
- `/lite/assistant/video-script`
- `/lite/assistant/customer-reply`
- `/lite/assistant/drafts/[id]`

旧 `/lite/ai` 可保留并逐步升级。

### 9.2 功能定位

Mo Assistant 是业务动作助手，不是普通聊天框。

它根据具体场景调用：

- Mo Workspace；
- Mo Content；
- Mo Asset Hub；
- Mo Marks；
- Mo Global；
- Mo Leads；
- V1.0 AI Skill Service。

### 9.3 图文生成

输入：

- 主题；
- 平台；
- 目标客户；
- 风格；
- 推荐素材；
- 用户 Persona；
- 用户 Knowledge。

输出：

- 标题；
- 副标题；
- 正文；
- 要点；
- CTA；
- GraphicBrief；
- 推荐素材；
- 推荐模板；
- 风险提示。

### 9.4 视频脚本生成

V1.1 只生成脚本，不生成成片。

输出：

- 30 秒脚本；
- 60 秒脚本；
- 开头 Hook；
- 分镜；
- 口播稿；
- 字幕文案；
- 画面建议；
- 素材建议；
- CTA；
- 封面标题。

### 9.5 私聊话术生成

输出：

- 微信私聊；
- 客户跟进；
- 商标推荐；
- 报价说明；
- 风险提醒；
- 二次跟进。

### 9.6 客户问题答复

流程：

1. 用户粘贴客户问题；
2. AI 判断问题类型；
3. AI 追问 1-3 个关键问题；
4. 用户补充信息；
5. AI 生成回复；
6. 输出专业分析；
7. 输出风险提示；
8. 输出成交引导；
9. 给出文案评分；
10. 推荐 FAQ。

### 9.7 文案评分

评分维度：

- 专业度；
- 清晰度；
- 风险提示；
- 成交引导；
- 语气自然度。

### 9.8 验收标准

- 生成内容能保存为 ContentDraft；
- 生成内容能引用主题和素材；
- 生成内容能参考 Persona；
- 生成内容有 AI Skill Run；
- 成功扣 Token，失败不扣 Token；
- 用户只能查看自己的生成记录。

---

## 10. Mo Marks｜商标货架

### 10.1 页面路径

- `/lite/marks`
- `/lite/marks/assets`
- `/lite/marks/import`
- `/lite/marks/for-sale`
- `/lite/marks/[id]`
- `/lite/marks/[id]/sales-page`
- `/lite/recommendation-pages`
- `/lite/recommendation-pages/new`
- `/lite/recommendation-pages/[id]`
- `/s/marks/[shareCode]`
- `/r/marks/[shareCode]`

旧 `/lite/assets` 需兼容。

### 10.2 功能定位

Mo Marks 把商标从“资产记录”变成“可包装、可展示、可推荐、可询盘”的商标货架。

### 10.3 商标分类

资产类型：

- 自有商标；
- 客户商标；
- 待售商标；
- 平台代售商标，预留。

销售状态：

- 不出售；
- 准备中；
- 可售；
- 已预订；
- 已售。

### 10.4 导入方式

支持：

- CSV / Excel；
- 粘贴表格；
- 批量输入商标名；
- 导入预览；
- 错误行提示；
- 待补全字段提示。

V1.1 不接正式全球商标数据 API。

### 10.5 商标 logo 与素材库联动

用户上传的商标 logo 应同步进入 Mo Asset Hub。

用于：

- 销售页；
- 推荐页；
- 图文内容；
- 视频脚本；
- 私聊推荐图。

### 10.6 单商标销售页

展示：

- 商标名称；
- logo；
- 国家；
- 类别；
- 注册号 / 申请号；
- 状态；
- 有效期；
- 推荐行业；
- 推荐客户画像；
- 核心卖点；
- 命名亮点；
- 品牌故事；
- 推荐售价；
- 交易说明；
- 风险说明；
- FAQ；
- 咨询按钮。

### 10.7 AI 包装

输出：

- 一句话卖点；
- 3 个核心亮点；
- 推荐行业；
- 推荐客户画像；
- 品牌故事；
- 朋友圈文案；
- 私聊推荐话术；
- 短视频脚本；
- 推荐页摘要。

### 10.8 多商标推荐页

支持：

- 固定推荐页；
- 临时客户推荐页；
- 行业推荐页；
- 类别推荐页；
- 预算推荐页。

内容：

- 推荐页标题；
- 推荐说明；
- 推荐对象；
- 推荐商标列表；
- 每个商标推荐理由；
- 价格；
- 咨询按钮；
- 询盘表单；
- 分享链接。

### 10.9 询盘

询盘进入：

- TrademarkInquiry；
- 可转 Opportunity；
- 可关联推荐页；
- 可关联商标。

### 10.10 验收标准

- 用户能导入商标；
- 能标记待售；
- 能生成销售页；
- 能生成多商标推荐页；
- 外部客户能提交询盘；
- 询盘能转商机；
- 不自动公开平台 marketplace；
- 不自动创建佣金。

---

## 11. Mo Global｜全球代理中心

### 11.1 页面路径

- `/lite/global`
- `/lite/global/prices`
- `/lite/global/price-rules`
- `/lite/global/quote-plans`
- `/lite/global/quote-plans/new`
- `/lite/global/quote-plans/[id]`
- `/q/[shareCode]`

### 11.2 功能定位

Mo Global 是全球商标报价方案生成器，不只是价格表。

### 11.3 报价层级

1. 平台服务价格：来自 CountryService / CountryPrice；
2. 用户报价规则：UserPriceRule；
3. 客户报价方案：QuotePlan / QuoteProposal。

### 11.4 客户需求输入

支持输入：

- 客户名称；
- 商标名称；
- 目标国家；
- 类别；
- 商品服务；
- 预算；
- 急迫程度；
- 是否已有中国商标；
- 是否已有海外销售；
- 平台，如 Amazon / TikTok Shop / Temu 等。

### 11.5 输出内容

报价方案应包含：

- 推荐国家；
- 每个国家费用；
- 总费用；
- 材料清单；
- 预计周期；
- 风险提示；
- 服务说明；
- 下一步建议；
- 客户版报价文案；
- 内部成本和利润，仅内部可见。

### 11.6 转订单

QuotePlan 可转 Markreg Order。

转订单时应复用 V1.0 Phase 8 Order，不创建新订单表。

### 11.7 验收标准

- 用户能查询国家价格；
- 用户能设置报价规则；
- 用户能生成报价方案；
- 用户能分享客户版报价；
- 用户能转 Markreg Order；
- 外部报价页不显示内部成本；
- 不触发真实支付或递交。

---

## 12. Mo Leads｜商机跟进台

### 12.1 页面路径

- `/lite/leads`
- `/lite/leads/today`
- `/lite/leads/campaigns`
- `/lite/leads/campaigns/[id]`
- `/lite/leads/[id]`

旧 `/lite/opportunities` 需兼容。

### 12.2 功能定位

Mo Leads 把 Opportunity 从列表升级为行动台。

### 12.3 今日跟进

显示：

- 今日待跟进；
- 高意向商机；
- 已报价未回复；
- 已推荐商标未回复；
- 长期未联系；
- 可转订单。

### 12.4 批量话术

支持生成：

- 微信话术；
- 邮件文案；
- 短信草稿；
- 电话提纲；
- 二次跟进；
- 报价跟进；
- 商标推荐跟进。

### 12.5 关联动作

商机可关联：

- ContentDraft；
- RecommendationPage；
- QuotePlan；
- MessageDraft；
- CommunicationLog；
- Markreg Order。

### 12.6 群发边界

V1.1 不做真实发送。

只做：

- 草稿；
- 复制；
- 导出；
- 标记已发送；
- 创建跟进记录。

### 12.7 验收标准

- 用户能看到今日待跟进；
- 能批量选择商机；
- 能生成跟进话术；
- 能记录沟通；
- 能转报价；
- 能转订单；
- 不真实发送邮件/短信/微信。

---

## 13. Mo Brain Connector 预留

### 13.1 页面路径

- `/lite/workspace/brain-connection`

### 13.2 状态

V1.1 默认：

- status: disabled；
- mode: none；
- allowReadEnhance: false；
- allowAnonFeedback: false；
- allowDataFusion: false。

### 13.3 页面说明

显示：

> Mo Brain 是 MarkOrbit 未来的行业大脑，将连接全球商标数据、行业知识、热点主题和国家报价。Lite 1.1 暂未接入，当前仅使用你的 Mo Workspace 和平台已有数据。

### 13.4 验收标准

- 页面显示未连接；
- 不提供真实连接；
- 不发送任何数据到 Mo Brain；
- 后续接入有授权边界预留。

---

## 14. 权限与数据边界

### 14.1 用户私有数据

以下数据默认私有：

- Workspace；
- Persona；
- Knowledge；
- 用户素材；
- 用户商标资产；
- 用户待售商标；
- 商机；
- 报价规则；
- 内容偏好；
- ContentDraft；
- 推荐页；
- 报价方案；
- 跟进记录。

### 14.2 公共数据

公共或平台数据包括：

- 平台内置主题；
- 平台内置素材；
- 平台内置模板；
- CountryService；
- CountryPrice；
- 平台规则说明。

### 14.3 分享页数据边界

公开分享页不得展示：

- 内部成本；
- 用户报价规则；
- 内部备注；
- 私有客户资料；
- 私有商机；
- MGSN 服务商成本；
- Commission。

### 14.4 Admin 边界

Admin 可管理平台数据和查看必要运营摘要，但不得把 A 用户私有数据暴露给 B 用户。

---

## 15. AuditLog 要求

关键操作写 AuditLog，包括：

- workspace.profile.update；
- persona.create / update；
- knowledge.create / update / delete；
- content_theme.create / select / ignore / use；
- content_draft.generate / copy；
- media_asset.upload / update / delete / use；
- template_asset.create / update；
- trademark.import / classify；
- trademark_listing.create / update / share；
- recommendation_page.create / update / publish；
- trademark_inquiry.create / convert_to_opportunity；
- quote_rule.create / update；
- quote_plan.create / update / share / convert_order；
- lead_campaign.create / generate_messages；
- communication_log.create；
- opportunity.convert_to_quote；
- opportunity.convert_to_order；
- permission.denied。

---

## 16. Token 与商业化

### 16.1 继续复用 V1.0 Token

Lite 1.1 不新增 Token 表。

继续复用：

- AISkill；
- AISkillRun；
- TokenLog。

原则：

- 成功扣 Token；
- 失败不扣 Token；
- 生成结果必须落业务对象。

### 16.2 新增 Skill 建议

- topic_graphic_copy_generate；
- topic_video_script_generate；
- topic_private_chat_generate；
- customer_reply_interactive；
- trademark_sales_copy_generate；
- recommendation_page_copy_generate；
- quote_plan_generate；
- lead_followup_message_generate；
- monthly_marketing_plan_generate；
- media_asset_recommend。

### 16.3 付费能力

可计费能力：

- 生成图文；
- 生成视频脚本；
- 生成客户答复；
- 生成商标销售文案；
- 生成推荐页文案；
- 生成报价方案；
- 批量生成商机跟进话术；
- 月度营销计划；
- 高级素材/模板使用；
- 更多素材存储空间。

---

## 17. 非功能要求

### 17.1 性能

- 首页加载不能依赖大量 AI 实时生成；
- 今日推荐可预计算或使用规则；
- 素材列表分页；
- 商标资产列表分页；
- AI 生成异步 loading；
- 失败可重试。

### 17.2 可用性

- 不显示 Phase 编号；
- 导航使用产品名；
- 页面有明确下一步按钮；
- 空状态必须有业务引导；
- 外部分享页移动端友好。

### 17.3 合规

- AI 输出需提示用户复核；
- 法律判断不能绝对化；
- 报价需提示以最终确认为准；
- 素材需记录来源和权利说明；
- 用户上传素材默认由用户保证权利；
- 私有数据默认不共享。

### 17.4 兼容

必须兼容旧入口：

- `/lite/assets`
- `/lite/ai`
- `/lite/opportunities`
- `/lite/partner`
- `/markreg`
- `/admin`
- `/mgsn`

---

## 18. Sprint 验收总览

### Sprint 0

验收：

- 今日工作台；
- Mo Workspace；
- Persona；
- Knowledge；
- Preferences；
- BrainConnection disabled；
- Mo Content / Mo Asset Hub 入口预留。

### Sprint 1

验收：

- Mo Topics；
- Mo Asset Hub 最小版；
- 主题关联素材；
- 结构化 ContentDraft；
- 主题详情页。

### Sprint 2

验收：

- 主题生成图文；
- 主题生成视频脚本；
- 主题生成私聊话术；
- 客户问题答复；
- ContentDraft 落库；
- AISkillRun 记录。

### Sprint 3

验收：

- 商标导入；
- 商标分类；
- 待售标记；
- logo 进入素材库；
- TrademarkDataProvider 预留。

### Sprint 4

验收：

- 单商标销售页；
- 多商标推荐页；
- 询盘表单；
- 询盘转商机。

### Sprint 5

验收：

- 国家价格查询；
- 用户报价规则；
- 报价方案；
- 报价分享页；
- 转 Markreg Order。

### Sprint 6

验收：

- 今日跟进；
- 批量话术；
- 沟通记录；
- 转报价；
- 转订单。

### Sprint 7

验收：

- WorkflowDefinition；
- WorkflowRun；
- WorkflowStepRun；
- 4 个轻 Workflow 记录。

---

## 19. 成功标准

### 19.1 产品成功指标

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

### 19.2 体验成功标准

用户能明确回答：

- 今天发什么；
- 用什么图；
- 推什么商标；
- 给谁报价；
- 跟进谁；
- 下一步做什么。

### 19.3 架构成功标准

- 不破坏 V1.0；
- 不修改历史 migration；
- 不创建平行系统；
- Mo Brain 仅预留；
- 用户数据默认私有；
- 内容、素材、商标、报价、商机之间能形成关联。

---

## 20. 下一步

本 PRD 确认后，应继续输出：

1. `MarkOrbit Lite 1.1 数据模型与架构设计`
2. `MarkOrbit Lite 1.1 Sprint 0 Codex 开发提示词`
3. `MarkOrbit Lite 1.1 Sprint 1 Codex 开发提示词：Mo Content Foundation`

其中 Sprint 0 可基于旧 Sprint 0 提示词调整，重点补充：

- Lite 1.1 是 Mo 应用层落地；
- 首页采用“五个今日”；
- 预留 Mo Content / Mo Asset Hub；
- Workspace 完整度增加素材库维度；
- 不开发素材库，只预留入口。
