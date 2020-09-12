#### 数据库初始化说明

+ 导入数据库脚本`epi.sql`
+ 进入`curl`文件夹路径，执行`npm install`，补全包
+ 执行`node app.js`启动服务器，将数据源中的数据插入数据库

#### 接口整理

|接口地址|请求方式|请求参数|返回示例|备注|
|:---|:---|:---|:---|:---|

#### 数据库设计及说明

-- user表：存放用户信息

|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|uid|用户id|int|primary key,auto_increment|
|unick|用户昵称|varchar()|not null,default|
|uname|用户登录名|varchar()|not null,unique|
|upwd|用户密码|varchar()|not null|
|uavatar|用户头像|varchar()|not null,default|
|ugender|用户性别|enum|default|
|uphone|用户电话号码|int(11)||
|uaddress|用户地址|varchar()||

-- article表：存放防护知识文章信息，疫苗研制最新情况

|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|aid|文章/视频id|int|primary key,auto_increment|
|asubject|文章/视频标题|varchar()|not null|
|aimg|文章/视频封面图|varchar()|not null|
|acontent|文章内容/视频路径|varchar()|not null|
|atime|发布时间|bigint|not null|
|aimport|是否置顶|enum|not null,default|
|type|类型|enum|not null|

-- dynamic表：用户上传动态表

|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|did|动态id|INT|primary key auto_increment|
|dtext|用户动态文本|varchar|not null|
|dimg|用户动态图片路径|varchar||
|dtime|发布时间|bigint|not null|
|uid|用户id|int|not null,foreign key reference|

-- islike表：用户点赞数据

|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|did|动态id|INT|not null,foreign key reference|
|uid|用户id|INT|not null,foreign key reference|

-- donation表：记录捐献数据
|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|did|捐赠物资id|int|primary key,auto_increment|
|dtype|捐赠类型|enum|not null,defalut|
|dname|捐赠物品|enum|not null|
|dcount|捐赠数量|int|not null|
|dcompany|捐赠单位|varchar()|not null|
|dtime|捐赠时间|bigint|not null|
|dstate|捐赠状态|enum|not null,default|
|uid|用户id|int|not null,foreign key reference|

*region_data表：记录区域数据*
|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|pname|省份名称|varchar|not null,unique|
|cname|城市名称|varchar|not null|
|confirm|确诊人数|int|not null|
|suspect|疑似人数|int|not null|
|heal|治愈人数|int|not null|
|dead|死亡人数|int|not null|

*country_data表：记录每个日期全国数据*
|表字段|备注|列类型|列约束|
|:---|:---|:---|:---|
|insert_date|数据插入日期|varchar|not null|
|confirm|确诊人数|int|not null|
|suspect|疑似人数|int|not null|
|heal|治愈人数|int|not null|
|dead|死亡人数|int|not null|
|input|境外输入人数|int|not null|