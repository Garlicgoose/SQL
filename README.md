# SQL



`CREATE` 不只是创建表（`TABLE`），它属于 **DDL（Data Definition Language，数据定义语言）**，主要用于创建数据库对象。

|对象|作用|示例|
|---|---|---|
|Database|创建数据库|`CREATE DATABASE CargoFlow;`|
|Table|创建表|`CREATE TABLE shipments (...);`|
|View|创建视图（虚拟表）|`CREATE VIEW v_shipments AS SELECT * FROM shipments;`|
|Index|创建索引，加快查询|`CREATE INDEX idx_awb ON shipments(awb);`|
|Trigger|创建触发器|`CREATE TRIGGER trg_update ...`|
|Procedure|创建存储过程|`CREATE PROCEDURE GetShipment ...`|
|Function|创建函数|`CREATE FUNCTION CalcWeight(...)`|
|Schema|创建模式（命名空间）|`CREATE SCHEMA logistics;`|
|Sequence|创建序列|`CREATE SEQUENCE seq_awb;`|
|User|创建数据库用户|`CREATE USER peng IDENTIFIED BY '123';`|
|Role|创建角色|`CREATE ROLE logistics_admin;`|


---

# 表

```
shipments  
├── awb  
├── status  
└── ship_date  
```

# CREATE VIEW（视图）

保存好的 SELECT 查询。

``` SQL
CREATE VIEW undelivered_shipments AS  
SELECT *  
FROM shipments  
WHERE status <> 'Delivered';

SELECT *  
FROM undelivered_shipments;
```

相当于下面:

```SQL
SELECT *  

FROM shipments  

WHERE status <> 'Delivered';
```


# CREATE INDEX（索引）

提高查询速度。


# CREATE TRIGGER（触发器）

数据库自动执行的代码。

```python
if status=="Delivered":  

自动执行
```

```SQL
CREATE TRIGGER trg_delivered  

AFTER UPDATE ON shipments  

FOR EACH ROW  

WHEN NEW.status='Delivered'  

BEGIN  

UPDATE shipments  

SET delivered_date=CURRENT_TIMESTAMP  

WHERE awb=NEW.awb;  

END;
```

自动记录完成时间
自动写日志


# CREATE DATABASE（数据库）

# CREATE FUNCTION（函数）

