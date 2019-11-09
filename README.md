# table
## 電商平台


![](https://i.imgur.com/uXIFp5h.png)

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




- 建立 products 資料表

## 產品
```bash
create table products  (
    pro_ID int , #產品編號
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





- 建立 sales 資料表

## 訂單
```bash
create table sales (
    sales_ID int, #訂單編號
    cust_ID  int, #客戶編號
    ip_address  varchar(20), # IP位址
    total_price int NOT NULL,  # 總和
    ship_method char(4) CHECK (ship_method IN ('宅配到府', '超商取貨')), # 運送模式
    pay_method char(4) CHECK (pay_method IN ('ATM轉帳', '貨到付款')), # 付費模式
    recipient_phone varchar(10), # 收件人電話
    recipient_remark varchar(100), # 收件備註
    sales_date_time timestamp DEFAULT CURRENT_TIMESTAMP, # 訂單日期
    sale_status boolean default false, # 是否處理
    
    primary key (sales_ID),
    CONSTRAINT check_recipient_phone CHECK (recipient_phone like '09________'),
    CONSTRAINT check_ip_address CHECK (ip_address like '%.%.%.%'),
    FOREIGN KEY (cust_ID) REFERENCES customers(cust_ID)
);
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



- 建立 sales_detail 資料表

## 訂單明細
```bash
create table sales_detail (
    sales_detail_ID  int , #明細編號
    sales_ID int, #訂單編號
    pro_ID int , #產品編號
    count int CHECK (count > 0) ,  # 數量
    price int CHECK (price > 0),  # 總和
    
    primary key (sales_detail_ID),
    Foreign Key (sales_ID) References  sales(sales_ID),
    Foreign Key (pro_ID) References products(pro_ID)
);
```








## 測試資料
```bash
INSERT INTO `customers` VALUES ('A001', '郭大豪', '男','0984273123', '20', 'A001@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 800 號');
INSERT INTO `customers` VALUES ('A002', '張彥宏', '男','0987627123', '21', 'A002@gcloud.csu.edu.tw', '台南市鳥松區澄清路 801 號');
INSERT INTO `customers` VALUES ('A003', '林郁評', '男','0987627129', '20', 'A003@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 802 號');
INSERT INTO `customers` VALUES ('A004', '劉姵君', '女','0987623239','25', 'A004@gcloud.csu.edu.tw', '新北市鳥松區澄清路 803 號');
INSERT INTO `customers` VALUES ('A005', '陸美女', '女','0987627249', '40', 'A005@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 804 號');


INSERT INTO `messages` VALUES ('1', 'A001', '2017/11/14', '3', '真美公司', '油畫', '不想留言')
INSERT INTO `messages` VALUES ('2', 'A002', '2017/11/15', '5', '留洋公司', '耳環', '很好')
INSERT INTO `messages` VALUES ('3', 'A001', '2017/10/20', '4', '真美公司', '帽子', '顏色不對')
INSERT INTO `messages` VALUES ('4', 'A004', '2017/10/21', '5', '上等公司', '衣服', '還好')



INSERT INTO `clothes` VALUES ('骷髏', '棉質製成001', 990)



```




[第十一章 多表格資料庫設計](http://www.tsnien.idv.tw/DataBase_WebBook/%E7%AC%AC%E5%8D%81%E4%B8%80%E7%AB%A0%20%E5%A4%9A%E8%A1%A8%E6%A0%BC%E8%B3%87%E6%96%99%E5%BA%AB%E8%A8%AD%E8%A8%88.html)


[[SA] 資料庫設計-以服飾購物網站為例](http://chancayenne.blogspot.com/2015/08/sa.html)




[MySQL Timestamp 型態 的 屬性(新增/修改 自動更新 Timestamp型態 的 欄位)](https://blog.longwin.com.tw/2007/10/mysql_timestamp_properties_2007/)
