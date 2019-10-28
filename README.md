# table
## 文創電商平台


- 訂單

## 建立 sales 資料表
```bash
create table sales (
    sales_ID CHAR(20) NOT NULL,

    primary key (sales_ID)
);
```


- 訂單明細

## 建立 sales_detail 資料表
```bash
create table sales_detail (
    cust_ID CHAR(20) NOT NULL,
 
    primary key (cust_ID)
);
```






- 客戶資料

## 建立 customers 資料表
```bash
create table customers (
    cust_ID CHAR(20) NOT NULL,
    name  CHAR(20) NOT NULL,
    sex  CHAR(20) NOT NULL,
    age  int  NOT NULL,
    Email  CHAR(50) ,
    address  CHAR(50) ,
    primary key (cust_ID)
);
```

- 產品

## 建立 products 資料表
```bash
create table products  (
    pro_ID CHAR(20) NOT NULL,
    name varchar(50) NOT NULL,  # 名稱
    descr varchar(200),  # 說明
    price INT NOT NULL,  # 價格
    primary key(clo_ID)      # 主鍵
);
```



- 銷貨商

## 建立 publishers 資料表
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



-  客戶回應訊息


## 建立 messages 資料表
```bash
create table messages (
    mess_ID  int auto_increment, 
    cust_ID  CHAR(20) NOT NULL,
    date  DATE ,  # 留言時間
    credit  int , # 滿意度(最多5顆星)
    manufacture  CHAR(20) , # 製造商
    classify CHAR(20),
    record CHAR(200),
    primary key (mess_ID),
    Foreign Key (cust_ID) References customers(cust_ID)
);
```








## 測試資料
```bash
INSERT INTO `customers` VALUES ('A001', '郭大豪', '男', '20', 'A001@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 800 號')
INSERT INTO `customers` VALUES ('A002', '張彥宏', '男', '21', 'A002@gcloud.csu.edu.tw', '台南市鳥松區澄清路 801 號')
INSERT INTO `customers` VALUES ('A003', '林郁評', '男', '20', 'A003@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 802 號')
INSERT INTO `customers` VALUES ('A004', '劉姵君', '女', '25', 'A004@gcloud.csu.edu.tw', '新北市鳥松區澄清路 803 號')
INSERT INTO `customers` VALUES ('A005', '陸美女', '女', '40', 'A005@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 804 號')
INSERT INTO `customers` VALUES ('A006', '郭大瑋', '男', '30', 'A006@gcloud.csu.edu.tw', '台中市鳥松區澄清路 805 號')
INSERT INTO `customers` VALUES ('A007', '李真樺', '男', '20', 'A007@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 806 號')
INSERT INTO `customers` VALUES ('A008', '陳大志', '男', '30', 'A008@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 807 號')
INSERT INTO `customers` VALUES ('A009', '劉飛翔', '男', '20', 'A009@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 808 號')
INSERT INTO `customers` VALUES ('A010', '郭珊姍', '女', '30', 'A010@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 809 號')
INSERT INTO `customers` VALUES ('A011', '許真人', '男', '30', 'A011@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 810 號')
INSERT INTO `customers` VALUES ('A012', '孫美麗', '女', '40', 'A012@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 811 號')
INSERT INTO `customers` VALUES ('A013', '鄭明明', '女', '40', 'A013@gcloud.csu.edu.tw', '台南市鳥松區澄清路 812 號')
INSERT INTO `customers` VALUES ('A014', '林惠容', '女', '40', 'A014@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 813 號')
INSERT INTO `customers` VALUES ('A015', '林秀氣', '女', '20', 'A015@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 814 號')
INSERT INTO `customers` VALUES ('A016', '陳立人', '男', '40', 'A016@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 815 號')
INSERT INTO `customers` VALUES ('A017', '張婉瑜', '女', '20', 'A017@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 816 號')
INSERT INTO `customers` VALUES ('A018', '郭鴻偉', '女', '18', 'A018@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 817 號')
INSERT INTO `customers` VALUES ('A019', '林克強', '男', '40', 'A019@gcloud.csu.edu.tw', '高雄市鳥松區澄清路 818 號')


INSERT INTO `messages` VALUES ('1', 'A001', '2017/11/14', '3', '真美公司', '衣服', '不想留言')
INSERT INTO `messages` VALUES ('2', 'A002', '2017/11/15', '5', '留洋公司', '褲子', '很好')
INSERT INTO `messages` VALUES ('3', 'A001', '2017/10/20', '4', '真美公司', '帽子', '顏色不對')
INSERT INTO `messages` VALUES ('4', 'A004', '2017/10/21', '5', '上等公司', '衣服', '還好')
INSERT INTO `messages` VALUES ('5', 'A005', '2017/10/22', '3', '真美公司', '鞋子', '還好')
INSERT INTO `messages` VALUES ('6', 'A003', '2017/10/23', '5', '流尚公司', '衣服', '還好')
INSERT INTO `messages` VALUES ('7', 'A007', '2017/10/24', '2', '時尚公司', '外套', '還好')
INSERT INTO `messages` VALUES ('8', 'A004', '2017/10/25', '4', '真美公司', '衣服', '還好留言')
INSERT INTO `messages` VALUES ('9', 'A002', '2017/10/26', '5', '會會公司', '上衣', '還好')
INSERT INTO `messages` VALUES ('10', 'A019', '2017/10/27', '5', '流流公司', '衣服', '真好')
INSERT INTO `messages` VALUES ('11', 'A012', '2017/10/28', '4', '有志公司', '外套', '還好')
INSERT INTO `messages` VALUES ('12', 'A013', '2017/10/29', '2', '美崙公司', '衣服', '還好')
INSERT INTO `messages` VALUES ('13', 'A014', '2017/10/30', '4', '真美公司', '外套', '我的留言')
INSERT INTO `messages` VALUES ('14', 'A015', '2017/10/31', '5', '求美公司', '鞋子', '還好')
INSERT INTO `messages` VALUES ('15', 'A002', '2017/11/1', '5', '真美公司', '衣服', '還好')
INSERT INTO `messages` VALUES ('16', 'A003', '2017/11/2', '4', '真美公司', '衣服', '還好')


INSERT INTO `clothes` VALUES ('骷髏', '棉質製成001', 990)



```

http://www.tsnien.idv.tw/DataBase_WebBook/%E7%AC%AC%E5%8D%81%E4%B8%80%E7%AB%A0%20%E5%A4%9A%E8%A1%A8%E6%A0%BC%E8%B3%87%E6%96%99%E5%BA%AB%E8%A8%AD%E8%A8%88.html



http://chancayenne.blogspot.com/2015/08/sa.html



https://ithelp.ithome.com.tw/articles/10184593
