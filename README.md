# DB Query Assistant - Codex Skill

> 让 AI 帮你查数据库。支持 MySQL、Oracle、PostgreSQL。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Codex Skill](https://img.shields.io/badge/Codex-Skill-blue)](https://github.com/openai/codex)

---

## 它能做什么

你用自然语言说"帮我查一下最近创建的10个用户"，AI 自动连接数据库、生成 SQL、执行查询、格式化输出。

```
你：帮我查 my-mysql，找状态为"A"的用户，最近10个

AI：✅ 查询成功（3ms）
    ┌──────────┬───────┬─────────────────────┐
    │ user_id  │ name  │ email               │
    ├──────────┼───────┼─────────────────────┤
    │ U001     │ 张三  │ zhangsan@test.com   │
    │ U002     │ 李四  │ lisi@test.com       │
    │ ...      │ ...   │ ...                 │
    └──────────┴───────┴─────────────────────┘
    共 10 条记录
```

---

## 快速开始

### 1. 配置数据库

```json
{
  "my-mysql": {
    "type": "mysql",
    "host": "localhost",
    "port": 3306,
    "user": "readonly",
    "password": "xxx",
    "database": "test_db"
  }
}
```

### 2. 告诉 AI 你要查什么

```
查 my-mysql：SELECT user_id, name FROM USERS LIMIT 10
```

或用自然语言：

```
帮我查 my-mysql，最近创建的10个活跃用户
```

---

## 支持的数据库

| 数据库 | 配置方式 |
|--------|---------|
| MySQL | host + port + user + password + database |
| Oracle | user + password + dsn |
| PostgreSQL | host + port + user + password + database |

---

## 安全建议

- 使用**只读数据库用户**
- `db-config.json` 加入 `.gitignore`
- 生产环境建议通过 SSH 隧道连接

---

## License

MIT
