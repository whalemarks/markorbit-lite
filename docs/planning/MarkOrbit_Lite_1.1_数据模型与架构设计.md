# MarkOrbit Lite 1.1 数据模型与架构设计

版本：Draft 1.0  
关联文档：  
- `Mo Architecture｜MarkOrbit 核心架构白皮书`
- `MarkOrbit Lite 1.1 重规划决策书`
- `MarkOrbit Lite 1.1 PRD`

适用范围：MarkOrbit Lite 1.1 数据模型、服务层、API、权限、AI Skill、Workflow 预留与 Codex 开发约束  
核心原则：不破坏 V1.0，不修改历史 migration，不创建平行系统，按 Mo 架构预留未来能力  
Mo Brain 状态：Lite 1.1 仅预留 BrainConnector，不做真实接入

---

## 0. 执行摘要

MarkOrbit Lite 1.1 的数据模型和架构设计，需要同时满足两个目标：

1. **让 Lite 1.1 形成真实可用的代理人工作台。**
2. **为后续 Mo Brain、Mo Intelligence、Mo Guide、Mo Flow 和 Workflow Runtime 预留稳定接口。**

Lite 1.1 不建设完整 Mo，但必须按照 Mo 架构组织数据和能力。

本设计将 Lite 1.1 拆成以下核心数据域：

1. Mo Workspace｜用户业务空间；
2. Mo Content｜内容主题与草稿；
3. Mo Asset Hub｜内容素材库；
4. Mo Assistant｜AI 业务动作；
5. Mo Marks｜商标货架；
6. Mo Global｜全球报价中心；
7. Mo Leads｜商机跟进台；
8. Mo Brain Connector｜未来大脑连接预留；
9. Workflow Lite Runtime｜轻工作流预留；
10. Capability Catalog｜能力目录预留。

Lite 1.1 的核心架构原则是：

> **业务对象复用 V1.0，新增模型只补充 V1.1 必需能力，不创建重复系统。**

---

## 1. 总体架构原则

### 1.1 不破坏 V1.0

必须保持 V1.0 已完成能力稳定：

- User；
- Organization；
- Membership；
- Token；
- AISkill；
- AISkillRun；
- TokenLog；
- UserMemory；
- TrademarkAsset；
- FileDocument；
- TrademarkTag；
- TrademarkPackage；
- PartnerAccount；
- ReferralLink；
- ReferralClick；
- Customer；
- Order；
- Commission；
- Opportunity；
- OpportunityFollowup；
- ServiceProvider；
- CountryService；
- CountryPrice；
- CaseAssignment；
- AuditLog。

### 1.2 不创建平行系统

禁止创建：

- duplicate users；
- duplicate customers；
- duplicate orders；
- duplicate opportunities；
- duplicate commissions；
- markreg_orders；
- mgsn_orders；
- lead_v2；
- asset_v2；
- trademark_assets_v2；
- ai_runs_v2。

### 1.3 不修改历史 migration

禁止修改任何已合并 main 的 migration。

特别注意：

- 不修改 Phase 8 migration；
- 不修改 Phase 9 migration；
- 不修改 `Order.countries` 类型；
- `Order.countries` 必须保持 `String?` / TEXT；
- 不改成 `String[]` / TEXT[]。

如需 schema 变更，只能新增当前 Sprint migration。

### 1.4 私有数据默认隔离

以下数据默认属于用户或组织私有：

- Workspace；
- Persona；
- Knowledge；
- MediaAsset；
- UserContentPreference；
- UserPriceRule；
- ContentDraft；
- TrademarkListing；
- RecommendationPage；
- QuotePlan；
- MessageDraft；
- CommunicationLog；
- WorkflowRun。

未授权不得进入 Mo Brain、平台公共池或其他用户空间。

### 1.5 Mo Brain 仅预留

Lite 1.1 只做：

- BrainConnection；
- BrainConnector 接口；
- DisabledBrainConnector；
- 数据源字段；
- 授权字段。

不做：

- 真实 Mo Brain API；
- 真实全球商标数据同步；
- 真实热点采集；
- 真实知识图谱查询；
- 自动上传用户私有数据。

---

## 2. 数据域总览

Lite 1.1 数据域如下：

```text
User / Organization
    ↓
Mo Workspace
    ├── UserBusinessProfile
    ├── UserPersona
    ├── UserKnowledgeBase
    ├── UserKnowledgeDocument
    ├── UserContentPreference
    └── BrainConnection

Mo Content
    ├── ContentTheme
    ├── ContentThemeRecommendation
    ├── ContentThemeUsage
    └── ContentDraft

Mo Asset Hub
    ├── MediaAsset
    ├── TemplateAsset
    ├── TopicAssetMapping
    └── AssetUsageLog

Mo Marks
    ├── TrademarkAsset，复用并增强
    ├── TrademarkImportBatch
    ├── TrademarkImportRow
    ├── TrademarkListing
    ├── TrademarkListingMedia
    ├── TrademarkRecommendationPage
    ├── TrademarkRecommendationPageItem
    └── TrademarkInquiry

Mo Global
    ├── CountryService，复用
    ├── CountryPrice，复用
    ├── UserPriceRule
    ├── QuotePlan
    ├── QuotePlanItem
    └── QuoteProposal

Mo Leads
    ├── Opportunity，复用
    ├── OpportunityFollowup，复用
    ├── OpportunityCampaign
    ├── CampaignRecipient
    ├── MessageDraft
    └── CommunicationLog

Workflow Lite Runtime，预留
    ├── WorkflowDefinition
    ├── WorkflowRun
    └── WorkflowStepRun

Capability Catalog，预留
    ├── CapabilityDefinition
    └── SkillImplementationMapping，可后置
```

---

## 3. Mo Workspace 数据模型

Mo Workspace 是用户业务空间，是 Lite 1.1 的上下文底座。

---

## 3.1 UserBusinessProfile

### 3.1.1 作用

保存用户业务资料，让 AI 知道用户是谁、服务谁、擅长什么、怎么联系。

### 3.1.2 Prisma 草案

```prisma
model UserBusinessProfile {
  id               String   @id @default(cuid())
  userId           String   @unique
  organizationName String?
  displayName      String?
  title            String?
  city             String?
  serviceCountries Json?
  serviceAreas     Json?
  customerTypes    Json?
  strengths        Json?
  defaultTone      String?
  defaultPlatforms Json?
  contactEmail     String?
  contactPhone     String?
  contactWechat    String?
  website          String?
  metadata         Json?
  createdAt        DateTime @default(now())
  updatedAt        DateTime @updatedAt

  user             User     @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@map("user_business_profiles")
}
```

### 3.1.3 说明

- `serviceCountries` 用 Json，便于多国家保存；
- `serviceAreas` 可保存国际申请、美国、欧盟、商标交易、OA 等；
- `strengths` 可保存服务优势；
- `userId` 唯一，单用户一个业务资料。

---

## 3.2 UserPersona

### 3.2.1 作用

保存用户 Mo Persona，用于 AI 生成内容、答复客户和商标包装时保持表达风格。

### 3.2.2 Prisma 草案

```prisma
model UserPersona {
  id             String   @id @default(cuid())
  userId         String
  name           String
  roleTitle      String?
  positioning    String?
  tone           String?
  style          String?
  openingLines   Json?
  closingLines   Json?
  forbiddenWords Json?
  commonCtas     Json?
  visualPrompt   String?
  avatarUrl      String?
  isDefault      Boolean  @default(false)
  metadata       Json?
  createdAt      DateTime @default(now())
  updatedAt      DateTime @updatedAt

  user           User     @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@map("user_personas")
}
```

### 3.2.3 说明

- 一个用户可以有多个 Persona；
- V1.1 页面可先只管理默认 Persona；
- `visualPrompt` 为后续 Mo Graphic / Mo Video / 数字人预留。

---

## 3.3 UserKnowledgeBase

### 3.3.1 作用

保存用户私有知识库容器。

### 3.3.2 Prisma 草案

```prisma
model UserKnowledgeBase {
  id          String                  @id @default(cuid())
  userId      String
  name        String
  description String?
  status      UserKnowledgeBaseStatus @default(active)
  createdAt   DateTime                @default(now())
  updatedAt   DateTime                @updatedAt

  user        User                    @relation(fields: [userId], references: [id], onDelete: Cascade)
  documents   UserKnowledgeDocument[]

  @@index([userId])
  @@map("user_knowledge_bases")
}

enum UserKnowledgeBaseStatus {
  active
  archived
}
```

---

## 3.4 UserKnowledgeDocument

### 3.4.1 作用

保存用户知识条目。

V1.1 只做纯文本知识，不做向量库。

### 3.4.2 Prisma 草案

```prisma
model UserKnowledgeDocument {
  id              String                    @id @default(cuid())
  knowledgeBaseId String
  userId          String
  title           String
  content         String
  documentType    UserKnowledgeDocumentType @default(note)
  sourceType      KnowledgeSourceType       @default(manual)
  sourceRef       String?
  tags            Json?
  metadata        Json?
  createdAt       DateTime                  @default(now())
  updatedAt       DateTime                  @updatedAt

  knowledgeBase   UserKnowledgeBase         @relation(fields: [knowledgeBaseId], references: [id], onDelete: Cascade)
  user            User                      @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@index([knowledgeBaseId])
  @@map("user_knowledge_documents")
}

enum UserKnowledgeDocumentType {
  note
  service_intro
  faq
  case_study
  template
  pricing_note
  process_note
  risk_note
}

enum KnowledgeSourceType {
  manual
  import
  generated
}
```

---

## 3.5 UserContentPreference

### 3.5.1 作用

保存用户内容偏好，用于每日主题推荐和内容生成。

### 3.5.2 Prisma 草案

```prisma
model UserContentPreference {
  id                    String   @id @default(cuid())
  userId                String   @unique
  preferredPlatforms    Json?
  preferredTone         String?
  preferredLengths      Json?
  preferredCategories   Json?
  dislikedCategories    Json?
  lastThemeUsedAt       DateTime?
  metadata              Json?
  createdAt             DateTime @default(now())
  updatedAt             DateTime @updatedAt

  user                  User     @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@map("user_content_preferences")
}
```

---

## 3.6 BrainConnection

### 3.6.1 作用

预留 Mo Brain 连接状态与授权边界。

### 3.6.2 Prisma 草案

```prisma
model BrainConnection {
  id                 String                @id @default(cuid())
  userId             String
  status             BrainConnectionStatus @default(disabled)
  connectionMode     BrainConnectionMode   @default(none)
  allowReadEnhance   Boolean               @default(false)
  allowAnonFeedback  Boolean               @default(false)
  allowDataFusion    Boolean               @default(false)
  lastSyncAt         DateTime?
  metadata           Json?
  createdAt          DateTime              @default(now())
  updatedAt          DateTime              @updatedAt

  user               User                  @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@map("brain_connections")
}

enum BrainConnectionStatus {
  disabled
  pending
  connected
  paused
  error
}

enum BrainConnectionMode {
  none
  read_only
  read_write
}
```

### 3.6.3 V1.1 默认

- `status = disabled`
- `connectionMode = none`
- `allowReadEnhance = false`
- `allowAnonFeedback = false`
- `allowDataFusion = false`

---

## 4. Mo Content 数据模型

Mo Content 负责每日选题、主题卡、内容草稿和使用记录。

---

## 4.1 ContentTheme

### 4.1.1 作用

保存平台内置主题和用户自建主题。

### 4.1.2 Prisma 草案

```prisma
model ContentTheme {
  id                 String                  @id @default(cuid())
  ownerUserId         String?
  organizationId      String?
  title              String
  summary            String?
  category           ContentThemeCategory
  sourceType         ContentThemeSourceType  @default(platform_builtin)
  sourceName         String?
  sourceRef          String?
  sourceUrl          String?
  sourceConfidence   Float?
  sourceUpdatedAt    DateTime?
  applicableFrom     DateTime?
  applicableTo       DateTime?
  evergreen          Boolean                 @default(false)
  targetAudiences    Json?
  platforms          Json?
  marketingGoals     Json?
  coreFacts          Json?
  keyOpinions        Json?
  angles             Json?
  recommendedFormats Json?
  riskNotes          Json?
  relatedServices    Json?
  relatedTrademarkTypes Json?
  recommendedCtas    Json?
  status             ContentThemeStatus      @default(active)
  metadata           Json?
  createdAt          DateTime                @default(now())
  updatedAt          DateTime                @updatedAt

  ownerUser          User?                   @relation(fields: [ownerUserId], references: [id], onDelete: Cascade)

  @@index([ownerUserId])
  @@index([category])
  @@index([status])
  @@map("content_themes")
}

enum ContentThemeCategory {
  trademark_knowledge
  how_to
  holiday
  hot_event
  case_analysis
  service_marketing
  trademark_sale
  quote_marketing
  personal_branding
  chicken_soup
  other
}

enum ContentThemeSourceType {
  platform_builtin
  user_created
  manual_hotspot
  brain_reserved
  external_reserved
}

enum ContentThemeStatus {
  draft
  active
  archived
}
```

### 4.1.3 设计说明

- `sourceType = brain_reserved` 为未来 Mo Brain 同步预留；
- V1.1 不做真实热点采集；
- `ownerUserId` 为空代表平台主题；
- `ownerUserId` 有值代表用户自建主题。

---

## 4.2 ContentThemeRecommendation

### 4.2.1 作用

保存每日推荐结果，不必每次实时计算。

### 4.2.2 Prisma 草案

```prisma
model ContentThemeRecommendation {
  id              String                     @id @default(cuid())
  userId          String
  themeId         String
  recommendationDate DateTime
  rank            Int
  score           Float?
  reason          String?
  status          ThemeRecommendationStatus  @default(shown)
  metadata        Json?
  createdAt       DateTime                   @default(now())
  updatedAt       DateTime                   @updatedAt

  user            User                       @relation(fields: [userId], references: [id], onDelete: Cascade)
  theme           ContentTheme               @relation(fields: [themeId], references: [id], onDelete: Cascade)

  @@index([userId, recommendationDate])
  @@index([themeId])
  @@map("content_theme_recommendations")
}

enum ThemeRecommendationStatus {
  shown
  clicked
  used
  ignored
  expired
}
```

---

## 4.3 ContentThemeUsage

### 4.3.1 作用

记录主题被用户如何使用。

### 4.3.2 Prisma 草案

```prisma
model ContentThemeUsage {
  id            String            @id @default(cuid())
  userId        String
  themeId       String
  action        ThemeUsageAction
  outputType    ContentOutputType?
  objectType    String?
  objectId      String?
  metadata      Json?
  createdAt     DateTime          @default(now())

  user          User              @relation(fields: [userId], references: [id], onDelete: Cascade)
  theme         ContentTheme      @relation(fields: [themeId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@index([themeId])
  @@map("content_theme_usages")
}

enum ThemeUsageAction {
  view
  click
  use
  ignore
  generate
  copy
  export
  save
}

enum ContentOutputType {
  graphic_copy
  video_script
  private_chat
  email
  sms
  phone_script
  quote_copy
  trademark_sales_copy
}
```

---

## 4.4 ContentDraft

### 4.4.1 作用

保存 AI 生成或用户编辑的内容草稿。

ContentDraft 是 V1.2 图文生成和视频生成的基础，不应只保存纯文本。

### 4.4.2 Prisma 草案

```prisma
model ContentDraft {
  id                  String             @id @default(cuid())
  userId              String
  themeId             String?
  aiSkillRunId         String?
  title               String?
  outputType           ContentOutputType
  platform             String?
  headline             String?
  subheadline          String?
  mainCopy             String?
  bulletPoints         Json?
  cta                  String?
  graphicBrief         Json?
  videoBrief           Json?
  scenePlan            Json?
  captionText          String?
  recommendedAssetIds  Json?
  templateType         String?
  visualStyle          String?
  legalDisclaimer      String?
  contactBlock         Json?
  status               ContentDraftStatus @default(draft)
  copiedAt             DateTime?
  exportedAt           DateTime?
  metadata             Json?
  createdAt            DateTime           @default(now())
  updatedAt            DateTime           @updatedAt

  user                 User               @relation(fields: [userId], references: [id], onDelete: Cascade)
  theme                ContentTheme?       @relation(fields: [themeId], references: [id], onDelete: SetNull)
  aiSkillRun           AISkillRun?         @relation(fields: [aiSkillRunId], references: [id], onDelete: SetNull)

  @@index([userId])
  @@index([themeId])
  @@index([outputType])
  @@map("content_drafts")
}

enum ContentDraftStatus {
  draft
  saved
  copied
  exported
  archived
}
```

### 4.4.3 设计说明

- `graphicBrief` 为 V1.2 Mo Graphic 使用；
- `videoBrief` / `scenePlan` 为 V1.2 Mo Video Worker 使用；
- `recommendedAssetIds` 用 Json 保存推荐素材 ID 列表，后续可规范化；
- `aiSkillRunId` 关联 AI 生成记录。

---

## 5. Mo Asset Hub 数据模型

Mo Asset Hub 是内容素材库，是 Mo Content、Mo Marks、Mo Global、Mo Leads 的共同支撑层。

---

## 5.1 MediaAsset

### 5.1.1 作用

保存平台和用户素材。

### 5.1.2 Prisma 草案

```prisma
model MediaAsset {
  id              String             @id @default(cuid())
  ownerUserId      String?
  organizationId   String?
  title           String
  assetType       MediaAssetType
  mediaCategory   MediaCategory
  sourceType      MediaSourceType
  fileUrl         String
  thumbnailUrl    String?
  previewUrl      String?
  description     String?
  tags            Json?
  jurisdiction    String?
  language        String?
  relatedScenario Json?
  visibility      MediaVisibility    @default(private)
  rightsNote      String?
  sourceUrl       String?
  sourceName      String?
  status          MediaAssetStatus    @default(active)
  metadata        Json?
  createdAt       DateTime           @default(now())
  updatedAt       DateTime           @updatedAt

  ownerUser       User?              @relation(fields: [ownerUserId], references: [id], onDelete: Cascade)

  @@index([ownerUserId])
  @@index([assetType])
  @@index([mediaCategory])
  @@index([visibility])
  @@map("media_assets")
}

enum MediaAssetType {
  image
  screenshot
  illustration
  logo
  svg
  template_preview
  video_clip
  transition
  audio
  icon
  document_image
}

enum MediaCategory {
  official_logo
  country_flag
  workflow
  rejection_case
  news_event
  trademark_marketing
  holiday
  video_transition
  video_intro
  video_outro
  subtitle_bar
  user_upload
  trademark_logo
  quote_visual
  lead_marketing
  other
}

enum MediaSourceType {
  platform_builtin
  user_upload
  external_capture
  generated
  brain_reserved
}

enum MediaVisibility {
  platform
  private
  organization
  shared
}

enum MediaAssetStatus {
  active
  archived
  disabled
}
```

### 5.1.3 权限说明

- `visibility = platform`：平台素材，所有用户可用；
- `visibility = private`：仅 ownerUser 可用；
- `visibility = organization`：组织内可用；
- `visibility = shared`：预留共享能力；
- 用户上传默认 private。

---

## 5.2 TemplateAsset

### 5.2.1 作用

保存图文、推荐页、报价页、视频封面等模板配置。

### 5.2.2 Prisma 草案

```prisma
model TemplateAsset {
  id             String              @id @default(cuid())
  ownerUserId     String?
  organizationId  String?
  templateType   TemplateAssetType
  title          String
  description    String?
  configJson     Json
  styleTags      Json?
  colorTheme     String?
  editableFields Json?
  outputRatio    String?
  isBuiltIn      Boolean             @default(false)
  status         TemplateAssetStatus  @default(active)
  metadata       Json?
  createdAt      DateTime            @default(now())
  updatedAt      DateTime            @updatedAt

  ownerUser      User?               @relation(fields: [ownerUserId], references: [id], onDelete: Cascade)

  @@index([ownerUserId])
  @@index([templateType])
  @@index([isBuiltIn])
  @@map("template_assets")
}

enum TemplateAssetType {
  graphic_post
  xiaohongshu_cover
  friend_circle_card
  private_chat_image
  trademark_listing_page
  trademark_recommendation_page
  quote_card
  video_cover
  video_intro
  video_outro
}

enum TemplateAssetStatus {
  active
  archived
  disabled
}
```

### 5.2.3 设计说明

V1.1 可先只保存模板配置和预览，不必须实现图文渲染。

---

## 5.3 TopicAssetMapping

### 5.3.1 作用

连接主题和推荐素材。

### 5.3.2 Prisma 草案

```prisma
model TopicAssetMapping {
  id        String          @id @default(cuid())
  themeId   String
  assetId   String
  usageType TopicAssetUsage
  priority  Int             @default(0)
  metadata  Json?
  createdAt DateTime        @default(now())

  theme     ContentTheme    @relation(fields: [themeId], references: [id], onDelete: Cascade)
  asset     MediaAsset      @relation(fields: [assetId], references: [id], onDelete: Cascade)

  @@index([themeId])
  @@index([assetId])
  @@map("topic_asset_mappings")
}

enum TopicAssetUsage {
  cover
  illustration
  evidence
  background
  ending
  video_broll
  logo
  reference
}
```

---

## 5.4 AssetUsageLog

### 5.4.1 作用

记录素材被谁、在哪个模块、哪个对象中使用。

### 5.4.2 Prisma 草案

```prisma
model AssetUsageLog {
  id         String          @id @default(cuid())
  userId     String
  assetId    String
  module     AssetUsageModule
  objectType String?
  objectId   String?
  action     AssetUsageAction
  metadata   Json?
  createdAt  DateTime        @default(now())

  user       User            @relation(fields: [userId], references: [id], onDelete: Cascade)
  asset      MediaAsset      @relation(fields: [assetId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@index([assetId])
  @@index([module])
  @@map("asset_usage_logs")
}

enum AssetUsageModule {
  content
  assistant
  marks
  global
  leads
  workspace
}

enum AssetUsageAction {
  view
  select
  use
  copy
  export
  attach
  remove
}
```

---

## 6. Mo Assistant 与 AI Skill 架构

Lite 1.1 不新增一套 AI 系统，而是复用 V1.0 AI Skill Service。

---

## 6.1 AI Skill 命名建议

新增或调整以下 Skill：

```text
topic_graphic_copy_generate
topic_video_script_generate
topic_private_chat_generate
customer_reply_interactive
trademark_sales_copy_generate
recommendation_page_copy_generate
quote_plan_generate
lead_followup_message_generate
monthly_marketing_plan_generate
media_asset_recommend
```

---

## 6.2 AI 调用上下文

所有 Lite 1.1 AI 生成应通过 WorkspaceContextBuilder 构造上下文。

上下文优先级：

```text
User explicit input
  ↓
Current business object
  ↓
Mo Workspace
  ↓
User Persona
  ↓
User Knowledge
  ↓
User Content Preference
  ↓
Related Assets / Templates
  ↓
Platform built-in rules
  ↓
Mo Brain reserved, disabled in V1.1
```

---

## 6.3 AI 输出落库要求

AI 输出不得只返回给前端。

必须落到业务对象：

- 图文 / 视频脚本 / 私聊话术 → ContentDraft；
- 客户答复 → ContentDraft 或 MessageDraft；
- 商标销售包装 → TrademarkPackage / TrademarkListing；
- 推荐页文案 → TrademarkRecommendationPage；
- 报价方案 → QuotePlan / QuoteProposal；
- 商机跟进 → MessageDraft。

同时记录：

- AISkillRun；
- TokenLog；
- AuditLog。

---

## 6.4 ContentActionEngine

建议新增服务：

`lib/assistant/contentActionEngine.ts`

职责：

- 根据 actionType 调用 AI skill；
- 读取 Workspace context；
- 读取 Theme；
- 读取推荐素材；
- 调用 AI；
- 保存 ContentDraft；
- 记录 usage；
- 返回结果。

---

## 7. Mo Marks 数据模型

Mo Marks 复用并增强 V1.0 `TrademarkAsset`，不要创建新资产表。

---

## 7.1 TrademarkAsset 增强建议

### 7.1.1 当前原则

- 继续复用 `TrademarkAsset`；
- 不创建 `TrademarkAssetV2`；
- 增强字段分 Sprint 新增；
- 如果字段过多，可新增关联模型，不强行塞进主表。

### 7.1.2 建议新增字段

```prisma
enum TrademarkAssetPurpose {
  own
  client
  for_sale
  platform_reserved
}

enum TrademarkSaleStatus {
  not_for_sale
  preparing
  available
  reserved
  sold
}

enum TrademarkAssetSourceType {
  manual
  import
  platform
  brain_reserved
}

enum TrademarkAssetVisibility {
  private
  organization
  shared
  public_listing
}
```

字段建议：

```prisma
assetPurpose       TrademarkAssetPurpose?
saleStatus         TrademarkSaleStatus?
sourceType         TrademarkAssetSourceType?
visibility         TrademarkAssetVisibility?
askingPrice        Decimal?
askingCurrency     String?
logoMediaAssetId   String?
externalDataStatus String?
lastStatusCheckedAt DateTime?
```

### 7.1.3 注意

如现有 `TrademarkAsset` 已有相似字段，优先复用，不重复。

---

## 7.2 TrademarkImportBatch

### 7.2.1 作用

记录商标导入批次。

```prisma
model TrademarkImportBatch {
  id             String                    @id @default(cuid())
  userId         String
  sourceType     TrademarkImportSourceType
  fileName       String?
  status         TrademarkImportBatchStatus @default(pending)
  totalRows      Int                       @default(0)
  successRows    Int                       @default(0)
  failedRows     Int                       @default(0)
  metadata       Json?
  createdAt      DateTime                  @default(now())
  updatedAt      DateTime                  @updatedAt

  user           User                      @relation(fields: [userId], references: [id], onDelete: Cascade)
  rows           TrademarkImportRow[]

  @@index([userId])
  @@map("trademark_import_batches")
}

enum TrademarkImportSourceType {
  csv
  excel
  paste
  manual_batch
}

enum TrademarkImportBatchStatus {
  pending
  previewed
  imported
  failed
  cancelled
}
```

---

## 7.3 TrademarkImportRow

```prisma
model TrademarkImportRow {
  id             String                   @id @default(cuid())
  batchId        String
  rowIndex       Int
  rawData        Json
  parsedData     Json?
  status         TrademarkImportRowStatus @default(pending)
  errorMessage   String?
  trademarkAssetId String?
  createdAt      DateTime                 @default(now())

  batch          TrademarkImportBatch      @relation(fields: [batchId], references: [id], onDelete: Cascade)
  trademarkAsset TrademarkAsset?           @relation(fields: [trademarkAssetId], references: [id], onDelete: SetNull)

  @@index([batchId])
  @@map("trademark_import_rows")
}

enum TrademarkImportRowStatus {
  pending
  valid
  invalid
  imported
  skipped
}
```

---

## 7.4 TrademarkListing

### 7.4.1 作用

保存单商标销售页配置。

```prisma
model TrademarkListing {
  id               String                 @id @default(cuid())
  userId           String
  trademarkAssetId String
  title            String
  subtitle         String?
  slug             String?
  shareCode        String                 @unique
  status           TrademarkListingStatus @default(draft)
  sellingPoints    Json?
  targetIndustries Json?
  targetCustomers  Json?
  brandStory       String?
  priceText        String?
  askingPrice      Decimal?
  askingCurrency   String?
  riskNotes        Json?
  faq              Json?
  contactBlock     Json?
  publishedAt      DateTime?
  metadata         Json?
  createdAt        DateTime               @default(now())
  updatedAt        DateTime               @updatedAt

  user             User                   @relation(fields: [userId], references: [id], onDelete: Cascade)
  trademarkAsset   TrademarkAsset          @relation(fields: [trademarkAssetId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@index([trademarkAssetId])
  @@map("trademark_listings")
}

enum TrademarkListingStatus {
  draft
  published
  archived
}
```

---

## 7.5 TrademarkListingMedia

```prisma
model TrademarkListingMedia {
  id        String        @id @default(cuid())
  listingId String
  assetId   String
  role      ListingMediaRole
  sortOrder Int           @default(0)
  metadata  Json?
  createdAt DateTime      @default(now())

  listing   TrademarkListing @relation(fields: [listingId], references: [id], onDelete: Cascade)
  asset     MediaAsset       @relation(fields: [assetId], references: [id], onDelete: Cascade)

  @@index([listingId])
  @@index([assetId])
  @@map("trademark_listing_media")
}

enum ListingMediaRole {
  logo
  cover
  illustration
  evidence
  background
}
```

---

## 7.6 TrademarkRecommendationPage

### 7.6.1 作用

保存多商标推荐页。

```prisma
model TrademarkRecommendationPage {
  id              String                            @id @default(cuid())
  userId          String
  title           String
  description     String?
  shareCode       String                            @unique
  status          TrademarkRecommendationPageStatus @default(draft)
  targetCustomerName String?
  targetIndustry  String?
  budgetRange     String?
  pageType        RecommendationPageType            @default(custom)
  introCopy       String?
  closingCopy     String?
  contactBlock    Json?
  publishedAt     DateTime?
  metadata        Json?
  createdAt       DateTime                          @default(now())
  updatedAt       DateTime                          @updatedAt

  user            User                              @relation(fields: [userId], references: [id], onDelete: Cascade)
  items           TrademarkRecommendationPageItem[]

  @@index([userId])
  @@map("trademark_recommendation_pages")
}

enum TrademarkRecommendationPageStatus {
  draft
  published
  archived
}

enum RecommendationPageType {
  custom
  industry
  category
  budget
  customer
}
```

---

## 7.7 TrademarkRecommendationPageItem

```prisma
model TrademarkRecommendationPageItem {
  id              String                     @id @default(cuid())
  pageId          String
  trademarkAssetId String
  listingId       String?
  sortOrder       Int                        @default(0)
  recommendationReason String?
  highlighted     Boolean                    @default(false)
  metadata        Json?
  createdAt       DateTime                   @default(now())

  page            TrademarkRecommendationPage @relation(fields: [pageId], references: [id], onDelete: Cascade)
  trademarkAsset  TrademarkAsset              @relation(fields: [trademarkAssetId], references: [id], onDelete: Cascade)
  listing         TrademarkListing?           @relation(fields: [listingId], references: [id], onDelete: SetNull)

  @@index([pageId])
  @@index([trademarkAssetId])
  @@map("trademark_recommendation_page_items")
}
```

---

## 7.8 TrademarkInquiry

```prisma
model TrademarkInquiry {
  id              String                 @id @default(cuid())
  userId          String?
  pageId          String?
  listingId       String?
  trademarkAssetId String?
  name            String?
  phone           String?
  email           String?
  wechat          String?
  message         String?
  sourceType      TrademarkInquirySource
  status          TrademarkInquiryStatus @default(new)
  opportunityId   String?
  metadata        Json?
  createdAt       DateTime               @default(now())
  updatedAt       DateTime               @updatedAt

  user            User?                  @relation(fields: [userId], references: [id], onDelete: SetNull)
  page            TrademarkRecommendationPage? @relation(fields: [pageId], references: [id], onDelete: SetNull)
  listing         TrademarkListing?      @relation(fields: [listingId], references: [id], onDelete: SetNull)
  trademarkAsset  TrademarkAsset?        @relation(fields: [trademarkAssetId], references: [id], onDelete: SetNull)
  opportunity     Opportunity?           @relation(fields: [opportunityId], references: [id], onDelete: SetNull)

  @@index([userId])
  @@index([pageId])
  @@index([listingId])
  @@map("trademark_inquiries")
}

enum TrademarkInquirySource {
  listing_page
  recommendation_page
  manual
}

enum TrademarkInquiryStatus {
  new
  contacted
  converted
  closed
}
```

---

## 8. Mo Global 数据模型

Mo Global 复用 V1.0 MGSN `CountryService` 和 `CountryPrice`。

---

## 8.1 UserPriceRule

### 8.1.1 作用

保存用户报价规则。

```prisma
model UserPriceRule {
  id              String                @id @default(cuid())
  userId          String
  name            String
  ruleType        UserPriceRuleType
  jurisdiction    String?
  serviceType     String?
  markupPercent   Float?
  fixedMarkup      Decimal?
  minimumFee       Decimal?
  currency         String               @default("USD")
  roundingRule     String?
  status           UserPriceRuleStatus  @default(active)
  metadata         Json?
  createdAt        DateTime             @default(now())
  updatedAt        DateTime             @updatedAt

  user             User                 @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@map("user_price_rules")
}

enum UserPriceRuleType {
  percentage_markup
  fixed_markup
  mixed
  manual
}

enum UserPriceRuleStatus {
  active
  archived
}
```

---

## 8.2 QuotePlan

### 8.2.1 作用

保存一次客户报价方案。

```prisma
model QuotePlan {
  id              String          @id @default(cuid())
  userId          String
  customerId      String?
  opportunityId   String?
  orderId         String?
  title           String
  trademarkName   String?
  classes         String?
  goodsServices   String?
  targetCountries Json?
  customerNeed    String?
  status          QuotePlanStatus @default(draft)
  totalCost        Decimal?
  totalPrice       Decimal?
  currency         String         @default("USD")
  internalNotes    String?
  customerCopy     String?
  riskNotes        Json?
  materials        Json?
  timelineNotes    Json?
  shareCode        String?        @unique
  publishedAt      DateTime?
  metadata         Json?
  createdAt        DateTime       @default(now())
  updatedAt        DateTime       @updatedAt

  user             User           @relation(fields: [userId], references: [id], onDelete: Cascade)
  customer         Customer?      @relation(fields: [customerId], references: [id], onDelete: SetNull)
  opportunity      Opportunity?   @relation(fields: [opportunityId], references: [id], onDelete: SetNull)
  order            Order?         @relation(fields: [orderId], references: [id], onDelete: SetNull)
  items            QuotePlanItem[]
  proposals        QuoteProposal[]

  @@index([userId])
  @@index([customerId])
  @@index([opportunityId])
  @@map("quote_plans")
}

enum QuotePlanStatus {
  draft
  generated
  shared
  accepted
  converted_to_order
  archived
}
```

---

## 8.3 QuotePlanItem

```prisma
model QuotePlanItem {
  id              String      @id @default(cuid())
  quotePlanId     String
  countryCode     String
  countryName     String?
  serviceType     String?
  classCount      Int?
  officialFee     Decimal?
  serviceFeeCost  Decimal?
  platformCost    Decimal?
  userPrice       Decimal?
  currency        String      @default("USD")
  materials       Json?
  timeline         String?
  riskNotes       Json?
  metadata        Json?
  createdAt       DateTime    @default(now())

  quotePlan       QuotePlan   @relation(fields: [quotePlanId], references: [id], onDelete: Cascade)

  @@index([quotePlanId])
  @@map("quote_plan_items")
}
```

---

## 8.4 QuoteProposal

```prisma
model QuoteProposal {
  id             String              @id @default(cuid())
  quotePlanId    String
  userId         String
  title          String?
  customerCopy   String?
  internalCopy   String?
  status         QuoteProposalStatus @default(draft)
  shareCode      String?             @unique
  copiedAt       DateTime?
  sharedAt       DateTime?
  metadata       Json?
  createdAt      DateTime            @default(now())
  updatedAt      DateTime            @updatedAt

  quotePlan      QuotePlan           @relation(fields: [quotePlanId], references: [id], onDelete: Cascade)
  user           User                @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([quotePlanId])
  @@index([userId])
  @@map("quote_proposals")
}

enum QuoteProposalStatus {
  draft
  generated
  shared
  accepted
  archived
}
```

---

## 9. Mo Leads 数据模型

Mo Leads 复用 V1.0 `Opportunity` 和 `OpportunityFollowup`。

新增模型只处理营销活动、话术草稿和沟通记录。

---

## 9.1 OpportunityCampaign

```prisma
model OpportunityCampaign {
  id          String                    @id @default(cuid())
  userId      String
  title       String
  campaignType OpportunityCampaignType
  goal        String?
  status      OpportunityCampaignStatus @default(draft)
  metadata    Json?
  createdAt   DateTime                  @default(now())
  updatedAt   DateTime                  @updatedAt

  user        User                      @relation(fields: [userId], references: [id], onDelete: Cascade)
  recipients  CampaignRecipient[]
  drafts      MessageDraft[]

  @@index([userId])
  @@map("opportunity_campaigns")
}

enum OpportunityCampaignType {
  followup
  quote_followup
  trademark_recommendation
  renewal_reminder
  holiday_greeting
  content_distribution
}

enum OpportunityCampaignStatus {
  draft
  generated
  in_progress
  completed
  archived
}
```

---

## 9.2 CampaignRecipient

```prisma
model CampaignRecipient {
  id             String                    @id @default(cuid())
  campaignId      String
  opportunityId   String?
  customerId      String?
  status          CampaignRecipientStatus  @default(pending)
  metadata        Json?
  createdAt       DateTime                 @default(now())
  updatedAt       DateTime                 @updatedAt

  campaign        OpportunityCampaign      @relation(fields: [campaignId], references: [id], onDelete: Cascade)
  opportunity     Opportunity?             @relation(fields: [opportunityId], references: [id], onDelete: SetNull)
  customer        Customer?                @relation(fields: [customerId], references: [id], onDelete: SetNull)

  @@index([campaignId])
  @@index([opportunityId])
  @@map("campaign_recipients")
}

enum CampaignRecipientStatus {
  pending
  drafted
  copied
  marked_sent
  replied
  converted
  skipped
}
```

---

## 9.3 MessageDraft

```prisma
model MessageDraft {
  id             String             @id @default(cuid())
  userId          String
  campaignId      String?
  opportunityId   String?
  customerId      String?
  quotePlanId     String?
  recommendationPageId String?
  channel         MessageChannel
  subject         String?
  body            String
  status          MessageDraftStatus @default(draft)
  copiedAt        DateTime?
  markedSentAt    DateTime?
  aiSkillRunId    String?
  metadata        Json?
  createdAt       DateTime           @default(now())
  updatedAt       DateTime           @updatedAt

  user            User               @relation(fields: [userId], references: [id], onDelete: Cascade)
  campaign        OpportunityCampaign? @relation(fields: [campaignId], references: [id], onDelete: SetNull)
  opportunity     Opportunity?        @relation(fields: [opportunityId], references: [id], onDelete: SetNull)
  customer        Customer?           @relation(fields: [customerId], references: [id], onDelete: SetNull)
  quotePlan       QuotePlan?          @relation(fields: [quotePlanId], references: [id], onDelete: SetNull)
  recommendationPage TrademarkRecommendationPage? @relation(fields: [recommendationPageId], references: [id], onDelete: SetNull)
  aiSkillRun      AISkillRun?         @relation(fields: [aiSkillRunId], references: [id], onDelete: SetNull)

  @@index([userId])
  @@index([opportunityId])
  @@index([campaignId])
  @@map("message_drafts")
}

enum MessageChannel {
  wechat
  email
  sms
  phone
  whatsapp
  other
}

enum MessageDraftStatus {
  draft
  copied
  marked_sent
  archived
}
```

---

## 9.4 CommunicationLog

```prisma
model CommunicationLog {
  id             String               @id @default(cuid())
  userId          String
  opportunityId   String?
  customerId      String?
  messageDraftId  String?
  channel         MessageChannel
  direction       CommunicationDirection @default(outbound)
  summary         String?
  content         String?
  nextActionAt    DateTime?
  metadata        Json?
  createdAt       DateTime             @default(now())

  user            User                 @relation(fields: [userId], references: [id], onDelete: Cascade)
  opportunity     Opportunity?          @relation(fields: [opportunityId], references: [id], onDelete: SetNull)
  customer        Customer?             @relation(fields: [customerId], references: [id], onDelete: SetNull)
  messageDraft    MessageDraft?         @relation(fields: [messageDraftId], references: [id], onDelete: SetNull)

  @@index([userId])
  @@index([opportunityId])
  @@index([customerId])
  @@map("communication_logs")
}

enum CommunicationDirection {
  inbound
  outbound
}
```

---

## 10. Workflow Lite Runtime 预留模型

该部分可在 Sprint 7 或 Lite 1.2 实现，但数据架构应提前规划。

---

## 10.1 WorkflowDefinition

```prisma
model WorkflowDefinition {
  id             String                 @id @default(cuid())
  code           String                 @unique
  name           String
  description    String?
  triggerType    WorkflowTriggerType
  definitionJson Json
  status         WorkflowDefinitionStatus @default(active)
  createdAt      DateTime               @default(now())
  updatedAt      DateTime               @updatedAt

  runs           WorkflowRun[]

  @@map("workflow_definitions")
}

enum WorkflowTriggerType {
  manual
  event
  scheduled
  guide
}

enum WorkflowDefinitionStatus {
  active
  archived
  disabled
}
```

---

## 10.2 WorkflowRun

```prisma
model WorkflowRun {
  id                   String            @id @default(cuid())
  workflowDefinitionId  String
  userId                String
  objectType            String?
  objectId              String?
  status                WorkflowRunStatus @default(running)
  startedAt             DateTime          @default(now())
  completedAt           DateTime?
  metadata              Json?

  workflowDefinition    WorkflowDefinition @relation(fields: [workflowDefinitionId], references: [id], onDelete: Cascade)
  user                  User               @relation(fields: [userId], references: [id], onDelete: Cascade)
  steps                 WorkflowStepRun[]

  @@index([userId])
  @@index([workflowDefinitionId])
  @@map("workflow_runs")
}

enum WorkflowRunStatus {
  running
  waiting_review
  completed
  failed
  cancelled
}
```

---

## 10.3 WorkflowStepRun

```prisma
model WorkflowStepRun {
  id            String                @id @default(cuid())
  workflowRunId String
  stepCode      String
  capabilityCode String?
  status        WorkflowStepRunStatus @default(pending)
  inputJson     Json?
  outputJson    Json?
  errorMessage  String?
  startedAt     DateTime?
  completedAt   DateTime?
  metadata      Json?

  workflowRun   WorkflowRun           @relation(fields: [workflowRunId], references: [id], onDelete: Cascade)

  @@index([workflowRunId])
  @@index([capabilityCode])
  @@map("workflow_step_runs")
}

enum WorkflowStepRunStatus {
  pending
  running
  waiting_review
  completed
  failed
  skipped
}
```

---

## 11. Capability Catalog 预留

V1.1 可先用 Markdown / seed 配置管理 Capability，不一定马上建表。

如需要建表，可采用以下轻量模型。

---

## 11.1 CapabilityDefinition

```prisma
model CapabilityDefinition {
  id            String              @id @default(cuid())
  code          String              @unique
  name          String
  category      CapabilityCategory
  description   String?
  inputSchema   Json?
  outputSchema  Json?
  dependsOn     Json?
  reviewPolicy  Json?
  status        CapabilityStatus    @default(active)
  metadata      Json?
  createdAt     DateTime            @default(now())
  updatedAt     DateTime            @updatedAt

  @@map("capability_definitions")
}

enum CapabilityCategory {
  workspace
  content
  asset
  trademark
  global_quote
  leads
  guide
  flow
}

enum CapabilityStatus {
  active
  draft
  archived
}
```

---

## 11.2 V1.1 最小 Capability

建议 seed 或文档管理以下 Capability：

### Workspace

- ManageBusinessProfile
- ManagePersona
- ManageKnowledge
- ManageContentPreference
- BuildWorkspaceContext

### Content

- RecommendDailyTopics
- CreateCustomTopic
- RecommendTopicAssets
- GenerateGraphicBrief
- GenerateGraphicCopy
- GenerateVideoScript
- GeneratePrivateChatCopy
- RecordContentUsage

### Asset

- UploadMediaAsset
- ClassifyMediaAsset
- RecommendMediaAsset
- RecordAssetUsage

### Trademark

- ImportTrademarkAssets
- ClassifyTrademarkAsset
- PackageTrademarkForSale
- GenerateTrademarkSalesPage
- GenerateTrademarkRecommendationPage
- ConvertInquiryToOpportunity

### Global Quote

- SearchCountryService
- ApplyUserPriceRule
- GenerateQuotePlan
- GenerateQuoteProposal
- ConvertQuoteToOrder

### Leads

- GenerateLeadFollowup
- RecordCommunication
- ConvertLeadToQuote
- ConvertLeadToOrder

---

## 12. 服务层架构

建议新增以下服务目录：

```text
lib/workspace/
  workspaceService.ts
  workspaceContextBuilder.ts

lib/brain/
  brainConnector.ts
  disabledBrainConnector.ts

lib/content/
  themeEngine.ts
  contentDraftService.ts
  contentUsageService.ts

lib/assets/
  mediaAssetService.ts
  templateAssetService.ts
  assetRecommendationService.ts

lib/assistant/
  contentActionEngine.ts
  customerReplyEngine.ts

lib/marks/
  trademarkImportService.ts
  trademarkListingService.ts
  recommendationPageService.ts
  trademarkInquiryService.ts

lib/global/
  quoteEngine.ts
  priceRuleService.ts
  quotePlanService.ts

lib/leads/
  leadActionService.ts
  messageDraftService.ts
  communicationLogService.ts

lib/workflows/
  workflowDefinitionService.ts
  workflowRunService.ts
```

---

## 12.1 WorkspaceContextBuilder

职责：

- 获取用户业务资料；
- 获取默认 Persona；
- 获取 Knowledge；
- 获取内容偏好；
- 获取 BrainConnection；
- 获取相关素材；
- 为 AI 生成提供上下文。

导出：

```ts
buildWorkspaceContext(userId: string, options?: WorkspaceContextOptions)
```

---

## 12.2 ThemeEngine

职责：

- 主题推荐；
- 主题匹配用户偏好；
- 主题关联素材；
- 记录主题使用；
- 自建主题生成。

V1.1 推荐逻辑先规则化，不做复杂模型。

---

## 12.3 AssetRecommendationService

职责：

- 根据主题推荐素材；
- 根据内容类型推荐模板；
- 根据商标销售页推荐 logo / 背景；
- 根据报价方案推荐国家服务图；
- 记录素材使用。

---

## 12.4 ContentActionEngine

职责：

- 生成图文；
- 生成视频脚本；
- 生成私聊话术；
- 保存 ContentDraft；
- 关联 Theme；
- 关联 MediaAsset；
- 记录 AISkillRun / TokenLog。

---

## 12.5 QuoteEngine

职责：

- 读取 CountryService / CountryPrice；
- 应用 UserPriceRule；
- 生成 QuotePlan；
- 生成 QuotePlanItem；
- 调用 AI 生成 QuoteProposal；
- 转 Markreg Order。

---

## 12.6 LeadActionService

职责：

- 获取今日待跟进；
- 批量生成 MessageDraft；
- 关联 QuotePlan / RecommendationPage；
- 创建 CommunicationLog；
- 转 QuotePlan；
- 转 Order。

---

## 13. API 设计

API 命名应贴近产品模块。

---

## 13.1 Workspace API

```text
GET    /api/lite/workspace
PATCH  /api/lite/workspace/profile

GET    /api/lite/workspace/personas
POST   /api/lite/workspace/personas
PATCH  /api/lite/workspace/personas/:id

GET    /api/lite/workspace/knowledge
POST   /api/lite/workspace/knowledge
PATCH  /api/lite/workspace/knowledge/:id
DELETE /api/lite/workspace/knowledge/:id

GET    /api/lite/workspace/preferences
PATCH  /api/lite/workspace/preferences

GET    /api/lite/workspace/brain-connection
```

---

## 13.2 Content API

```text
GET    /api/lite/content/themes
POST   /api/lite/content/themes
GET    /api/lite/content/themes/today
GET    /api/lite/content/themes/:id
POST   /api/lite/content/themes/:id/use
POST   /api/lite/content/themes/:id/ignore

GET    /api/lite/content/drafts
POST   /api/lite/content/drafts
GET    /api/lite/content/drafts/:id
PATCH  /api/lite/content/drafts/:id
POST   /api/lite/content/drafts/:id/copy
POST   /api/lite/content/drafts/:id/archive
```

---

## 13.3 Asset API

```text
GET    /api/lite/assets/media
POST   /api/lite/assets/media
GET    /api/lite/assets/media/:id
PATCH  /api/lite/assets/media/:id
DELETE /api/lite/assets/media/:id
POST   /api/lite/assets/media/:id/use

GET    /api/lite/assets/templates
GET    /api/lite/assets/templates/:id
```

注意：如已有 `/api/lite/assets` 资产接口，要避免命名冲突，可使用 `/api/lite/media-assets`。

---

## 13.4 Assistant API

```text
POST /api/lite/assistant/generate-graphic-copy
POST /api/lite/assistant/generate-video-script
POST /api/lite/assistant/generate-private-chat
POST /api/lite/assistant/customer-reply
POST /api/lite/assistant/recommend-assets
```

---

## 13.5 Marks API

```text
GET    /api/lite/marks
POST   /api/lite/marks
POST   /api/lite/marks/import/preview
POST   /api/lite/marks/import/commit
PATCH  /api/lite/marks/:id
POST   /api/lite/marks/:id/package
POST   /api/lite/marks/:id/mark-for-sale

GET    /api/lite/marks/listings
POST   /api/lite/marks/listings
GET    /api/lite/marks/listings/:id
PATCH  /api/lite/marks/listings/:id
POST   /api/lite/marks/listings/:id/publish

GET    /api/lite/marks/recommendation-pages
POST   /api/lite/marks/recommendation-pages
GET    /api/lite/marks/recommendation-pages/:id
PATCH  /api/lite/marks/recommendation-pages/:id
POST   /api/lite/marks/recommendation-pages/:id/publish

POST   /api/public/trademark-inquiries
```

---

## 13.6 Global API

```text
GET    /api/lite/global/country-services
GET    /api/lite/global/country-prices

GET    /api/lite/global/price-rules
POST   /api/lite/global/price-rules
PATCH  /api/lite/global/price-rules/:id
DELETE /api/lite/global/price-rules/:id

GET    /api/lite/global/quote-plans
POST   /api/lite/global/quote-plans
GET    /api/lite/global/quote-plans/:id
PATCH  /api/lite/global/quote-plans/:id
POST   /api/lite/global/quote-plans/:id/generate-proposal
POST   /api/lite/global/quote-plans/:id/share
POST   /api/lite/global/quote-plans/:id/convert-order
```

---

## 13.7 Leads API

```text
GET    /api/lite/leads/today
GET    /api/lite/leads/campaigns
POST   /api/lite/leads/campaigns
GET    /api/lite/leads/campaigns/:id
POST   /api/lite/leads/campaigns/:id/generate-messages

GET    /api/lite/leads/message-drafts
PATCH  /api/lite/leads/message-drafts/:id
POST   /api/lite/leads/message-drafts/:id/copy
POST   /api/lite/leads/message-drafts/:id/mark-sent

POST   /api/lite/leads/communication-logs
POST   /api/lite/leads/:id/convert-quote
POST   /api/lite/leads/:id/convert-order
```

---

## 14. 页面结构

### 14.1 Lite 导航

```text
今日工作台
Mo Workspace
Mo Content
  今日选题
  内容草稿
  素材库
  模板库
Mo Assistant
  写图文
  写视频脚本
  回客户
Mo Marks
  商标资产
  待售商标
  推荐页
  询盘
Mo Global
  国家服务
  报价规则
  报价方案
Mo Leads
  今日跟进
  商机列表
  营销草稿
订单中心
Partner Center
Token 中心
设置
```

### 14.2 兼容旧路由

- `/lite/assets` 继续可访问，逐步迁移到 Mo Marks；
- `/lite/ai` 继续可访问，逐步迁移到 Mo Assistant；
- `/lite/opportunities` 继续可访问，逐步迁移到 Mo Leads；
- 不删除旧路由；
- 不出现无效 `#` 链接。

---

## 15. 权限设计

### 15.1 权限原则

所有 API 必须服务端校验：

- 当前用户是否登录；
- 当前用户是否属于组织；
- 当前用户是否拥有对象；
- Admin 是否有管理权限；
- public shareCode 页面是否仅展示公开字段。

### 15.2 私有对象校验

私有对象必须按 `userId` 或 `ownerUserId` 校验：

- UserBusinessProfile；
- UserPersona；
- UserKnowledgeDocument；
- UserContentPreference；
- ContentDraft；
- MediaAsset private；
- TrademarkListing；
- TrademarkRecommendationPage；
- QuotePlan；
- QuoteProposal；
- OpportunityCampaign；
- MessageDraft；
- CommunicationLog。

### 15.3 分享页

分享页通过 `shareCode` 访问，只展示 public-safe 字段。

不得显示：

- internalNotes；
- 成本价；
- 服务商信息；
- 用户报价规则；
- 私有客户资料；
- 私有商机；
- Token；
- Commission。

---

## 16. AuditLog 设计

关键 action：

```text
workspace.profile.update
persona.create
persona.update
knowledge.create
knowledge.update
knowledge.delete

content_theme.create
content_theme.select
content_theme.ignore
content_theme.use
content_draft.generate
content_draft.copy
content_draft.export

media_asset.upload
media_asset.update
media_asset.delete
media_asset.use
template_asset.create
template_asset.update

trademark.import
trademark.classify
trademark.package
trademark_listing.create
trademark_listing.update
trademark_listing.publish
recommendation_page.create
recommendation_page.update
recommendation_page.publish
trademark_inquiry.create
trademark_inquiry.convert_to_opportunity

quote_rule.create
quote_rule.update
quote_plan.create
quote_plan.update
quote_plan.share
quote_plan.convert_order

lead_campaign.create
lead_campaign.generate_messages
message_draft.copy
message_draft.mark_sent
communication_log.create
opportunity.convert_to_quote
opportunity.convert_to_order

permission.denied
```

---

## 17. Migration 策略

### 17.1 Sprint 分段 migration

建议 migration：

```text
v11_sprint0_workspace
v11_sprint1_content_assets
v11_sprint2_assistant_drafts
v11_sprint3_marks_import
v11_sprint4_marks_listings_recommendations
v11_sprint5_global_quotes
v11_sprint6_leads_campaigns
v11_sprint7_workflow_runtime
```

### 17.2 每个 Sprint 原则

- 只新增当前 Sprint 需要的模型；
- 不提前建过多表；
- 不修改历史 migration；
- 不 reset 开发库，除非明确确认；
- 每个 Sprint 都要通过 Prisma validate / generate / typecheck / build。

---

## 18. Seed 策略

### 18.1 Sprint 0 Seed

创建：

- UserBusinessProfile；
- 默认 UserPersona；
- UserKnowledgeBase；
- 3-5 条 UserKnowledgeDocument；
- UserContentPreference；
- BrainConnection disabled。

### 18.2 Sprint 1 Seed

创建：

- 20-30 个 ContentTheme；
- 3-5 个节假日主题；
- 5-10 个商标冷知识主题；
- 5-10 个服务营销主题；
- 10 个 MediaAsset 平台素材；
- 5 个 TemplateAsset 模板；
- TopicAssetMapping。

### 18.3 Sprint 3/4 Seed

创建：

- 示例待售商标；
- 示例 TrademarkListing；
- 示例 RecommendationPage；
- 示例 Inquiry。

### 18.4 Sprint 5 Seed

创建：

- 示例 UserPriceRule；
- 示例 QuotePlan。

### 18.5 Sprint 6 Seed

创建：

- 示例 OpportunityCampaign；
- 示例 MessageDraft。

---

## 19. 技术验收命令

每个 Sprint 完成后必须执行：

```bash
npm run prisma:validate
npm run prisma:generate
npm run typecheck
npm run build
npx prisma migrate status
npm run prisma:seed
```

如出现 Next/TS 缓存问题，可清理：

```powershell
Remove-Item -Recurse -Force .next -ErrorAction SilentlyContinue
Remove-Item -Force tsconfig.tsbuildinfo -ErrorAction SilentlyContinue
```

---

## 20. 风险与控制

### 20.1 范围膨胀风险

控制：

- V1.1 不做真实 Mo Brain；
- V1.1 不做视频成片；
- V1.1 不做真实群发；
- V1.1 不做自动采集；
- V1.1 不做完整小程序。

### 20.2 数据模型膨胀风险

控制：

- 复用 V1.0；
- 分 Sprint 建表；
- 不提前建大而全模型；
- 复杂字段先 Json；
- 稳定后再规范化。

### 20.3 素材版权风险

控制：

- 记录 sourceUrl / sourceName / rightsNote；
- 用户上传默认 private；
- 用户自行保证权利；
- 平台素材优先自制或可商用。

### 20.4 AI 误导风险

控制：

- 法律内容提示人工复核；
- 报价以最终确认为准；
- AI 输出保留风险提示；
- 高风险动作不自动执行。

### 20.5 分享页泄露风险

控制：

- 分享页只展示 public-safe 字段；
- 不展示成本价；
- 不展示内部备注；
- 不展示客户私有资料。

---

## 21. 最终架构结论

MarkOrbit Lite 1.1 的数据模型应围绕以下主线建设：

```text
Workspace Context
  ↓
Content Theme + Asset
  ↓
AI Business Action
  ↓
Draft / Listing / Quote / Message
  ↓
Share / Inquiry / Follow-up / Order
```

核心判断：

> **Lite 1.1 不是重建系统，而是在 V1.0 之上增加 Mo 应用层能力。**

数据模型设计必须坚持：

- User / Customer / Order / Opportunity 复用；
- TrademarkAsset 复用并增强；
- CountryService / CountryPrice 复用；
- AISkillRun / TokenLog 复用；
- AuditLog 复用；
- 新增模型只服务于 Workspace、Content、Asset、Marks、Global、Leads 和 Workflow 预留；
- Mo Brain 不真实接入，只预留。

---

## 22. 下一步

本数据模型与架构设计确认后，应继续输出：

1. `MarkOrbit Lite 1.1 Sprint 0 Codex 开发提示词`
2. `MarkOrbit Lite 1.1 Sprint 1 Codex 开发提示词：Mo Content Foundation`

Sprint 0 需要基于本设计更新：

- 今日工作台采用“五个今日”；
- Workspace 增加素材库完整度占位；
- 预留 Mo Content / Mo Asset Hub 入口；
- 不开发真实素材库；
- 不开发真实主题引擎；
- 不接 Mo Brain。
