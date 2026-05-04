```markdown
# LLM Customer Service System

一个基于大语言模型的智能对话系统框架，支持多轮对话、流程控制、策略路由和知识检索。

## 项目简介

本项目实现了一个生产级别的对话系统框架，包含完整的对话理解、意图识别、流程管理、策略决策和自然语言生成模块。通过 LangGraph 编排，支持复杂的多轮对话场景和业务流程自动化。

核心特性包括：
- **对话理解**：基于 LLM 的命令生成和解析
- **流程管理**：YAML 定义的对话流程，支持复杂的业务逻辑
- **状态跟踪**：对话状态机和槽位管理
- **策略路由**：多策略集成，支持 Flow、搜索、企业知识库等
- **自然语言生成**：模板和 LLM 双重支持
- **多通道支持**：REST API、WebSocket、交互式 Shell

## 技术栈

- **框架**：LangChain + LangGraph
- **LLM**：通义千问 (Qwen) / OpenAI
- **向量存储**：Neo4j GraphRAG
- **关系数据库**：MySQL
- **后端**：FastAPI
- **嵌入模型**：bge-base-zh-v1.5


## 项目结构

    .
    ├── atguigu_ai/                 # 核心框架
    │   ├── agent/                  # Agent 与 LangGraph 编排
    │   ├── core/                   # 对话追踪、领域、槽位管理
    │   ├── dialogue_understanding/ # 对话理解（命令、Flow、栈）
    │   ├── policies/               # 策略模块
    │   ├── nlg/                    # 自然语言生成
    │   ├── retrieval/              # 检索与嵌入
    │   ├── channels/               # 通道适配器
    │   ├── cli/                    # 命令行工具
    │   ├── api/                    # FastAPI 服务
    │   └── shared/                 # 共享工具与配置
    │
    ├── ecs_demo/                   # 电商客服示例项目
    │   ├── actions/                # 订单、物流、售后 Action
    │   ├── addons/                 # 检索增强生成扩展
    │   ├── domain/                 # 领域定义（意图、槽位、实体）
    │   ├── data/flows/             # 流程定义
    │   ├── config.yml              # 系统配置
    │   └── endpoints.yml           # 模型与数据库配置
    │
    ├── setup.py                    # 项目安装配置
    └── requirements-atguigu.txt    # 依赖列表
## 快速开始

### 环境准备

1. **安装依赖**
```bash
pip install -r requirements-atguigu.txt
```

2. **配置环境变量**
在 `ecs_demo/.env` 中设置：
```
DASHSCOPE_API_KEY=your_qwen_api_key
MYSQL_PASSWORD=your_mysql_password
NEO4J_PASSWORD=your_neo4j_password
```

3. **启动数据库**
- MySQL：创建 `ecommerce` 数据库并导入 SQL 文件
- Neo4j：启动实例并加载知识图谱数据

### 运行示例

**交互式对话（Shell 模式）**
```bash
cd ecs_demo
python -m atguigu_ai shell
```

**启动 REST API 服务**
```bash
python -m atguigu_ai run --config config.yml
```

**调试页面**
```bash
python -m atguigu_ai inspect
```

## 核心概念

### 对话命令系统
对话理解模块将用户输入转换为结构化命令，支持：
- `StartFlowCommand` - 启动对话流程
- `SlotCommand` - 槽位填充与更新
- `AnswerCommand` - 直接回答
- `SessionCommand` - 会话管理

### Flow 流程定义
使用 YAML 定义对话流程，支持：
- 线性流程
- 条件分支
- 子流程调用
- 槽位约束验证

### 策略与动作
- **FlowPolicy**：基于预定义流程的对话策略
- **EnterpriseSearchPolicy**：基于知识库检索的策略
- **Action**：业务逻辑实现（订单查询、物流追踪等）

## 示例场景

电商客服系统演示包含三个主要场景：
1. **订单查询** - 查询订单状态、退货处理
2. **物流追踪** - 查看配送进度、物流信息
3. **售后服务** - 退换货、发票开具

## 主要特性

✨ **生产级框架** - 完整的模块化设计，支持快速定制和扩展

🎯 **灵活的对话流程** - YAML 定义，支持复杂业务逻辑

🔄 **多策略路由** - 自动选择最适合的回答策略

📊 **知识检索增强** - 集成 Neo4j 知识图谱与向量检索

💾 **状态管理** - 支持 JSON、MySQL 等多种存储后端

🌐 **多通道支持** - REST、WebSocket、命令行等多种交互方式

## 后续优化方向

- [ ] 完善数据库配置与示例数据
- [ ] 添加更多内置策略
- [ ] 优化 LLM 提示词工程
- [ ] 支持多轮对话历史管理
- [ ] 添加对话日志与分析模块

## 许可证

MIT License
```
