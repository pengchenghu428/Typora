# 《SQL必知必会》

## 第1章 了解SQL

## 第2章 检索数据

本章介绍如何使用 SELECT 语句从表中检索一个或多个数据列

### 2.1 SELECT 语句

### 2.2 检索单列

`SELECT prod_name FROM Products;`

### 2.3 检索多个列

`SELECT prod_id, prod_name, prod_price FROM Products;`

### 2.4 检索所有列

`SELECT * FROM Products;`

## 第3章 排序检索数据

本章学习如何使用SELECT子句的ORDER BY子句

### 3.1排序数据

`SELECT prod_name FROM Products ORDER BY product_name;`

1. ORDER BY子句应保证为SELECT 的最后一行。

### 3.2 按多个列排序

`SELECT prod_id, prod_name prod_price FROM Products ORDER BY prod_price, prod_name;`

### 3.3 按列位置排序

`SELECT prod_id, prod_name FROM Products ORDER BY 2，3;`

### 3.4 指定排序方向

默认是升序, DESC降序

`SELECT prod_id, prod_name prod_price FROM Products ORDER BY prod_price DESC;`

DESC只应用到直接位于其前面的列名；

`SELECT prod_id, prod_name prod_price FROM Products ORDER BY prod_price DESC, prod_name;`

## 第4章 过滤数据

本章学习如何使用SELECT语句的WHERE子句指定搜索条件；

### 4.1 使用WHERE子句

`SELECT prod_id, prod_name prod_price FROM Products WHERE prod_price = 3.49;`

当同时使用ORDER BY和WHERE子句时，ORDER BY应位于WHERE之后。

### 4.2 WHERE 子句操作符

1. `=; <>; !=; <=; !=; >; >=; !>;`
2. `BETWEEN`
3. `IS NULL`

#### 4.2.1 检测单个值

`SELECT prod_price, prod_name FROM Products WHERE prod_price < 10;`

#### 4.2.2 不匹配检查

`SELECT vend_id, prod_name FROM Products WHERE vend_id <> 'DLL01';`

`SELECT vend_id, prod_name FROM Products WHERE vend_id <> 'DLL01';`

注： 单引号用来限定字符串

#### 4.2.3 范围值检查

`SELECT prod_price, prod_name FROM Products WHERE prod_price BETWEEN 5 AND 10;`

#### 4.2.4 空值检查

`SELECT prod_name FROM Products WHERE prod_price IS NULL`

### 4.3 小结

## 第5章 高级数据过滤

本章讲授如何组合WHERE子句建立功能更强的更高级的搜索条件，我们还将学习如何使用NOT和IN操作符。

### 5.1 组合WHERE子句

#### 5.1.1 AND 操作符

`SELECT prod_id, prod_price, prod_name FROM Products WHERE vend_id = 'DLL01' AND prod_price <= 4;`

此SQL语句检索由供应商DLL01制造且加个小于等于4美元的所有产品的名称和加个。

#### 5.1.2 OR操作符

`SELECT prod_id, prod_price, prod_name FROM Products WHERE vend_id = 'DLL01' OR vebd_id = 'BRS01';`

#### 5.1.3 计算次序

SQL 在处理OR操作符之前，优先处理AND操作。可以通过添加括号来限制操作符的运算次序。

`SELECT prod_id, prod_price, prod_name FROM Products WHERE (vend_id = 'DLL01' OR vebd_id = 'BRS01') AND prod_price >= 10;`

### 5.2 IN 操作符

IN 操作符用来指定条件范围，范围中的每个条件都可以进行匹配。

`SELECT prod_name, prod_price FROM Products WHERE vend_id IN ('DLL01', 'BRS01') ORDER BY prod_nams;`

IN 操作符的优点：

- 更加清楚、直观
- 计算次序更容易管理
- IN比OR更快
- 最大优点时可以包含其他SELECT语句，更动态建立WHERE子句

### 5.3 NOT 操作符

`SELECT prod_name FROM Products WHERE NOT vend_id = 'DLL01';`

列出除 `DLL01` 的所有制造商制造的产品；

### 5.4 小结



## 第6章 用通配符进行过滤

本章介绍什么是通配符、如何使用通配符以及怎样使用LIKE操作符进行通配搜索，以便对数据进行复杂过滤。

### 6.1 LIKE 操作符

#### 6.1.1 百分号%通配符

% 表示任何字符出现任意次数。

`SELECT prod_id, prod_names FROM Products WHERE prod_name LIKE 'Fish%';`

搜索任意以 `Fish` 起头的词。

`SELECT prod_id, prod_name FROM Products WHERE Peoduct_name LIKE '%bean bag%';`

匹配包含文本 `bean bag` 的值，而不论塔之前或之后出现什么字符；

#### 6.1.2 下划线（_）通配符

`(_)` 只匹配单个字符而不是多个字符。

`SELECT prod_id, prod_name FROM Products WHERE prod_name LIKE '__ inch teddy bear';`

对比

`SELECT prod_id, prod_name FROM Products WHERE prod_name LIKE '% inch teddy bear';`

#### 6.1.3 方括号([])通配符

`([])`通配符用来指定一个字符集，它必须匹配指定位置的一个字符。

`SELECT cust_contact FROM Customers WHERE cust_contact LIKE '[JM]%' ORDER BY cust_contact;`

`[JM]` 匹配任何以方括号中字母开头的联系任命，它智能匹配单个字符。

`SELECT cust_contact FROM Customers WHERE cust_contact LIKE '[^JM]%' ORDER BY cust_contact;`

此通配符可以用前缀字符 `^`来否定。

### 6.2 通配符使用技巧

通配符搜索的处理一般要比前面讨论的其他搜索所花时间更长。

## 6.3 小结



## 第7章 创建计算字段

本章介绍什么时计算字段，如何创建计算字段以及怎样应用从应用程序中使用别名引用他们。

### 7.1 计算字段

### 7.2 拼接字段

`SELECT vend_name + ' (' + vend_counter + ')' FROM Vendors ORDER BY vend_name;`

等同于

`SELECT vend_name || ' (' || vend_counter || ')' FROM Vendors ORDER BY vend_name;`

RTRIM() 去除串尾空格

`SELECT RTRIM(vend_name) + ' (' + RTRIM(vend_counter) + ')' FROM Vendors ORDER BY vend_name;`

使用别名: 即指定计算列的列名

`SELECT RTRIM(vend_name) + ' (' + RTRIM(vend_counter) + ')' AS vend_title FROM Vendors ORDER BY vend_name;`

### 7.3 执行算术计算

`SELECT prod_id, quantity, item_price, quantity*item_price AS expanded_price FROM OrderItems WHERE order)num = 20008`

SQL 支持基本操作符 `+ - * /`

### 7.4 小结



## 第8章 使用数据处理函数

本章介绍什么是函数，DBMS支持何种函数，以及如何使用这些函数。

### 8.1 函数

1. 提取串的组成部分
2. 数据类型转换

### 8.2 使用函数

#### 8.2.1 文本处理函数

1. `LEFT() LENGTH() LOWER() LTRIM() RIGHT() RTRIM() SOUNDEX() UPPER()` 
2. `SOUNDEX()`  将任何文本串转换为描述其语音表示的字母数字模式的算法。

#### 8.2.2 日期和时间处理函数

1. `SELECT order_num FROM Orders WHERE DATEPART(yy, order_date) = 2004`

   `DATEPART()` 返回日期的一部分

2. `SELECT order_num FROM Orders WHERE order_date BETWEEN to_date('01-JAN-2004') AND to_date('31-DEC-2004')`

#### 8.2.3 数值处理函数

`ABS() COS() EXP() PI() SIN() SORT() TAN()`

### 8.3 小结



## 第9章 汇总数据

本章介绍什么是SQL的聚集函数以及如何利用他们汇总表的数据。

### 9.1 聚集函数

1. 聚集函数：运行再行组上，计算和返回单个值的函数。

#### 9.1.1 AVG() 函数

1.  `SELECT AVG(prod_price) AS avg_price FROM Products;`
2.  `SELECT AVG(prod_price) AS avg_price FROM Products WHERE vend_id = 'DLL01';`
3. 只用于单个列，AVG() 只能用来确定特定数值列的平均值，而且列名必须作为函数的参数给出，为了获得多个列的平均值，则必须使用多个AVG()函数。

#### 9.1.2 COUNT() 函数

1.  `SELECT COUNT(*) AS num_cust FROM Customers;`
2.  `SELECT COUNT(cust_email) AS num_cust FROM Customers;`
3. COUNT() 如果指定列名，则指定列的值为空的行被忽略，若COUNT()函数中用的是星号，则不忽略。

#### 9.1.3 MAX() 函数

1. `SELECT MAX(prod_price) AS max_price FROM Products;`
2. 对非数值使用 MAX()

#### 9.1.4 MIN() 函数

1. 用法同MAX()，返回最小值

#### 9.1.5 SUM() 函数

1. `SELECT SUM(quantity) AS items_ordered FROM OrderItems WHERE order_num = 20005`
2. `SELECT SUM(item_price*quantity) AS total_price FROM OrderItems WHERE OrderItems WHERE Order_num = 20005`

### 9.2 聚集不同值

1. `SELECT AVG(DISTINCT prod_price) AS avg_price FROM Products WHERE wend_id = 'DLL01';`

   DISTINCT 只考虑各个不同的值

### 9.3 组合聚集函数

1. `SELECT COUNT(*) AS num_items, MIN(prod_price) AS price_min MAX(prod_price) as price_max  AVG(prod_price) AS price_avg FROM Products;`

### 9.4 小结



## 第10章 分组数据

本章将介绍如何分组数据，以便能汇总表内容的子集。这涉及两个新SELECT语句子句，分别是：GROUP BY子句和HAVING子句。

### 10.1 数据分组

### 10.2 创建分组

1. `SELECT vend_id, COUNT(*) AS num_prods FROM Products GROUP BY vend_id;`
2. GROUP BY 子句必须出现在WHERE子句之后，ORDER BY子句之前

### 10.3 过滤分组

1. `SELECT cust_id, COUNT(*) AS orders FROM Orders GROUP BY cust_id HAVING COUNT(*) >= 2`;

2. WHERE 在数据分组前进行过滤，HAVING在数据分组后进行过滤。

3. `SELECT vend_id, COUNT(*) AS num_prods FROM Products WHERE prod_price >= 4 GROUP BY vend_id HAVING COUNT(*) >= 2;`

   同时使用WHERE和HAVING。

### 10.4 分组和排序

1. | ORDER BY                       | GROUP BY                                                   |
   | ------------------------------ | ---------------------------------------------------------- |
   | 排序产生输出                   | 分组行，但输出可能不是分组的顺序                           |
   | 任意列都可以使用，包括非选择列 | 只能使用选择列或者表达式列，而且必须使用每个选择列的表达式 |
   | 不一定需要                     | 如果与聚集函数一起使用列，则必须使用                       |

2. ORDER BY 一般使用在GROUP BY子句之后

3. `SELECT order_num, COUNT(*) AS items FROM OrderItems GROUP BY order_num HAVING COUNT(*) >= 3;`

4. `SELECT order_num, COUNT(*) AS items FROM OrderItems GROUP BY order_num HAVING COUNT(*) >= 3 ORDER BY items, order_num;`

### 10.5 SELECT 子句顺序

1. `SELECT; FROM; WHERE; GROUP BY; HAVING; ORDER BY;`

### 10.6 小结



## 第11章 使用子查询

本章介绍什么是子查询以及如何使用他们。

### 11.1 子查询

### 11.2 利用子查询进行过滤

1. 场景描述：订单存储在两个表中，对于包含订单编号、客户ID、订单日期的每个订单，Orders表存储一行。各订单的物品存储在相关的OrderItems表中。

2. 现在，加入需要列出订购物品RGAN01的所有客户，怎样检索？

3. 如下步骤

   （1） 检索包含武平RGAN01的所有订单的编号

   ​	`SELECT order_num FROM OrderItems WHERE prod_id = 'RGAN01';`

   （2） 检索具有前一步骤列出的订单编号的所有客户ID

   ​	`SELECT cust_id FROM Orders WHERE order_id IN (2007, 2008);`

   ​	注：（2007， 2008）由（1）给出

   （3） 检索客户ID的客户信息

   ​	`SELECT cust_name, cust_contact FROM Customer WHERE cust_id IN ('1000004', '1000005');`

   ​	 注：由（2）得来

4. 一句查询

   `SELECT cust_id FROM Orders WHERE order_num IN (SELECT order_num FROM OrderItems WHERE prod_id = 'RGAN01');`

5. ```sql
   SELECT cust_name, cust_contact
   FROM Customers
   WHERE cust_id IN (SELECT cust_id 
                    FROM Orders
                    WHERE order_id IN (SELECT order_num
                                      FROM OrderItems
                                      WHERE prod_id = 'RGAN01'));
   ```

6. 只能是单列，作为子查询的SELECT语句只能查询单个列。企图检索多个列将返回错误。

### 11.3 作为计算字段使用子查询

1. ```sql
   SELECT cust_name, cust_state, 
   (SELECT COUNT(*)
   		FROM Orders
   		WHERE Orders.cust_id = Customers.cust_id) AS orders
   FROM Customers
   ORDER BY cust_name;
   ```

### 11.4 小结



## 第12章 联结表

本章将介绍什么是联结，为什么要使用联结，如何编写使用联结的SELECT语句。

### 12.1 联结

#### 12.1.1 关系表

#### 12.1.2 为什么要使用联结

### 12.2 创建联结

1. `SELECT vend_name, prod_name, prod_price FROM Vendors, Products WHERE Vendors.vend_id = Products.vend_id;`

#### 12.2.1 WHERE 子句的重要性

#### 12.2.2 内部联结

1. `SELECT vend_name, prod_name, prod_price FROM Vendors INNER JOIN Products ON Vendors.vend_id = Products.vend_id;`

#### 12.2.3 联结多个表

1. `SELECT prod_name, vend_name, prod_price, quantity FROM OrderItems, Products, Vendors WHERE Products.vend_id = Vendors.vend_id AND OrderItems.prod_id = Products.prod_id AND order_num = 20007;`

2. 第11章的例子

   `SELECT cust_name, cust_contact FROM Customers, Orders, OrderItems WHERE Customers.cust_id = Oders.cust_id AND OrderItems.order_num = Orders.order_num AND prod_id = 'RGAN01'; `

### 12.3 小结



## 第13章 创建高级联结

本章将讲解另外一些联结类型（包括他们的含义和使用方法），介绍如何对被联结的表使用表列名和聚集函数。

### 13.1 使用表别名

1. `SELECT cust_name, cust_contact FROM Customers AS C, Orders AS O, OrderItems AS OI WHERE C.cust_id = O.cust_id AND OI.order_num = O.Order_num AND proid_id = 'RGAN01';`

### 13.2 使用不同类型的联结

#### 13.2.1 自联结

1. `SELECT cust_id, cust_name, cust_contact FROM Customers WHERE cust_name = (SELECT cust_name FROM Customers WHERE cust_contact = 'Jim Jones');`
2. `SELECT c.cust_id, c1.cust_name, c1.cust_contact FROM Customers AS c1, Customers AS c2 WHERE c1.cust_name = c2.cust_name AND c2.cust_contact = 'Jim Jones;'`

#### 13.2.2 自然联结

1. `SELECT c.*, O.order_num, O.order_date, OI.prod_id, OI.quantity, OI.item_price FROM Customers AS C, Orders AS O, OrderItems AS OI WHERE C.cust_id = O.cust_id AND OI.order_num = O.order_num AND prod_id = 'RGAN01';`

#### 13.2.3 外部联结

1. 应用场景描述

   对每个客户下了多少订单进行技术，包括把鞋至今尚未下订单的客户

2. `SELECT Customers.cust_id, Order.order_num FROM Customers INNER JOIN Orders ON Customers.cust_id = Orders.cust_id;`

   简单的内部联结，它检索所有的客户及其订单。

3. `SELECT Customers.cust_id, Orders.order_num FROM Customers LEFT OUTER JOIN Orders ON Customers.cust_id = Orders.cust_id;`

   外部联结语法类似。包括那些没有订单的客户

4. `SELECT Customers.cust_id, Orders.order_num FROM Customers, Orders WHERE Customers.cust *= Orders.cust_id;`

   该操作结果同3.

5. `*= =*`

### 13.3 使用带聚集函数的联结

1. `SELECT Customers.cust_id, COUNT(Orders.order_num) AS num_ord FROM Customers INNER JOIN Orders ON Customers.cust_id = Orders.cust_id GROUP BY Customers.cust_id;`
2. `SELECT Customers.cust_id, COUNT(Orders.order_num) AS num_ord FROM Customers LEFT OUTER JOIN Orders ON Customers.cust_id = Orders.cust_id GROUP BY Customer.cust_id;`

### 13.4 使用联结和联结条件

### 13.5 小结



## 第14章

本章讲述如何利用UNION操作符将多条SELECT语句组合成一个结果集。

### 14.1 组合查询

1. 并 或 复合查询

2. 使用场景：

   在单个查询中从不同的表类似返回数据结构

   对单个表执行多个查询，暗淡个查询返回数据

### 14.2 创建组合查询

#### 14.2.1 使用UNION

1. `SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_state IN ('IL', 'IN', 'MI');`

2. `SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_name = 'Fun4All';`

3. ```sql
   SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_state IN ('IL', 'IN', 'MI')
   UNION
   SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_name = 'Fun4All';
   ```

4. 也可以使用UNION完成

   `SELECT cust_name,, cust_contact, cust_email FROM Customers WHERE cust_state IN ('IL', 'IN', 'MI') OR cust_name = 'Fun4All';`

#### 14.2.2 UNION 规则

1. UNION 的每个查询必须包含相同的列、表达式或聚集函数。
2. 列数据类型必须兼任：类型不必完全响应，但必须是DBMS可以隐含地转换数据类型。

#### 14.2.3 包含或取消重复的行

1. UNION 从查询结果中自动去除了重读的行。

2. 如果想要匹配全部的行，使用UNION ALL

   ```sql
   SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_state IN ('IL', 'IN', 'MI')
   UNION ALL
   SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_name = 'Fun4All';
   ```

#### 14.2.4 对组合查询结果排序

1. 在用UNION组合查询时，只能使用一条ORDER BY子句

   ```sql
   SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_state IN ('IL', 'IN', 'MI')
   UNION ALL
   SELECT cust_name, cust_contact, cust_emai FROM Customers WHERE cust_name = 'Fun4All'
   ORDER BY cust_name, cust_contact;
   ```

### 14.3 小结







































































