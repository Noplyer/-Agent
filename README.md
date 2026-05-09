RiskRadar Agent
企业级 AI 风险预警与舆情洞察平台

RiskRadar Agent 是一个基于 Spring Boot 3 + 多 Agent 协作 + 数据分析看板 构建的企业风险预警系统。
项目面向企业经营、供应链管理、舆情监控、用户投诉分析等场景，帮助企业从大量分散数据中自动发现风险、分析原因，并生成可执行的风险报告。

本项目不是简单的数据展示系统，而是将 AI Agent 思路 引入企业数据分析流程，让系统不仅能回答“发生了什么”，还能进一步分析“为什么发生”和“应该怎么处理”。

项目核心痛点

传统企业数据系统通常存在以下问题：

数据分散
新闻舆情、用户投诉、供应商交付、订单异常等数据分散在不同系统中，人工汇总成本高。
只能展示结果，不能解释原因
普通 BI 报表只能告诉用户“投诉量上升了”“负面舆情增加了”，但不能自动分析背后的原因。
风险发现滞后
很多风险需要人工定期排查，等问题暴露时已经产生较大影响。
报告编写效率低
企业风险报告通常需要人工整理数据、分析趋势、撰写结论，耗时较长。

RiskRadar Agent 的目标是通过多 Agent 协作，让系统自动完成：

风险数据采集
舆情情绪分析
风险事件识别
异常波动检测
多维度原因归因
风险报告生成
运营处理建议输出
核心功能
1. 用户登录与权限认证

系统内置 JWT 登录鉴权，用户登录后才能访问风险数据和分析接口。

默认账号：

管理员账号：admin / admin123
分析员账号：analyst / analyst123

登录成功后，系统会返回 Token，前端请求后续接口时自动携带该 Token。

2. 企业风险看板

风险看板用于展示企业当前整体风险状态，包括：

风险事件总数
高风险事件数量
中风险事件数量
低风险事件数量
负面舆情热度
风险趋势变化
风险类型分布
风险来源分布

用户可以快速了解企业当前风险情况。

3. 风险事件管理

系统支持对风险事件进行管理，包括：

查看风险事件列表
查看风险等级
查看风险来源
查看风险状态
按风险类型筛选
按风险等级筛选
按时间范围查询

风险事件示例：

物流延迟导致客户投诉
产品质量问题引发退货
供应商交付延迟
负面舆情扩散
售后响应速度下降
4. 舆情监测与情绪分析

系统可以对新闻、评论、投诉等文本数据进行分析，识别其中的情绪倾向：

正面
中性
负面

并统计：

负面舆情数量
负面占比
热门负面话题
舆情趋势
舆情来源分布

该功能适合用于企业品牌监控、产品口碑分析和投诉热点发现。

5. 供应商风险评分

系统根据供应商的交付情况、质量问题、合作稳定性等指标，为供应商生成风险评分。

供应商风险指标包括：

风险评分
风险等级
交付及时率
质量合格率
合作年限
主要风险类型

风险等级示例：

高风险
中风险
低风险

企业可以根据评分结果优先关注高风险供应商。

6. 多 Agent 协作分析

项目中设计了多个 Agent 协作完成完整分析流程。

核心 Agent 包括：

Agent	作用
问题理解 Agent	解析用户输入的问题，识别分析对象、时间范围和风险类型
数据检索 Agent	从风险事件、舆情数据、供应商数据中检索相关信息
情绪分析 Agent	判断文本内容的正负面倾向
异常检测 Agent	检测投诉量、舆情热度、供应商延迟率等指标是否异常
归因分析 Agent	结合产品、地区、渠道、时间、供应商等维度分析风险原因
报告生成 Agent	汇总分析结果，生成 Markdown 风险报告
多 Agent 核心流程

用户输入问题后，系统会按照下面的流程进行分析：

用户提问
   ↓
问题理解 Agent
   ↓
数据检索 Agent
   ↓
情绪分析 Agent
   ↓
异常检测 Agent
   ↓
归因分析 Agent
   ↓
报告生成 Agent
   ↓
输出风险摘要、原因分析和处理建议

示例问题：

最近负面舆情主要集中在哪些产品？

系统会自动完成：

识别用户要分析的是“负面舆情”
检索最近一段时间的舆情数据
统计负面内容数量和占比
找出负面舆情集中的产品或话题
分析可能原因
输出处理建议
技术栈
后端
Java 17
Spring Boot 3
Spring Web
Spring Security
JWT
Spring Validation
Spring Data JPA
H2 Database
PostgreSQL
Maven
数据与中间件
MySQL / PostgreSQL
H2 内存数据库
Redis
Kafka
Flink
ClickHouse
Docker
前端
HTML
CSS
JavaScript
Vue 3
ECharts
AI / Agent 设计
多 Agent 协作
长链推理
情绪分析
异常检测
风险归因
自动报告生成
项目目录结构
riskradar-enterprise-mvp
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com.riskradar
│   │   │       ├── RiskRadarApplication.java
│   │   │       ├── config
│   │   │       │   └── SecurityConfig.java
│   │   │       ├── controller
│   │   │       │   ├── AuthController.java
│   │   │       │   ├── DashboardController.java
│   │   │       │   ├── RiskEventController.java
│   │   │       │   ├── SupplierController.java
│   │   │       │   └── AgentController.java
│   │   │       ├── service
│   │   │       │   ├── AuthService.java
│   │   │       │   ├── RiskEventService.java
│   │   │       │   ├── SupplierRiskService.java
│   │   │       │   └── AgentWorkflowService.java
│   │   │       ├── agent
│   │   │       │   ├── QuestionUnderstandingAgent.java
│   │   │       │   ├── DataRetrievalAgent.java
│   │   │       │   ├── SentimentAgent.java
│   │   │       │   ├── AnomalyDetectionAgent.java
│   │   │       │   ├── AttributionAgent.java
│   │   │       │   └── ReportGenerationAgent.java
│   │   │       ├── entity
│   │   │       ├── repository
│   │   │       ├── dto
│   │   │       ├── security
│   │   │       └── common
│   │   └── resources
│   │       ├── application.yml
│   │       ├── data.sql
│   │       ├── schema.sql
│   │       └── static
│   │           ├── index.html
│   │           ├── app.js
│   │           └── style.css
│   └── test
├── pom.xml
├── docker-compose.yml
└── README.md
快速启动
1. 环境要求

运行项目前，请先准备以下环境：

JDK 17+
Maven 3.8+
IDEA 或 VS Code

可选环境：

Docker
PostgreSQL
Redis
Kafka
ClickHouse

如果只是运行 MVP 演示版本，使用默认的 H2 数据库即可，不需要额外安装数据库。

2. 克隆项目
git clone https://github.com/你的用户名/riskradar-agent.git
cd riskradar-agent
3. 启动项目
mvn spring-boot:run

启动成功后，控制台会看到类似信息：

Started RiskRadarApplication in 3.5 seconds
Tomcat started on port 8080
4. 访问系统

浏览器打开：

http://localhost:8080

默认登录账号：

admin / admin123

或者：

analyst / analyst123
使用流程
第一步：登录系统

进入首页后，输入默认账号：

用户名：admin
密码：admin123

登录成功后进入企业风险看板。

第二步：查看风险总览

在风险总览页面可以看到：

风险事件总数
高风险事件数
中风险事件数
低风险事件数
负面舆情热度
风险趋势图
风险类型分布图

该页面适合用来快速判断企业当前风险情况。

第三步：查看风险事件

进入风险事件页面，可以查看系统识别出的风险事件。

每条风险事件通常包含：

事件名称
风险等级
事件来源
事件状态
发现时间
影响范围
处理建议

风险等级越高，代表该事件越需要优先处理。

第四步：查看舆情分析

进入舆情监测页面，可以查看：

舆情总数
负面舆情数
正面舆情数
中性舆情数
负面占比
热门话题
平台分布

该模块主要用于分析用户评价、新闻评论、投诉内容中的情绪变化。

第五步：查看供应商风险

进入供应商风险页面，可以查看不同供应商的风险评分。

示例：

供应商A：87，高风险
供应商B：75，高风险
供应商C：62，中风险
供应商D：58，中风险
供应商E：32，低风险

企业可以根据评分结果对高风险供应商进行重点排查。

第六步：使用 Agent 分析

进入 Agent 分析页面，输入问题：

最近负面舆情主要集中在哪些方面？

或者：

为什么供应商A的风险等级升高？

或者：

帮我生成本周企业风险分析报告

系统会调用多个 Agent 协作分析，并输出完整结果。

输出内容通常包括：

风险摘要
关键指标
异常发现
原因归因
影响范围
处理建议
Markdown 分析报告
API 使用示例
登录接口
POST /api/auth/login
Content-Type: application/json

请求体：

{
  "username": "admin",
  "password": "admin123"
}

返回示例：

{
  "code": 200,
  "message": "登录成功",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiJ9..."
  }
}
获取风险看板数据
GET /api/dashboard/overview
Authorization: Bearer <token>

返回示例：

{
  "code": 200,
  "message": "success",
  "data": {
    "totalRiskEvents": 1258,
    "highRiskEvents": 235,
    "mediumRiskEvents": 687,
    "lowRiskEvents": 336,
    "negativeSentimentRate": 33.56
  }
}
获取风险事件列表
GET /api/risk-events
Authorization: Bearer <token>

支持筛选：

GET /api/risk-events?level=HIGH&type=SUPPLIER
获取供应商风险评分
GET /api/suppliers/risk-score
Authorization: Bearer <token>
执行 Agent 分析
POST /api/agent/analyze
Authorization: Bearer <token>
Content-Type: application/json

请求体：

{
  "question": "最近负面舆情主要集中在哪些产品？"
}

返回示例：

{
  "code": 200,
  "message": "分析完成",
  "data": {
    "summary": "近期负面舆情主要集中在产品质量、物流延迟和售后响应三个方面。",
    "riskLevel": "HIGH",
    "rootCauses": [
      "部分产品批次质量波动",
      "华东地区物流延迟",
      "售后处理响应时间较长"
    ],
    "suggestions": [
      "优先排查高投诉产品批次",
      "临时切换备用物流供应商",
      "增加售后客服排班"
    ],
    "report": "## 企业风险分析报告..."
  }
}
Agent 分析报告示例

系统可以自动生成类似下面的 Markdown 报告：

# 企业风险分析报告

## 一、风险摘要

本周期内企业风险事件数量较上周有所上升，其中高风险事件主要集中在产品质量、物流延迟和负面舆情扩散三个方面。

## 二、关键指标

- 风险事件总数：1258
- 高风险事件：235
- 负面舆情占比：33.56%
- 高风险供应商数量：6

## 三、异常发现

系统检测到最近 7 天投诉量和负面舆情热度均出现明显上升，其中华东地区和电商平台渠道增长最明显。

## 四、原因归因

结合产品、地区、渠道和供应商维度分析，风险上升可能与以下因素有关：

1. 部分产品批次质量问题导致退货增加
2. 供应商交付延迟影响订单履约
3. 社交媒体中负面内容传播速度较快
4. 售后响应不及时导致用户不满扩大

## 五、处理建议

1. 优先排查高投诉产品批次
2. 对高风险供应商进行临时风险复核
3. 增加客服排班，提高售后响应速度
4. 对负面舆情进行主动回应和解释
数据库说明

默认情况下，项目使用 H2 内存数据库，启动时会自动初始化演示数据。

H2 控制台地址：

http://localhost:8080/h2-console

默认配置示例：

JDBC URL: jdbc:h2:mem:riskradar
Username: sa
Password:

如果需要切换到 PostgreSQL，可以修改 application.yml 中的数据源配置。

Docker Compose 启动

如果项目中包含 docker-compose.yml，可以使用下面命令启动相关服务：

docker compose up -d

常见服务包括：

PostgreSQL
Redis
Kafka
ClickHouse

启动后再运行 Spring Boot 项目：

mvn spring-boot:run
项目亮点
1. 企业级分层架构

项目按照标准后端结构进行分层：

Controller 层：处理 HTTP 请求
Service 层：处理业务逻辑
Repository 层：访问数据库
Agent 层：处理智能分析逻辑
DTO 层：封装请求和响应数据
Security 层：处理 JWT 鉴权
Common 层：统一响应和异常处理

代码结构清晰，便于扩展和维护。

2. 多 Agent 协作机制

系统不是单个模型直接回答，而是将一个复杂问题拆解成多个步骤：

理解问题 → 检索数据 → 情绪分析 → 异常检测 → 原因归因 → 报告生成

每个 Agent 负责一个明确任务，最终形成完整分析链路。

3. 长链推理能力

项目支持从多个维度分析风险原因，例如：

时间维度
地区维度
产品维度
渠道维度
供应商维度
用户投诉维度
舆情传播维度

通过多维度组合分析，系统可以给出更接近真实业务的风险归因结果。

4. 自动报告生成

系统可以将分析结果自动整理成 Markdown 风险报告，适合用于：

周报
月报
企业风险复盘
供应商风险评估
舆情分析汇报

减少人工整理数据和写报告的时间。

5. 适合继续扩展

该 MVP 可以继续扩展为完整企业级平台，例如：

接入真实大模型 API
接入 Kafka 实时数据流
接入 Flink 实时计算任务
接入 ClickHouse 分析型数据库
增加权限角色管理
增加告警通知
增加邮件报告推送
增加多租户企业管理
增加 RAG 知识库问答
后续优化方向
接入真实大模型
可以接入 OpenAI、通义千问、智谱、DeepSeek 等模型，用于更强的自然语言分析和报告生成。
接入真实数据流
使用 Kafka 接入订单、投诉、评论、新闻等实时数据。
使用 Flink 实时计算
对风险指标进行实时统计和异常检测。
使用 ClickHouse 存储分析数据
提升大规模数据查询性能。
增加告警通知
高风险事件出现时，自动通过邮件、短信或企业微信通知负责人。
增加 RAG 企业知识库
将企业制度、历史报告、处理方案接入知识库，让 Agent 生成更贴合企业实际的建议。
常见问题
1. 项目启动失败怎么办？

先检查 Java 版本：

java -version

需要 JDK 17 或以上。

再检查 Maven：

mvn -version

如果依赖下载失败，可以尝试：

mvn clean install
2. 登录失败怎么办？

请确认使用默认账号：

admin / admin123
analyst / analyst123

如果修改过初始化数据，请检查数据库中的用户信息。

3. 前端页面打不开怎么办？

确认后端是否启动成功，并访问：

http://localhost:8080

如果端口被占用，可以在 application.yml 中修改端口：

server:
  port: 8081
4. H2 数据库看不到数据怎么办？

确认 application.yml 中开启了 H2 控制台：

spring:
  h2:
    console:
      enabled: true

然后访问：

http://localhost:8080/h2-console
项目成果总结

RiskRadar Agent 实现了一个完整可运行的企业级 AI 风险预警 MVP。
它将传统数据看板升级为智能分析平台，能够通过多 Agent 协作完成数据检索、情绪分析、异常检测、风险归因和报告生成。

项目体现了以下能力：

Spring Boot 企业级后端开发
JWT 登录鉴权
数据看板设计
风险评分模型
多 Agent 协作设计
长链推理流程设计
自动报告生成
大数据平台架构理解
AI 驱动业务分析能力

该项目可以作为 AI Agent、大数据分析、企业风险预警、智能决策辅助方向的综合实践项目。
