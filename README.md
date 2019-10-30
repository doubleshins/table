# table
## 電商平台

![](https://i.imgur.com/MNvsTQM.png)

- 建立 customers 資料表

## 客戶資料
```bash
create table customers (
    cust_ID char(20) NOT NULL,
    name  char(20) NOT NULL, # 姓名
    sex  char(1) CHECK (sex IN ('男', '女')), # 性別
    phone char(10) UNIQUE NOT NULL, # 行動電話
    age  int CHECK (age>0 and age<=180), # 年齡
    email  char(50) UNIQUE NOT NULL, # 電子信箱
    address  char(50) NOT NULL, # 地址
    
    CONSTRAINT check_phone CHECK (phone like '09________%'),
    primary key (cust_ID)
);
```




- 建立 products 資料表

## 產品
```bash
create table products  (
    pro_ID int auto_increment NOT NULL, 
    name varchar(50) NOT NULL,  # 名稱
    price int NOT NULL,  # 單價
    inventory int NOT NULL, # 庫存量
    descr varchar(200),  # 產品說明
    added_date  TIMESTAMP DEFAULT CURRENT_TIMESTAMP, # 上架時間
    is_on_sale boolean NOT NULL default true, # 是否上架
    
    primary key( pro_ID)      # 主鍵
);
```





- 建立 sales 資料表

## 訂單
```bash
create table sales (
    sales_ID CHAR(20) NOT NULL,
    cust_ID  CHAR(20) NOT NULL,
    pro_ID CHAR(20) NOT NULL,
    
    ip_address  varchar(20), # IP位址
    sales_date_time timestamp NOT NULL, # 訂單日期
    recipient_address varchar(50), # 收件地址
    recipient_phone varchar(10), # 收件人電話
    recipient_remark varchar(100), # 收件備註
   
    
    primary key (sales_ID),
    FOREIGN KEY (cust_ID) REFERENCES customers(cust_ID),
    Foreign Key (pro_ID) References products(pro_ID)
);
```







-  建立 messages 資料表


## 客戶回應訊息
```bash
create table messages (
    mess_ID  int auto_increment, 
    cust_ID  CHAR(20) NOT NULL,
    date  DATE ,  # 留言時間
    credit  int , # 滿意度(最多5顆星)
    manufacture  CHAR(20) , # 製造商
    pro_ID CHAR(20) NOT NULL, # 物品
    record CHAR(200), # 留言
    primary key (mess_ID),
    Foreign Key (cust_ID) References customers(cust_ID),
    Foreign Key (pro_ID) References products(pro_ID)
);
```



- 建立 sales_detail 資料表

## 訂單明細
```bash
create table sales_detail (
    sales_detail_ID  int auto_increment,
    sales_ID CHAR(20) NOT NULL,

    total_price int NOT NULL,  # 總和
    
    ship_status boolean NOT NULL default true, # 是否出貨
    
    primary key (sales_detail_ID),
    Foreign Key (sales_ID) References  sales(sales_ID)
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


- 建立 publishers 資料表
## 銷貨商
```bash
create table publishers (
    pub_ID int auto_increment, # 銷貨商編碼
    pub_name  CHAR(50) NOT NULL,　# 出版商名稱
    contact  CHAR(20) , # 聯絡人
    tel  CHAR(20) , # 電話
    address  CHAR(50) , # 地址
    primary key (pub_ID)
);
```
