| mysql    | go   | nullable |
| -------- | ---- | ---- |
| tinyint  | int | sql.NullInt64 |
| int      | int | sql.NullInt64 |
| smallint | int | sql.NullInt64 |
| mediumint | int | sql.NullInt64 |
| bigint | int64 | sql.NullInt64 |
| char | string | sql.NullString |
| enum | string | sql.NullString |
| varchar | string | sql.NullString |
| longtext | string | sql.NullString |
| mediumtext | string | sql.NullString |
| text | string | sql.NullString |
| tinytext | string | sql.NullString |
| json | string | sql.NullString |
| date | time.Time | null.Time |
| datetime | time.Time | null.Time |
| time | time.Time | null.Time |
| timestamp | time.Time | null.Time |
| decimal | float64 | sql.NullFloat64 |
| double | float64 | sql.NullFloat64 |
| float | float32 | sql.NullFloat64 |
| binary | []byte |      |
| blob | []byte |      |
| longblob | []byte |      |
| mediumblob | []byte |      |
| varbinary | []byte |      |
|  |      |      |
|  |      |      |
|  |      |      |
|  |      |      |
|  |      |      |
|  |      |      |
|  |      |      |
|  |      |      |





```sql
CREATE TABLE `user_account_tbl` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `account` varchar(64) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `password` varchar(64) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `account_type` int(11) NOT NULL DEFAULT '0' COMMENT '帐号类型:0手机号，1邮件',
  `app_key` varchar(255) CHARACTER SET utf8 COLLATE utf8_unicode_ci NOT NULL COMMENT 'authbucket_oauth2_client表的id',
  `user_info_id` int(11) NOT NULL,
  `reg_time` datetime DEFAULT NULL,
  `reg_ip` varchar(15) CHARACTER SET utf8 COLLATE utf8_general_ci DEFAULT NULL,
  `bundle_id` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci DEFAULT NULL,
  `describ` varchar(255) CHARACTER SET utf8 COLLATE utf8_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE KEY `account` (`account`),
  UNIQUE KEY `UNIQ_5696AD037D3656A4` (`app_key`,`user_info_id`) USING BTREE,
  KEY `user_info_id` (`user_info_id`),
  CONSTRAINT `1` FOREIGN KEY (`user_info_id`) REFERENCES `user_info_tbl` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=29 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci ROW_FORMAT=DYNAMIC COMMENT='用户信息'
```





| 标签名     | 说明                                                         |
| :--------- | :----------------------------------------------------------- |
| column     | 指定 db 列名                                                 |
| type       | 列数据类型，推荐使用兼容性好的通用类型，例如：所有数据库都支持 bool、int、uint、float、string、time、bytes 并且可以和其他标签一起使用，例如：`not null`、`size`, `autoIncrement`… 像 `varbinary(8)` 这样指定数据库数据类型也是支持的。在使用指定数据库数据类型时，它需要是完整的数据库数据类型，如：`MEDIUMINT UNSINED not NULL AUTO_INSTREMENT` |
| size       | 指定列大小，例如：`size:256`                                 |
| primaryKey | 指定列为主键                                                 |
| unique     | 指定列为唯一                                                 |
| default    | 指定列的默认值                                               |
| precision  | 指定列的精度                                                 |





```
type InsInfo struct {
// 列名字 ， 
	Connections  string    `gorm:"column:connections"`
}
```



```java
//  用户信息
type UserAccountTbl struct {
    ID          int       `gorm:"primaryKey;column:id;type:int(11);not null" json:"-"`                                                   //
    Account     string    `gorm:"unique;column:account;type:varchar(64);not null" json:"account"`                                         //
    Password    string    `gorm:"column:password;type:varchar(64);not null" json:"password"`                                              //
    AccountType int       `gorm:"column:account_type;type:int(11);not null" json:"account_type"`                                         
        //    帐号类型:0手机号，1邮件
    AppKey      string    `json:"app_key" gorm:"unique_index:UNIQ_5696AD037D3656A4;column:app_key;type:varchar(255);not null"`            //    authbucket_oauth2_client表的id
    UserInfoID  int       `gorm:"unique_index:UNIQ_5696AD037D3656A4;index;column:user_info_id;type:int(11);not null" json:"user_info_id"` //
    RegTime     time.Time `gorm:"column:reg_time;type:datetime" json:"reg_time"`                                                          //
    RegIP       string    `gorm:"column:reg_ip;type:varchar(15)" json:"reg_ip"`                                                           //
    BundleID    string    `json:"bundle_id" gorm:"column:bundle_id;type:varchar(255)"`                                                    //
    Describ     string    `gorm:"column:describ;type:varchar(255)" json:"describ"`                                                        //
}
```