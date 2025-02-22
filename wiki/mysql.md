### 插入语句
> INSERT INTO `pv_p_ai_agent` (origin,image_type) VALUES ("EL-3-1","danjing_9bb_bp_daojiao_6*12")

### inner join
```sql
SELECT
	ph.image_name AS "图片名字",
	air.ai_result_before_data AS "AI过滤前的结果",
	air.ai_result_data AS "AI过滤后的结果",
	air.it_filter_data AS "MES过滤后的结果"
FROM
	`pv_p_ai_result` AS air
	INNER JOIN pv_p_photovoltaic AS ph ON ph.ai_result_id = air.id 
LIMIT 1000
```

### like
```sql
SELECT	pvpbatch.id,
	pvpp.image_name,
	pvpai.id AS ai_resultId,
	pvpp.id AS photovoltaicId /*http://10.123.33.2:8001/pv/back/ai_result_view/?id=448571*/
FROM
	pv_p_batchforecast AS pvpbatch
	INNER JOIN pv_p_photovoltaic AS pvpp ON pvpbatch.id = pvpp.batch_forecast_id
	INNER JOIN pv_p_ai_result AS pvpai ON pvpp.ai_result_id = pvpai.id 
WHERE
	pvpbatch.id IN ( 333, 334, 335, 336, 337, 338 ) 
	AND pvpp.image_name LIKE "%6501039267000993%"
```

### 配置远程访问
```sql
use mysql;
SELECT `Host`,`User` FROM user;
UPDATE user SET `Host` = '%' WHERE `User` = 'root' LIMIT 1;
alter user 'root'@'%' identified with mysql_native_password by 'Zt@2020jt';
ALTER USER 'root'@'%' IDENTIFIED BY 'Zt@2020jt';
flush privileges;
SELECT `Host`,`User` FROM user;
```

### 创建数据库
```sql
CREATE database `ztpanels-haining` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```
### 导入数据库
```sql
source D:/www/sql/back.sql;
```

### mysql-server安装
> 我把数据库的安装包文件放在了/home/admin/software/mysql这个，里面有一个tar包，
> 使用命令tar -xvf mysql-8.0.21-1.el7.x86_64.rpm-bundle.tar进行解压缩，
> 得到几个rpm安装包，在解压缩目录里使用yum -y localinstall *.rpm进行安装

### 启动mysql：
```shell script
#使用 service 启动
service mysqld restart 
systemctl start  mysqld.service
# 启动失败打开日志查看
cat /var/log/mysqld.log
```
