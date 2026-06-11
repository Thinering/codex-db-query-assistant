# 常见查询示例

## 数据准备（为接口测试准备数据）

### 获取一个活跃用户

```
帮我查 my-mysql，找一个状态为"活跃"的用户ID
```

```sql
SELECT user_id, name FROM USERS WHERE state='A' LIMIT 1;
```

### 获取一个可用手机号

```
帮我查 my-oracle，找一个未分配的手机号
```

```sql
SELECT msisdn FROM MSISDN_POOL WHERE status='AVAILABLE' AND ROWNUM <= 1;
```

## 数据校验（验证接口结果）

### 验证数据库写入

```
帮我查 my-pg，确认 userId='U12345' 的记录是否已写入
```

```sql
SELECT user_id, name, email, created_date FROM USERS WHERE user_id='U12345';
```

### 验证状态变更

```
帮我查 my-mysql，查订单 ORDER_001 的最新状态
```

```sql
SELECT order_id, order_state, updated_date FROM ORDERS WHERE order_id='ORDER_001';
```

## 数据探索

### 查看表中所有状态值

```
帮我查 my-oracle，USERS 表有哪些 state 值，各有多少条
```

```sql
SELECT state, COUNT(*) as cnt FROM USERS GROUP BY state ORDER BY cnt DESC;
```

### 查看最近的记录

```
帮我查 my-pg，最近 10 条订单记录
```

```sql
SELECT * FROM ORDERS ORDER BY created_date DESC LIMIT 10;
```
