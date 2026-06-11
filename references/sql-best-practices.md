# SQL 最佳实践

## 安全查询准则

### 1. 始终使用只读用户

```sql
-- ✅ 好：只读用户只能 SELECT
SELECT user_id, name FROM USERS WHERE state='A'

-- ❌ 坏：避免使用有写权限的用户
```

### 2. 始终加 LIMIT/ROWNUM

```sql
-- MySQL/PostgreSQL
SELECT * FROM USERS LIMIT 100;

-- Oracle
SELECT * FROM USERS WHERE ROWNUM <= 100;
```

### 3. 避免 SELECT *

```sql
-- ✅ 好：明确字段
SELECT user_id, name, email FROM USERS WHERE state='A'

-- ❌ 坏：全字段，性能差
SELECT * FROM USERS
```

### 4. 大表查询加索引字段约束

```sql
-- ✅ 好：用索引字段过滤
SELECT * FROM ORDERS WHERE user_id='U12345' AND created_date > '2024-01-01'

-- ❌ 坏：全表扫描
SELECT * FROM ORDERS WHERE note LIKE '%test%'
```

### 5. 避免在 WHERE 子句中对字段做函数操作

```sql
-- ✅ 好
SELECT * FROM ORDERS WHERE created_date >= '2024-01-01'

-- ❌ 坏：无法使用索引
SELECT * FROM ORDERS WHERE DATE(created_date) = '2024-01-01'
```

## 常见查询模板

### 查看表结构

```sql
-- MySQL
DESCRIBE table_name;

-- Oracle
SELECT column_name, data_type, nullable FROM all_tab_columns WHERE table_name='TABLE_NAME';

-- PostgreSQL
SELECT column_name, data_type, is_nullable FROM information_schema.columns WHERE table_name='table_name';
```

### 随机抽样

```sql
-- MySQL/PostgreSQL
SELECT * FROM USERS WHERE state='A' ORDER BY RANDOM() LIMIT 10;

-- Oracle
SELECT * FROM (SELECT * FROM USERS WHERE state='A' ORDER BY DBMS_RANDOM.VALUE) WHERE ROWNUM <= 10;
```

### 查记录数

```sql
SELECT COUNT(*) FROM USERS WHERE state='A';
```

### 查最近的记录

```sql
SELECT * FROM USERS ORDER BY created_date DESC LIMIT 10;
```
