---
title: "SQLServer sql语句基础语法"
date: 2024-10-24
categories: ["database"]
---

SQL Server 数据库中的操作指令基于 SQL 语言标准，支持常见的数据库操作语句。以下是 SQL Server 中常见的 SQL 指令，按照不同的操作类别进行归纳。

### 一、数据库管理操作

1. **创建数据库**
   ```sql
   CREATE DATABASE database_name;
   ```
   
2. **修改数据库**
   ```sql
   ALTER DATABASE database_name
   MODIFY FILE (NAME = logical_file_name, SIZE = new_size);
   ```

3. **删除数据库**
   ```sql
   DROP DATABASE database_name;
   ```

4. **选择数据库**
   ```sql
   USE database_name;
   ```

### 二、表的管理操作

1. **创建表**
   ```sql
   CREATE TABLE table_name (
       column1 datatype constraint,
       column2 datatype constraint,
       ...
   );
   ```

2. **修改表结构**
   - 添加列：
     ```sql
     ALTER TABLE table_name
     ADD column_name datatype;
     ```
   - 删除列：
     ```sql
     ALTER TABLE table_name
     DROP COLUMN column_name;
     ```
   - 修改列的数据类型：
     ```sql
     ALTER TABLE table_name
     ALTER COLUMN column_name new_datatype;
     ```

3. **删除表**
   ```sql
   DROP TABLE table_name;
   ```

### 三、数据操作（DML）

1. **插入数据**
   ```sql
   INSERT INTO table_name (column1, column2, ...)
   VALUES (value1, value2, ...);
   ```

2. **更新数据**
   ```sql
   UPDATE table_name
   SET column1 = value1, column2 = value2, ...
   WHERE condition;
   ```

3. **删除数据**
   ```sql
   DELETE FROM table_name
   WHERE condition;
   ```

4. **查询数据**
   ```sql
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition;
   ```

5. **查询所有数据**
   ```sql
   SELECT * FROM table_name;
   ```

6. **排序查询结果**
   ```sql
   SELECT column1, column2
   FROM table_name
   ORDER BY column1 [ASC|DESC];
   ```

7. **过滤重复数据**
   ```sql
   SELECT DISTINCT column1
   FROM table_name;
   ```

8. **统计查询**
   - 计数：
     ```sql
     SELECT COUNT(*)
     FROM table_name;
     ```
   - 求和：
     ```sql
     SELECT SUM(column_name)
     FROM table_name;
     ```
   - 平均值：
     ```sql
     SELECT AVG(column_name)
     FROM table_name;
     ```
   - 最大值和最小值：
     ```sql
     SELECT MAX(column_name), MIN(column_name)
     FROM table_name;
     ```

### 四、索引操作

1. **创建索引**
   - 创建普通索引：
     ```sql
     CREATE INDEX index_name
     ON table_name (column_name);
     ```
   - 创建唯一索引：
     ```sql
     CREATE UNIQUE INDEX index_name
     ON table_name (column_name);
     ```

2. **删除索引**
   ```sql
   DROP INDEX index_name ON table_name;
   ```

### 五、视图操作

1. **创建视图**
   ```sql
   CREATE VIEW view_name AS
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition;
   ```

2. **修改视图**
   ```sql
   ALTER VIEW view_name AS
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition;
   ```

3. **删除视图**
   ```sql
   DROP VIEW view_name;
   ```

### 六、存储过程和函数操作

1. **创建存储过程**
   ```sql
   CREATE PROCEDURE procedure_name
   AS
   BEGIN
       -- SQL语句
   END;
   ```

2. **执行存储过程**
   ```sql
   EXEC procedure_name;
   ```

3. **删除存储过程**
   ```sql
   DROP PROCEDURE procedure_name;
   ```

4. **创建用户定义函数**
   - 标量函数：
     ```sql
     CREATE FUNCTION function_name (@param1 datatype, ...)
     RETURNS datatype
     AS
     BEGIN
         RETURN expression;
     END;
     ```
   - 表值函数：
     ```sql
     CREATE FUNCTION function_name (@param1 datatype, ...)
     RETURNS TABLE
     AS
     RETURN
     (
         SELECT ...
     );
     ```

5. **删除函数**
   ```sql
   DROP FUNCTION function_name;
   ```

### 七、触发器操作

1. **创建触发器**
   ```sql
   CREATE TRIGGER trigger_name
   ON table_name
   AFTER INSERT, UPDATE, DELETE
   AS
   BEGIN
       -- SQL 逻辑
   END;
   ```

2. **删除触发器**
   ```sql
   DROP TRIGGER trigger_name;
   ```

### 八、事务控制

1. **开启事务**
   ```sql
   BEGIN TRANSACTION;
   ```

2. **提交事务**
   ```sql
   COMMIT TRANSACTION;
   ```

3. **回滚事务**
   ```sql
   ROLLBACK TRANSACTION;
   ```

### 九、权限管理

1. **创建用户**
   ```sql
   CREATE LOGIN login_name WITH PASSWORD = 'password';
   CREATE USER user_name FOR LOGIN login_name;
   ```

2. **赋予权限**
   ```sql
   GRANT permission_type ON object_name TO user_name;
   ```

3. **撤销权限**
   ```sql
   REVOKE permission_type ON object_name FROM user_name;
   ```

4. **删除用户**
   ```sql
   DROP USER user_name;
   ```

### 十、其他常用命令

1. **联合查询（UNION）**
   ```sql
   SELECT column1, column2 FROM table1
   UNION
   SELECT column1, column2 FROM table2;
   ```

2. **分组查询**
   ```sql
   SELECT column1, COUNT(*)
   FROM table_name
   GROUP BY column1;
   ```

3. **子查询**
   ```sql
   SELECT column1
   FROM table_name
   WHERE column2 IN (SELECT column2 FROM another_table);
   ```

4. **限制查询条数**
   ```sql
   SELECT TOP 10 column1, column2
   FROM table_name;
   ```

### 总结
上述 SQL 指令涵盖了 SQL Server 中大部分常用的数据库操作。熟悉这些指令后，你可以轻松管理数据库、表、数据，以及控制用户权限、操作事务等。每个指令都有其特殊的使用场景，建议在实际操作中根据需求选择合适的命令。