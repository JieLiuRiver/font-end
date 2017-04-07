
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


### 创建表
    CREATE TABLE OrderItems (
        order_num      INTEGER          NOT NULL,
        order_item     INTEGER          NOT NULL,
        prod_id        CHAR(10)         NOT NULL,
        quantity       INTEGER          NOT NULL      DEFAULT 1,
        item_price     DECIMAL(8,2)     NOT NULL
    );

### 新增列
    ALTER TABLE Vendors
    ADD vend_phone CHAR(20);

### 删除表
    DROP TABLE CustCopy;

### 利用视图简化复杂的联结
    # 这条语句创建一个名为ProductCustomers的视图，它联结三个表
    CREATE VIEW
        ProductCustomers
    AS SELECT
        cust_name, cust_contact, prod_id
    FROM
        Customers, Orders, OrderItems
    WHERE
        Customers.cust_id = Orders.cust_id
    AND
        OrderItems.order_num = Orders.order_num;


    # 这条语句通过WHERE子句从视图中检索特定数据
    SELECT
        cust_name, cust_contact
    FROM ProductCustomers
    WHERE
        prod_id = 'RGAN01';


### 用视图过滤不想要的数据

    CREATE VIEW
        CustomerEMailList
    AS SELECT
        cust_id, cust_name, cust_email
    FROM Customers
    WHERE
        cust_email IS NOT NULL;

    # 像使用其他表一样使用视图Cus-tomerEMailList
    SELECT * FROM CustomerEMailList;


### 事务处理
    通过确保成批的SQL操作要么完全执行，要么完全不执行，来维护数据库的完整性
    如果故障发生在插入Orders行之后，添加OrderItems行之前，怎么办？
    现在，数据库中有一个空订单。更糟的是，如果系统在添加OrderItems行之时出现故障，怎么办？
    事物处理这个机制可以保证数据库不包含不完整的操作结果
    1. 事务（transaction）指一组SQL语句；
    2. 回退（rollback）指撤销指定SQL语句的过程；
    3. 提交（commit）指将未存储的SQL语句结果写入数据库表；
    4. 保留点（savepoint）指事务处理中设置的临时占位符（placeholder），可以对它发布回退（与回退整个事务处理不同）。


    # BEGIN TRANSACTION和COMMITTRANSACTION语句之间的SQL必须完全执行或者完全不执行
    BEGIN TRANSACTION
        ...
    COMMIT TRANSACTION


#### 回退 ROLLBACK
    # 执行DELETE操作，然后用ROLL-BACK语句撤销
    DELETE FROM Orders;
    ROLLBACK;

#### 提交 COMMIT
    # 涉及更新两个数据库表Orders和OrderItems，所以使用事务处理块来保证订单不被部分删除。
        最后的COMMIT语句仅在不出错时写出更改。如果第一条DELETE起作用，但第二条失败，则DELETE不会提交
    BEGIN TRANSACTION
        DELETE OrderItems WHERE order_num = 12345
        DELETE Orders WHERE order_num = 12345
    COMMIT TRANSACTION


####　保留点
    ＃　前面描述的添加订单的过程就是一个事务。＼
        如果发生错误，只需要返回到添加Orders行之前即可。不需要回退到Customers表（如果存在的话）

    ROLLBACK TO delete1;


### 特性

#### 约束
##### 主键
     # 保证一列是唯一的
     CREATE TABLE Vendors
     (
        vend_id         CHAR(10)       NOT NULL     PRIMARY KEY,
        vend_name       CHAR(50)       NOT NULL
     )


##### 外键
    外键是表中的一列，其值必须列在另一表的主键中

    # 使用了REFERENCES关键字，它表示cust_id中的任何值都必须是Customers表的cust_id中的值
    CREATE TABLE Orders
    (
        order_num     INTEGER     NOT NULL PRIMARY KEY,
        order_date    DATETIME    NOT NULL,
        cust_id       CHAR(10)    NOT NULL REFERENCES Customers(cust_id)
    );


##### 唯一约束
    唯一约束用来保证一列（或一组列）中的数据是唯一的。它们类似于主键
        1. 表可包含多个唯一约束，但每个表只允许一个主键。
        2. 唯一约束列可包含NULL值。
        3. 唯一约束列可修改或更新。
        4. 唯一约束列的值可重复使用。
        5. 与主键不一样，唯一约束不能用来定义外键。

##### 检查约束
    检查约束在数据类型内又做了进一步的限制，这些限制极其重要，
    可以确保插入数据库的数据正是你想要的数据。
    不需要依赖于客户端应用程序或用户来保证正确获取它

    # 利用这个约束，任何插入（或更新）的行都会被检查，保证quantity大于0
    CREATE TABLE OrderItems
    (
        order_num     INTEGER     NOT NULL,
        order_item    INTEGER     NOT NULL,
        prod_id       CHAR(10)    NOT NULL,
        quantity      INTEGER     NOT NULL CHECK (quantity > 0),
        item_price    MONEY       NOT NULL
    );


##### 索引
    索引用来排序数据以加快搜索和排序操作的速度。

    # 索引必须唯一命名。这里的索引名prod_name_ind在关键字CREATE INDEX之后定义。ON用来指定被索引的表，而索引中包含的列
    CREATE INDEX
        prod_name_ind
    ON PRODUCTS (prod_name);
