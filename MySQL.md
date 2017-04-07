
## SQL
    SQL是Struc-tured Query Language（结构化查询语言）的缩写。SQL是一种专门用来与数据库沟通的语言
### 主键
    唯一标识表中每行的这个列（或这几列）称为主键。
    主键用来表示一个特定的行。没有主键，更新或删除表中特定行就极为困难，
    因为你不能保证操作只涉及相关的行。

### 检索列
    SELECT prod_name FROM Products;
    SELECT prod_id, prod_name, prod_price FROM Products;


### 只返回不同（具有唯一性）的行
    SELECT DISTINCT
    loadstationname
    FROM
    consignnote

### 返回不超过5行数据
    SELECT
    loadstationname
    FROM
    consignnote
    LIMIT 5

### 返回从第5行开始的8行数据
    SELECT
    loadstationname
    FROM
    consignnote
    LIMIT 8 OFFSET 5

### 注释
    SELECT prod_name    -- 这是一条注释
    FROM Products;

    # 这是一条注释
    SELECT
    prod_name
    FROM
    Products;

### 排序查询
    SELECT prod_name
    FROMO Products
    ORDER BY prod_name

    SELECT prod_id, prod_price, prod_name
    FROM Products
    ORDER BY prod_price, prod_name


### 价格降序来排序产品（最贵的排在最前面）
    SELECT prod_id, prod_price, prod_name
    FROM Products
    ORDER BY prod_price DESC;

    （ASC代表升序，默认升序）

### 过滤查询
    SELECT prod_name, prod_price FROM Products WHERE prod_price = 3.49;

    SELECT prod_id, prod_price, prod_name
    FROM Products
    WHERE vend_id = 'DLL01' AND prod_price <= 4;

    SELECT prod_name, prod_price
    FROM Products
    WHERE vend_id = 'DLL01' OR vend_id = ‘BRS01’;

    SELECT prod_name, prod_price FROM Products
    WHERE (vend_id = 'DLL01' OR vend_id = 'BRS01') AND prod_price >= 10;

    SELECT prod_name, prod_price FROM Products
    WHERE vend_id IN ( 'DLL01', 'BRS01' ) ORDER BY prod_name;
    相当于=>
    SELECT prod_name, prod_price FROM Products
    WHERE vend_id = 'DLL01' OR vend_id = 'BRS01' ORDER BY prod_name;

    # 列出除DLL01之外的所有供应商制造的产品
    SELECT prod_name FROM Products
    WHERE NOT vend_id = 'DLL01' ORDER BY prod_name;


### 使用通配符过滤
    为在搜索子句中使用通配符，必须使用LIKE操作符。
    LIKE指示DBMS，后跟的搜索模式利用通配符匹配而不是简单的相等匹配进行比较。
    通配符搜索只能用于文本字段（串），非文本数据类型字段不能使用通配符搜索。

    # 检索任意以Fish起头的词。%告诉DBMS接受Fish之后的任意字符，不管它有多少字符。
    SELECT prod_id, prod_name
    FROM Products WHERE prod_name LIKE 'Fish%';

    # 找出所有名字以J或M起头的联系人
    SELECT cust_contact
    FROM Customers WHERE cust_contact
    LIKE '[JM]%' ORDER BY cust_contact;、


### 字段组合
    # 返回是这样的： '何柳杰/17017271200'
    SELECT Concat(enlinkername, ' /', enlinkerphone)
    FROM consignnote

### 算术计算
     #汇总（单价乘数量）
     SELECT
     	totalqty,
     	totalfare,
     	totalqty * totalfare AS expanded_fare
     FROM consignnote

### 函数处理数据
     # 转换大写
     SELECT
        vend_name,
        UPPER(vend_name) AS vend_name_upcase
     FROM Vendors ORDER BY vend_name;

### 求平均值
     SELECT
     	AVG(totalfare) AS avg_totalfare
     FROM
     	consignnote

### 总数
     SELECT
        COUNT(*) AS num_cust
     FROM
        Customers;

### 最大值
     SELECT
        MAX(prod_price) AS max_price
     FROM
        Products;

     # MIN()最小值

### 返回购物品总数
     # OrderItems包含订单中实际的物品，每个物品有相应的数量，
     SELECT
        SUM(quantity) AS items_ordered
     FROM OrderItems
     WHERE order_num = 20005;

### 子查询
    # 获取产品名为'苹果'的订单号
    SELECT ordernum
    FROM orderitem
    WHERE productname = '苹果'

    #返回 1023,1024

    #根据订单号，获取对应的客户名
    SELECT customername
    FROM order
    WHERE ordernum IN (1023, 1024)

    =======》 等同于 子查询
    SELECT customername
    FROM order
    WHERE ordernum IN (
            SELECT ordernum
            FROM orderitem
            WHERE productname = '苹果'
        );

### 联结
     如果数据存储在多个表中，怎样用一条SELECT语句就检索出数据呢？
     使用联结

     # 一条SELECT语句返回了两个不同表中的数据。
     SELECT vend_name, prod_name, prod_price
     FROM Vendors, Products
     WHERE Vendors.vend_id = Products.vend_id;


     内联结
     SELECT vend_name, prod_name, prod_price
     FROM Vendors
     INNER JOIN Products
     ON Vendors.vend_id = Products.vend_id;

     联结多个表
     SELECT
        prod_name, vend_name, prod_price, quantity
     FROM
        OrderItems, Products, Vendors
     WHERE
        Products.vend_id = Vendors.vend_id
     AND
        OrderItems.prod_id = Products.prod_id
     AND
        order_num = 20007;


### 使用表别名
     SELECT cust_name, cust_contact
     FROM Customers AS C, Orders AS O, OrderItems AS OI
     WHERE C.cust_id = O.cust_id
     AND OI.order_num = O.order_num
     AND prod_id = 'RGAN01';


### 组合查询
    #这条语句由前面的两条SELECT语句组成，之间用UNION关键字分隔。UNION指示DBMS执行这两条SELECT语句，并把输出组合成一个查询结果集
    SELECT
        cust_name, cust_contact, cust_email
    FROM
        Customers
    WHERE
        cust_state IN ('IL','IN','MI')
    UNION
    SELECT
        cust_name, cust_contact, cust_email
    FROM
        Customers
    WHERE
        cust_name = 'Fun4All';

    # UNION从查询结果集中自动去除了重复的行；换句话说，它的行为与一条SELECT语句中使用多个WHERE子句条件一样
    # 如果想返回所有的匹配行，可使用UNION ALL而不是UNION


### 插入数据
    INSERT INTO Customers(
        cust_id,
        cust_name,
    )
    VALUES('1000000006', 'Toy Land')

### 从一个表复制到另一个表
    CREATE TABLE goods2 AS
    SELECT * FROM goods

### 更新数据
    UPDATE
        Customers
    SET
        cust_contact = 'Sam Roberts',
        cust_email = 'sam@toyland.com'
    WHERE
        cust_id = '1000000006';

### 删除数据
    DELETE FROM
        Customers
    WHERE 
        cust_id = '1000000006';
