# 微服务项目模板 (Microservice Template)

## 标准目录结构
```
my-service/
├── src/
│   ├── api/                    # 表现层 - Controller / Router
│   │   ├── controllers/        # 请求处理器
│   │   ├── middlewares/        # 中间件 (Auth, CORS, Logger, ErrorHandler)
│   │   ├── validators/         # 入参校验规则
│   │   └── routes.js           # 路由注册
│   ├── application/            # 应用层 - Use Cases
│   │   ├── services/           # 应用服务 (业务编排)
│   │   ├── dtos/               # 数据传输对象 (Request/Response DTO)
│   │   └── mappers/            # Entity <-> DTO 映射器
│   ├── domain/                 # 领域层 - 纯业务逻辑
│   │   ├── entities/           # 领域实体
│   │   ├── value-objects/      # 值对象
│   │   ├── repositories/       # Repository 接口定义 (抽象)
│   │   ├── services/           # 领域服务
│   │   ├── events/             # 领域事件
│   │   └── exceptions/         # 领域异常
│   ├── infrastructure/         # 基础设施层
│   │   ├── database/           # 数据库连接与 Repository 实现
│   │   │   ├── migrations/     # Migration 脚本
│   │   │   └── repositories/   # Repository 实现
│   │   ├── messaging/          # 消息队列 Producer/Consumer
│   │   ├── external/           # 外部 API 客户端
│   │   ├── cache/              # 缓存实现
│   │   └── config/             # 配置加载
│   └── shared/                 # 共享工具与常量
│       ├── constants/          # 全局常量
│       ├── utils/              # 工具函数
│       └── types/              # 共享类型定义
├── tests/
│   ├── unit/                   # 单元测试 (镜像 src 结构)
│   ├── integration/            # 集成测试
│   └── fixtures/               # 测试数据 & Factories
├── docs/
│   └── adr/                    # 架构决策记录
├── scripts/                    # 构建/部署/数据脚本
├── .env.example                # 环境变量模板
├── .gitignore
├── Dockerfile
├── docker-compose.yml          # 本地开发用依赖编排
├── README.md
└── CHANGELOG.md
```

## 内置配置清单
- **统一错误处理中间件**：自动捕获未处理异常，以标准格式返回。
- **请求日志中间件**：记录入站请求的 traceId、方法、路径、耗时。
- **健康检查端点**：`GET /health` 返回服务健康状态和依赖可达性。
- **优雅停机**：捕获 SIGTERM，完成进行中请求后退出。
- **环境变量验证**：启动时校验必需的环境变量，缺失则 Fail Fast。

## 定制指南
创建新项目时，修改以下占位：
1. `package.json` / `pom.xml` 中的项目名称和描述。
2. `.env.example` 中的环境变量列表。
3. `README.md` 中的项目简介。
4. 删除不需要的 `infrastructure/` 子模块（如不用消息队列则删除 `messaging/`）。
