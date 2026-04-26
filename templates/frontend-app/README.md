# 前端应用模板 (Frontend App Template)

## 标准目录结构
```
my-frontend-app/
├── public/
│   ├── index.html
│   ├── favicon.ico
│   └── manifest.json
├── src/
│   ├── assets/                 # 静态资源 (图片/字体/图标)
│   ├── components/             # 通用UI组件 (原子级)
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.test.tsx
│   │   │   ├── Button.module.css
│   │   │   └── index.ts
│   │   └── ...
│   ├── features/               # 功能模块 (按业务域组织)
│   │   ├── auth/               # 认证模块
│   │   │   ├── components/     # 模块专用组件
│   │   │   ├── hooks/          # 模块专用 Hooks
│   │   │   ├── services/       # 模块 API 调用
│   │   │   ├── stores/         # 模块状态管理
│   │   │   └── types.ts        # 模块类型定义
│   │   └── orders/             # 订单模块 (示例)
│   ├── layouts/                # 页面布局组件
│   ├── pages/                  # 路由页面入口
│   ├── hooks/                  # 全局公共 Hooks
│   ├── services/               # API 基础设施 (HTTP Client / 拦截器)
│   ├── stores/                 # 全局状态管理
│   ├── i18n/                   # 国际化配置
│   │   ├── locales/
│   │   │   ├── zh-CN.json
│   │   │   └── en-US.json
│   │   └── config.ts
│   ├── styles/                 # 全局样式与设计 Token
│   │   ├── variables.css       # CSS 变量 / 设计 Token
│   │   ├── reset.css           # CSS Reset
│   │   └── global.css          # 全局样式
│   ├── utils/                  # 工具函数
│   ├── types/                  # 全局类型定义
│   ├── constants/              # 全局常量
│   ├── App.tsx
│   ├── main.tsx
│   └── router.tsx              # 路由配置
├── tests/
│   ├── e2e/                    # 端到端测试
│   └── setup.ts                # 测试配置
├── .env.example
├── .gitignore
├── README.md
├── CHANGELOG.md
└── vite.config.ts              # 构建配置
```

## 内置配置
- **HTTP 拦截器**：统一处理 Token 注入、401 跳转、错误提示。
- **路由守卫**：未登录用户自动重定向至登录页。
- **i18n 框架**：开箱即用的多语言支持，支持运行时切换。
- **错误边界 (Error Boundary)**：全局程序崩溃兜底页面。
- **性能监控**：Web Vitals (LCP/INP/CLS) 采集上报。
- **a11y 基线**：语义化标签 + ARIA 角色 + 键盘导航支持。

## 设计 Token 体系
通过 CSS Variables 建立统一的设计语言：
```css
:root {
  --color-primary: #2563eb;
  --color-error: #dc2626;
  --font-family-base: 'Inter', system-ui, sans-serif;
  --spacing-unit: 8px;
  --border-radius-md: 8px;
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
}
```
