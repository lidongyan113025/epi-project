## 数据库初始化说明

+ 导入数据库脚本`epi.sql`
+ 进入`curl`文件夹路径，执行`npm install`，补全包
+ 执行`node app.js`启动服务器，将数据源中的数据插入数据库

### 接口整理

#### 省份名称接口
|接口地址|返回方式|请求方式|请求示例|接口备注|
|:---|:---|:---|:---|:---|
|/api/regionpname|json|GET|/api/regionpname|返回省份名称|
##### 请求参数说明
|名称|必填|类型|说明|
|:---|:---|:---|:---|
|/|/|/|/|
##### 返回参数说明
|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码|
|msg|string|返回码描述|
|pname|省份名|
##### JSON返回示例
```json
{
    "code": 200,
    "msg": "请求成功",
    "data": {
        "pname": [
            "湖北",
            "广东",
            "香港",
            "浙江",
            "河南",
            "湖南",
            "安徽",
            "黑龙江",
            "上海",
            "江西",
            "北京",
            "新疆",
            "山东",
            "四川",
            "江苏",
            "重庆",
            "福建",
            "台湾",
            "陕西",
            "河北",
            "辽宁",
            "内蒙古",
            "广西",
            "天津",
            "山西",
            "云南",
            "海南",
            "甘肃",
            "吉林",
            "贵州",
            "宁夏",
            "西藏",
            "澳门",
            "青海"
        ]
    }
}
```

#### 城市名称接口
|接口地址|返回方式|请求方式|请求示例|接口备注|
|:---|:---|:---|:---|:---|
|/api/regioncname|json|GET|/api/regioncname|返回城市名称|
##### 请求参数说明
|名称|必填|类型|说明|
|:---|:---|:---|:---|
|pname|是|string|省份名|
##### 返回参数说明
|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码|
|msg|string|返回码描述|
|pname|城市名|
##### 接口返回示例
```json
{
    "code": 200,
    "msg": "请求成功",
    "data": [
        {
            "cname": "宜昌"
        },
        {
            "cname": "黄石"
        },
        {
            "cname": "黄冈"
        },
        {
            "cname": "荆州"
        },
        {
            "cname": "孝感"
        },
        {
            "cname": "随州"
        },
        {
            "cname": "鄂州"
        },
        {
            "cname": "武汉"
        },
        {
            "cname": "襄阳"
        },
        {
            "cname": "咸宁"
        },
        {
            "cname": "荆门"
        },
        {
            "cname": "潜江"
        },
        {
            "cname": "境外输入人员"
        },
        {
            "cname": "境外输入"
        },
        {
            "cname": "神农架"
        },
        {
            "cname": "恩施州"
        },
        {
            "cname": "仙桃"
        },
        {
            "cname": "天门"
        },
        {
            "cname": "十堰"
        },
        {
            "cname": "未明确地区"
        },
        {
            "cname": "神农架林区"
        },
        {
            "cname": "监狱系统"
        }
    ]
}
```

### 数据库设计及说明

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