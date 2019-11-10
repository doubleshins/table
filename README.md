# table
## 電商平台


![](https://i.imgur.com/4y7yFf0.png)


- 建立 customers 資料表

## 客戶資料
```bash
create table customers (
    cust_ID int NOT NULL, #客戶編號
    name  VARCHAR(30) CHECK (CHAR_LENGTH(name)>=2), # 姓名
    sex  char(1) CHECK (sex IN ('男', '女')), # 性別
    phone VARCHAR(10) UNIQUE , # 行動電話
    age  int CHECK (age > 0), # 年齡
    email  char(50) UNIQUE , # 電子信箱
    address  char(50) , # 地址
    
    CONSTRAINT check_phone CHECK (phone like '09________'),
    CONSTRAINT check_email CHECK (email like '%@%'),
    primary key (cust_ID)
);
```
```bash
INSERT INTO customers(name, sex, phone, age, email, address) VALUES('郭大豪', '男', '0984273123', '20', 'A001@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 800 號');
INSERT INTO customers(name, sex, phone, age, email, address) VALUES('張彥宏', '男', '0987627123', '21', 'A002@gcloud.csu.edu.tw', '台南市鳥松區澄清路 823 號');
INSERT INTO customers(name, sex, phone, age, email, address) VALUES('林郁評', '男', '0987627129', '33', 'A003@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 843 號');
INSERT INTO customers(name, sex, phone, age, email, address) VALUES('劉姵君', '女', '0987623239', '40', 'A004@gcloud.csu.edu.tw', '新北市鳥松區澄清路 812 號');
INSERT INTO customers(name, sex, phone, age, email, address) VALUES('陸美女', '女', '0987627249', '25', 'A005@gcloud.csu.edu.tw', '桃園市鳥松區澄清路 123 號');
```



- 建立 products 資料表

## 產品
```bash
create table products  (
    pro_ID int NOT NULL, #產品編號
    name varchar(50) UNIQUE CHECK (CHAR_LENGTH(name)>=1),  #產品名稱
    price int CHECK (price > 0),  # 單價
    inventory int CHECK (inventory >= 0), # 庫存量
    descr varchar(200) UNIQUE,  # 產品說明
    added_date  TIMESTAMP DEFAULT CURRENT_TIMESTAMP, # 上架時間
    end_date DATE CHECK (added_date<end_date), # 下架時間
    is_on_sale boolean default true, # 是否上架
    
    primary key(pro_ID)      # 主鍵
);
```
```bash
INSERT INTO products(name, price, inventory, descr) VALUES('KOKUYO KARUCUT夾式膠台', '99', '50', '讓你隨時方便使用紙膠帶，只要拿在手裡，更換膠帶好容易，刀口平整，再也不必怕撕不斷跟醜醜的撕開開口');
INSERT INTO products(name, price, inventory, descr) VALUES('Wedgwood淺藍色碧玉浮雕細頸花瓶', '700', '10', 'WEDGWOOD 創立於西元1759年，由被尊為英國陶瓷之父的 Josiah Wedgwood 所創辦。');
INSERT INTO products(name, price, inventory, descr) VALUES('手作耳環', '350', '20', '925銀配三層鍍金 很難褪色 又抗過敏(除非你是鉑金才不會過敏的特異體質)');
```




- 建立 sales 資料表

## 訂單
```bash
create table sales (
    sales_ID int NOT NULL, #訂單單號
    cust_ID  int NOT NULL, #客戶編號
    
    odate  TIMESTAMP DEFAULT CURRENT_TIMESTAMP, # 訂貨日期
    ddate DATE CHECK (odate<ddate), # 送貨日期
    ip_address  varchar(20), # IP位址
    recipient_phone varchar(10), # 收件人電話
    recipient_remark varchar(100) NOT NULL, # 收件備註
 
    sale_status boolean default false, # 是否處理
    
    primary key (sales_ID),
    CONSTRAINT check_recipient_phone CHECK (recipient_phone like '09________'),
    CONSTRAINT check_ip_address CHECK (ip_address like '%.%.%.%'),
    FOREIGN KEY (cust_ID) REFERENCES customers(cust_ID)
);
```
```bash
INSERT INTO `sales` (`sales_ID`, `cust_ID`, `odate`, `ddate`, `ip_address`, `recipient_phone`, `recipient_remark`, `sale_status`) VALUES (NULL, '1', current_timestamp(), NULL, '120.114.140.17', '0987686543', '不用統編', '0');
```





-  建立 messages 資料表


## 訊息資料表
```bash
create table messages (
    mess_ID int NOT NULL, #訊息編號
    cust_ID int NOT NULL, #客戶編號
    date  TIMESTAMP DEFAULT CURRENT_TIMESTAMP ,  # 留言時間
    credit  int CHECK (credit >= 0 and credit <=5), # 滿意度(最多5顆星)
    pro_ID int, #產品編號
    record CHAR(200), #客戶留言
    
    primary key (mess_ID),
    Foreign Key (cust_ID) References customers(cust_ID),
    Foreign Key (pro_ID) References products(pro_ID)
);
```
```bash
INSERT INTO `messages` (`mess_ID`, `cust_ID`, `date`, `credit`, `pro_ID`, `record`) VALUES (NULL, '1', current_timestamp(), '5', '2', '超級棒');
```



- 建立 sales_detail 資料表

## 訂單明細
```bash
create table sales_detail (
    sales_detail_ID  int NOT NULL, #明細編號
    sales_ID int NOT NULL, #訂單編號
    pro_ID int NOT NULL, #產品編號
    count int CHECK (count > 0) ,  # 訂單數量

    
    primary key (sales_detail_ID),
    Foreign Key (sales_ID) References  sales(sales_ID),
    Foreign Key (pro_ID) References products(pro_ID)
);
```


```bash
INSERT INTO `sales_detail` (`sales_detail_ID`, `sales_ID`, `pro_ID`, `count`) VALUES (NULL, '1', '2', '3');
```











[第十一章 多表格資料庫設計](http://www.tsnien.idv.tw/DataBase_WebBook/%E7%AC%AC%E5%8D%81%E4%B8%80%E7%AB%A0%20%E5%A4%9A%E8%A1%A8%E6%A0%BC%E8%B3%87%E6%96%99%E5%BA%AB%E8%A8%AD%E8%A8%88.html)


[[SA] 資料庫設計-以服飾購物網站為例](http://chancayenne.blogspot.com/2015/08/sa.html)




[MySQL Timestamp 型態 的 屬性(新增/修改 自動更新 Timestamp型態 的 欄位)](https://blog.longwin.com.tw/2007/10/mysql_timestamp_properties_2007/)
