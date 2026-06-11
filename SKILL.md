# Database Query Assistant

> 让 AI 帮你查数据库。支持 MySQL、Oracle、PostgreSQL。你只需要说"帮我查一下XX表"，AI 自动连接、查询、格式化输出。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 多数据库支持 | MySQL、Oracle、PostgreSQL |
| 自然语言查询 | "查一下最近创建的10个用户" → 自动生成 SQL |
| 连接管理 | 从配置文件读取连接信息，不硬编码 |
| 结果格式化 | 自动格式化输出为表格或 JSON |

---

## 快速开始

### 1. 配置数据库连接

创建 `db-config.json`：

```json
{
  "my-mysql": {
    "type": "mysql",
    "host": "localhost",
    "port": 3306,
    "user": "readonly",
    "password": "xxx",
    "database": "test_db"
  },
  "my-oracle": {
    "type": "oracle",
    "user": "readonly",
    "password": "xxx",
    "dsn": "localhost:1521/ORCL"
  },
  "my-pg": {
    "type": "postgresql",
    "host": "localhost",
    "port": 5432,
    "user": "readonly",
    "password": "xxx",
    "database": "test_db"
  }
}
```

### 2. 告诉 AI 你要查什么

```
帮我查 my-mysql 数据库，最近创建的10个用户
```

AI 会自动：
1. 读取 `db-config.json` 获取连接信息
2. 根据你的描述生成 SQL
3. 执行查询并格式化输出

---

## 使用方式

### 指定 SQL

```
查 my-mysql：SELECT user_id, name, email FROM USERS WHERE state='A' LIMIT 10
```

### 自然语言

```
帮我查 my-pg 数据库，状态为"待处理"的订单有哪些
```

### 结果格式化

```
用 JSON 格式输出
```

---

## 配置说明

### MySQL

```json
{
  "type": "mysql",
  "host": "localhost",
  "port": 3306,
  "user": "readonly",
  "password": "xxx",
  "database": "test_db"
}
```

### Oracle

```json
{
  "type": "oracle",
  "user": "readonly",
  "password": "xxx",
  "dsn": "localhost:1521/ORCL"
}
```

### PostgreSQL

```json
{
  "type": "postgresql",
  "host": "localhost",
  "port": 5432,
  "user": "readonly",
  "password": "xxx",
  "database": "test_db"
}
```

---

## 安全建议

- 数据库用户建议使用**只读权限**
- 密码不要提交到 Git，使用 `.gitignore` 忽略 `db-config.json`
- 建议使用 SSH 隧道或 VPN 连接生产数据库

---

## 目录结构

```
db-query-assistant/
├── SKILL.md                  # 本文件
├── db-config.example.json    # 配置示例
├── LICENSE                   # MIT
├── references/
│   └── sql-best-practices.md # SQL 最佳实践
└── examples/
    └── queries.md            # 常见查询示例
```

---

## License

MIT
