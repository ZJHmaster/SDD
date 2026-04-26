# 公共库/SDK模板 (Library Package Template)

## 标准目录结构
```
my-library/
├── src/
│   ├── index.ts                # 统一导出入口
│   ├── core/                   # 核心功能模块
│   ├── utils/                  # 工具函数
│   └── types/                  # 类型定义
├── tests/
│   ├── unit/
│   └── fixtures/
├── docs/
│   ├── api-reference.md        # API 参考文档
│   └── migration-guide.md      # 版本迁移指南
├── examples/                   # 使用示例
├── .gitignore
├── README.md
├── CHANGELOG.md
├── LICENSE
├── tsconfig.json               # TypeScript 配置
└── package.json                # 包定义 (含导出字段)
```

## 关键配置

### package.json 最佳实践
```json
{
  "name": "@company/my-library",
  "version": "1.0.0",
  "main": "dist/cjs/index.js",
  "module": "dist/esm/index.js",
  "types": "dist/types/index.d.ts",
  "exports": {
    ".": {
      "require": "./dist/cjs/index.js",
      "import": "./dist/esm/index.js",
      "types": "./dist/types/index.d.ts"
    }
  },
  "files": ["dist"],
  "sideEffects": false
}
```

### 版本发布流程
1. 版本号遵循 Semantic Versioning (SemVer)。
2. 破坏性变更必须在 CHANGELOG 和 migration-guide.md 中详细记录。
3. 发布前须通过全部测试 + 构建 + 类型检查。
4. 发布到公司私有 npm/Maven Registry。

### API 设计原则
- 导出的 API 表面积应最小化（只导出用户需要的）。
- 所有公共 API 必须有完整的 TypeDoc/JSDoc 注释。
- 内部实现不导出，使用 `/** @internal */` 标记。
- 提供类型安全的 API（充分利用 TypeScript 泛型）。
