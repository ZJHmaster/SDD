# 命名约定与规范 (Naming Conventions)

## 1. 核心原则
- **清晰胜于简短**：绝不要为了少打几个字母牺牲可读性（`customer` 优于 `cust`）。
- **可搜索性**：避免使用如 `data`, `info`, `obj` 这样空洞且在整个项目中泛滥的名称。
- **意图导向**：变量名必须回答以下问题：它表示什么？它包含了什么？它的单位是什么？

## 2. 大小写与命名法约定

### 2.1 常见约定 (适用于绝大多数C-style语言如Java, TS, C#)
- **类名 (Class/Interface)**：大驼峰式 (`PascalCase`)，如 `UserRepository`, `PaymentProcessor`。
    - *接口建议带前缀 `I` (C#/TS为主) 或使用 `able` 后缀 (Java)。*
- **方法名 (Methods)**：小驼峰式 (`camelCase`)，如 `getUserById()`, `calculateTotal()`。必须是动词或动宾短语。
- **变量名 (Variables)**：小驼峰式 (`camelCase`)，名词为主。
- **常量 (Constants)**：大写蛇形 (`UPPER_SNAKE_CASE`)，如 `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT_MS`。

### 2.2 数据库与文件命名
- **数据库表与列**：小写蛇形 (`snake_case`)，如 `user_profiles`, `created_at`。表名推荐复数。
- **文件名 (HTML/CSS/JS/Config)**：小写烤肉串/连字符 (`kebab-case`)，如 `user-profile-component.ts`, `app-settings.json`。

## 3. 布尔类型命名
布尔变量或返回布尔值的函数，必须使用能够明确表达是/否的前缀：
- `is`：判断状态 (`isReady`, `isVIP`)
- `has`：判断是否拥有 (`hasChildren`, `hasPermission`)
- `can`：判断是否允许动作 (`canExecute`)
- `should`：判断是否应当发生 (`shouldUpdate`)

## 4. 集合与循环变量
- 数组或列表的变量应当使用**复数名词**（`users`, `orderItems`）或添加显式后缀（`userList`）。
- 禁止在嵌套作用域内外使用单字母 `i`, `j`, `k` 引起混淆，可针对性使用 `userIndex`, `orderIndex`。
