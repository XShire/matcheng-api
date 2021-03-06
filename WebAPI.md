
# 电子班牌接口

*   测试接口地址：http://192.168.1.10:9000

## 目录

*   [多文件上传接口](#多文件上传接口)
*   [文件预览接口](#文件预览接口)
*   [文件下载接口](#文件下载接口)

*   [根据设备编号查询班牌信息](#根据设备编号查询班牌信息)
*   [上传班牌基本参数](#上传班牌基本参数)
*   [上传班牌运行状态信息](#上传班牌运行状态信息)
*   [根据班级查询模式切换列表](#根据班级查询模式切换列表)
*   [模式切换时上传新模式](#模式切换时上传新模式)
*   [查询一个班级的班牌设置](#查询一个班级的班牌设置)
*   [发送一条消息](#发送一条消息)
*   [删除一条消息](#删除一条消息)
*   [查询消息列表](#查询消息列表)
*   [查询展示内容列表](#查询展示内容列表)
*   [查询一个班级基本信息](#查询一个班级基本信息)

*   [走班课程开始签到](#走班课程开始签到)
*   [学生走班签到](#学生走班签到)
*   [查询走班考勤列表](#查询走班考勤列表)

*   [人脸搜索](#人脸搜索)
*   [添加一个人脸](#添加一个人脸)
*   [查询一个用户的人脸列表](#查询一个用户的人脸列表)

*   [发送通知](#发送通知)
*   [向班级相册添加图片](#向班级相册添加图片)
*   [查询我发布的通知列表](#查询我发布的通知列表)
*   [查询我发布的图片列表](#查询我发布的图片列表)
*   [我的消息对话](#我的消息对话)


## 接口错误说明

*** 500 JSON示例 ***

```
{
    "timestamp": "2018-05-22 09:45:19",
    "status": 500,
    "error": "Internal Server Error",
    "exception": "java.lang.Exception",
    "message": "班级不存在",
    "path": "/setup/1001100110011001111"
}
```

## 多文件上传接口

```
请求地址：/file/multipart

请求类型：POST

```

#### 返回结果

*** JSON示例 ***

```

[
    {
        "title": "a470dc3d05e45b2a372c179bf4f0e0ae70db67eb!9.jpg",
        "original": "http://127.0.0.1:9001/file/201805251517543851.jpg",
        "state": "SUCCESS",
        "thumb": "http://127.0.0.1:9001/file/201805251517543851.jpg?rules=thumb",
        "url": "201805251517543851.jpg"
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
state | string | 状态
title | string | 文件的原始名称
url | string | 保存文件名（这个是需要保存到数据库的字段）
original | string | 源文件预览路径
thumb | string | 缩略图预览路径


## 文件预览接口

```
请求地址：/file/{fileName}

请求类型：GET

```

#### 返回结果

*** ResponseEntity<?> ***


## 文件下载接口

```
请求地址：/file/download/{fileName}

请求类型：GET

```

#### 返回结果

*** ResponseEntity<InputStreamResource> ***


## 根据设备编号查询班牌信息

```
请求地址：/v1/device/sn/{sn}

请求类型：GET

请求说明：
1、验证班牌是否可用；2、查询或更新班牌基本信息；3、查询当前模式信息

```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
sn | true | string | 设备唯一编号 

#### 返回结果

*** JSON示例 ***

```

{
    "id": 7,
    "title": "电子班牌",
    "model": "品牌型号",
    "intro": "设备说明信息",
    "category": 1,
    "sn": "10000006",
    "bind": 0,
    "tenantId": "",
    "schoolId": "10031002",
    "classId": "1003100210011003",
    "installTime": "2018-05-20 13:36:35",
    "installPlace": "校门口",
    "runStatus": 1,
    "androidVersion": "",
    "softVersion": "",
    "dpi": "",
    "startTime": "",
    "styleId": "",
    "styleTitle": "",
    "createTime": "2018-05-20 13:36:44",
    "updateTime": "2018-05-21 16:43:05",
    "deleted": 0
}

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
title | string | 设备名称
model | string | 设备品牌、型号 
intro | string | 设备说明
category | string | 设备类型：1-班级班牌
sn | string | 设备编号：用于和班牌设备的绑定
bind | int | 是否已经绑定设备：1-已绑定；0-未绑定
tenantId | string | 租户ID
schoolId | string | 学校ID
classId | string | 班级ID
installTime | string | 安装时间
installPlace | string | 安装位置
runStatus | int | 运行状态：1-正常；0-异常
androidVersion | string | 安卓版本
softVersion | string | 班牌软件版本
dpi | string | 分辨率
startTime | string | 上次启动时间
styleId | string | 当前运行模式ID
styleTitle | string | 当前运行模式名称
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是


## 上传班牌基本参数

```
请求地址：/v1/device/{id}

请求类型：POST

请求说明：
1、上传班牌参数；2、上传上次启动时间；3、上传当前运行模式；4、上传信息即绑定当前班牌

```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
androidVersion | false | string | 安卓版本
softVersion | false | string | 班牌软件版本
dpi | false | string | 分辨率
startTime | false | string | 上次启动时间
styleId | false | string | 当前运行模式ID

#### 返回结果

*** 返回值为空 ***


## 上传班牌运行状态信息

```
请求地址：/v1/check/

请求类型：POST

请求说明：
上传班牌运行状态信息，并将状态信息同步到班牌基本信息中

```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
deviceId | true | string | 设备ID
runStatus | true | string | 运行状态：1-正常；0-异常
image | false | string | 班牌截图
styleId | false | string | 当前运行模式ID
network | false | string | 网络模式
ramAll | false | int | 班牌内存，单位：KB
ramFree | false | int | 可用内存，单位：KB
romAll | false | int | 班牌存储，单位：KB
romFree | false | int | 可用存储，单位：KB
softVersion | false | string | 班牌软件版本

#### 返回结果

*** 返回值为空 ***

## 根据班级查询模式切换列表

```
请求地址：/v1/style-change/{classId}

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
classId | false | string | 班级ID

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 1,
        "schoolId": "10011001",
        "schoolName": "中国儿童中心实验幼儿园",
        "classId": "1001100110011001",
        "className": "大（1）班",
        "styleId": 1,
        "styleName": "公告模式",
        "changeTime": "1970-01-01 16:30:00",
        "createTime": "2018-05-20 15:15:03",
        "updateTime": "2018-05-20 15:24:14",
        "deleted": 0
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
schoolId  | string | 学校ID
schoolName | string | 学校名称 
classId | string | 班级ID
className | int | 班级名称
styleId | int | 切换模式ID
styleName | string | 模式名称
changeTime | string | 切换模式时间，有效值为时间，日期无效
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是


## 模式切换时上传新模式

```
请求地址：/v1/device/{id}/style

请求类型：POST
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
id | true | int | 设备ID 
styleId | true | int | 新模式ID 

#### 返回结果

*** 返回值为空 ***


## 查询一个班级的班牌设置

```
请求地址：/v1/setup/{classId}

请求类型：GET

```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
classId | true | string | 班级ID 

#### 返回结果

*** JSON示例 ***

```

{
    "id": 1,
    "schoolId": "10011001",
    "schoolName": "中国儿童中心实验幼儿园",
    "classId": "1001100110011001",
    "className": "大（1）班",
    "fontSize": "",
    "fontColor": "#F0F0F0",
    "playType": 1,
    "playSpeed": 2,
    "playShow": 30,
    "openTime": "1970-01-01 10:30:00",
    "closeTime": "",
    "brightness": 80,
    "contrast": 50,
    "volume": 50,
    "createTime": "2018-05-21 13:44:46",
    "updateTime": "2018-05-21 13:46:16",
    "deleted": 0
}

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
schoolId  | string | 学校ID
schoolName | string | 学校名称 
classId | string | 班级ID
className | string | 班级名称
fontSize | int | 文字大小
fontColor | string | 文字颜色
playType | int | 播放方式：1-左右滚动；2-上下滚动；3-静止；4-不显示；默认1
playSpeed | int | 播放速度，play_type为1或2时生效：1-慢速；2-中速；3-快速；默认2
playShow | int | 查看显示时间：10秒、30秒、60秒、只允许刷卡关闭（999999秒）；默认30秒
openTime | string | 开机时间，格式为“1970-01-01 10:30:00”，有效值为时间，日期为补偿字符串
closeTime | string | 关机时间，格式为“1970-01-01 10:30:00”，有效值为时间，日期为补偿字符串
brightness | int | 屏幕亮度（百分比，0到100的整数）
contrast | int | 对比度（百分比，0到100的整数）
volume | int | 音量（百分比，0到100的整数）
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是



## 发送一条消息

```
请求地址：/v1/message/

请求类型：POST
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
schoolId | true | string | 学校ID 
classId | true | string | 班级ID 
senderUsername | true | string | 发送人username
receiverUsername | true | string | 接收人username 
msgType | true | int | 消息类型：1-文本消息；2-图片消息；默认1
msgSource | true | int | 消息发送平台：1-APP；2-电子班牌；默认1
msgContent | true | string | 消息内容

#### 返回结果

*** 返回值为空 ***


## 删除一条消息

```
请求地址：/v1/message/{id}

请求类型：DELETE
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
id | true | int | 菜单ID

#### 返回结果

*** 返回值为空 ***


## 查询消息列表

```
请求地址：/v1/message/list

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
schoolId | false | string | 学校ID
classId | false | string | 班级ID
senderUsername | false | string | 发送人username
receiverUsername | false | string | 接收人username
msgContent | false | string | 消息内容
msgContent | false | string | 消息内容
readStatus | false | int | 是否已读：0-未读；1-已读；为空时查询全部
page | false | int | 页码
limit | false | int | 每页显示条数

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 1,
        "schoolId": "10010001",
        "classId": "1001000110010002",
        "senderUsername": "1001150925154536025",
        "senderName": "安辰朗",
        "receiverUsername": "1001150925154537031",
        "receiverName": "张桐赫",
        "msgType": 1,
        "msgSource": 1,
        "readStatus": 0,
        "readTime": "",
        "createTime": "2018-05-22 10:41:42",
        "updateTime": "2018-05-22 10:41:42",
        "deleted": 0,
        "msgContent": "这是发送为班牌的文本消息"
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | 菜单ID
schoolId  | string | 学校ID
classId | string | 班级ID 
senderUsername | string | 发送人username
senderName | string | 发送人姓名
receiverUsername | string | 接收人username
receiverName | string | 接收人姓名
msgType | string | 消息类型：1-文本消息；2-图片消息；默认1
msgSource | string | 消息发送平台：1-APP；2-电子班牌；默认1
readStatus | int | 是否已读：0-未读；1-已读；默认0
readTime | string | 读取时间
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是
msgContent | string | 消息内容：文本消息是文本内容，图片消息是图片路径


## 查询展示内容列表

```
请求地址：/v1/content-show/list

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
classId | true | string | 班级ID
blockId | true | int | 区块ID
contentType | false | int | 内容类型：1-文章；2-相册；3-视频
page | true | int | 分页页数 
limit | true | int | 每页显示条数

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 2,
        "contentType": 1,
        "contentId": 1,
        "contentTitle": "杭州下大雨",
        "contentBody": "看见就看看水水水水水",
        "schoolId": "10010001",
        "schoolName": "中国儿童早教基地",
        "blockId": 3,
        "blockTitle": "班级窗口3",
        "classId": "1001000110010010",
        "className": "周六(1)班",
        "beginTime": "2018-05-21 10:30:00",
        "endTime": "2018-05-25 10:30:00",
        "createTime": "2018-05-21 20:30:00",
        "updateTime": "2018-05-21 20:30:00"
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
contentType  | string | 内容类型：1-文章；2-相册；3-视频
contentId | string | 内容ID：对应文章、相册、视频的ID 
contentTitle | string | 内容标题
contentBody | int | 内容主体
schoolId | int | 学校ID
schoolName | string | 学校名称
blockId | string | 班牌区块ID
blockTitle | string | 区块标题
classId | string | 班级ID
className | string | 班级名称
beginTime | string | 展示开始时间
endTime | string | 展示结束时间
createTime | string | 创建时间
updateTime | string | 修改时间


## 查询一个班级基本信息

```
请求地址：/v1/organization/class/{classId}

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
classId | true | string | 班级ID 

#### 返回结果

*** JSON示例 ***

```

{
    "classID": "1003100110011002",
    "className": "正常班级",
    "tenantId": "18790591074",
    "createTime": "2016-08-11 09:40:55",
    "logo": "",
    "slogan": "",
    "remark": "",
    "headTeacher": "杨小拉"
}

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
classID | string | 班级ID
className  | string | 班级名称
tenantId | string | 集团ID 
createTime | string | 创建时间
logo | string | logo
slogan | string | 班级口号
remark | string | 班级介绍
headTeacher | string | 班主任


## 走班课程开始签到

```
请求地址：/v1/course/sign/signs

请求类型：POST
```

#### 请求参数
字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
curriculumId | true | int | 走班课表ID

#### 返回结果

*** 返回值为空 ***


## 学生走班签到

```
请求地址：/v1/course/sign/sign

请求类型：POST
```

#### 请求参数
字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
curriculumId | true | int | 走班课表ID
studentId | true | string | 学生ID
signTime | true | string | 签到时间，格式为“2018-05-29 09:20:00”
image | false | string | 考勤拍照照片，一般为图片上传后返回的文件名

#### 返回结果

*** 返回值为空 ***



## 查询走班考勤列表

```
请求地址：/v1/course/sign/list

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
courseId | false | int | 走班课程ID
curriculumId | false | int | 走班课表ID
studentId | false | string | 学生ID
studentClassId | false | string | 学生所在物理班级ID
page | false | int | 分页页数 
limit | false | int | 每页显示条数

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 6,
        "courseId": 1,
        "curriculumId": 1,
        "studentId": "17092701111654847",
        "studentName": "何梓鑫",
        "studentClassId": "1006100410011010",
        "signTime": "1970-01-01 09:30:00",
        "signStatus": 1,
        "image": "201805240941309670.jpg",
        "createTime": "2018-05-29 11:21:02",
        "updateTime": "2018-05-29 11:36:47",
        "deleted": 0,
        "imageThumb": "http://127.0.0.1:9001/file/201805240941309670.jpg?rules=thumb"
    }
]

```

#### 返回参数
字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
courseId  | int | 走班课程ID
curriculumId | int | 走班课表ID
studentId | string | 学生ID
studentName | string | 学生姓名
studentClassId | string | 学生所在物理班级ID
signTime | string | 签到时间
signStatus | int | 签到状态：1-正常、2-迟到、3-未签到；默认3
image | string | 考勤拍照照片
createTime | string | 创建时间
updateTime | string | 修改时间
imageThumb | string | 考勤照片的缩略图路径


## 查询班级的有效通知列表

```
请求地址：/v1/notice/available

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
classId | false | string | 班级ID，为空时查询全部通知
page | false | int | 分页页数，默认1
limit | false | int | 每页显示条数，默认1000

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 1,
        "schoolId": "10010001",
        "schoolName": "中国儿童早教基地",
        "classIds": "1001000110010002,1001000110010010,1001000110011001,1001000110011002",
        "classNames": "周六(2)班,周六(1)班,平时(1)班,平时(2)班",
        "content": "发送一条学校通知",
        "publishUsername": "18790591074",
        "publishName": "系统管理员",
        "beginTime": "2018-05-05 09:00:00",
        "endTime": "2018-06-09 09:00:00",
        "createTime": "2018-05-29 14:17:44",
        "updateTime": "2018-05-29 14:20:13",
        "deleted": 0
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
schoolId  | string | 学校ID
schoolName | string | 学校名称 
classIds | string | 班级ID，多个以逗号隔开
classNames | string | 班级名称，多个以逗号隔开
content | string | 通知内容
publishUsername | string | 发布人用户名
publishName | string | 发布人姓名
beginTime | string | 展示开始时间
endTime | string | 展示结束时间
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是


## 人脸搜索

```
请求地址：/v1/face/search

请求类型：POST
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
file | true | MultipartFile | 人脸图片
schoolId | true | string | 学校ID

#### 返回结果

*** JSON示例 ***

```

{
	"username": "1003170227105333596",
	"nickname": "阿拉丁",
	"studentId": "123456",
	"classId": "1003100110011002",
	"className": "正常班级",
	"schoolId": "10031001",
	"schoolName": "媒成科技有限公司",
	"score": 99.999084
}

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
username  | string | 用户名
nickname | string | 姓名 
studentId | string | 学生ID
classId | string | 班级ID
className | string | 班级名称
schoolId | string | 学校ID
schoolName | string | 学校名称
score | number | 匹配度，0 到 100


## 添加一个人脸

```
请求地址：/v1/face/face

请求类型：POST
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
file | true | MultipartFile | 人脸正面清晰的图片
schoolId | true | string | 学校ID
classId | true | string | 班级ID
username | true | string | 用户名

#### 返回结果

*** 空 ***


## 查询一个用户的人脸列表

```
请求地址：/v1/face/{username}/faces

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
username | true | string | 用户名

#### 返回结果

*** JSON示例 ***

```

[
    {
        "image": "201806191848372325.jpg",
        "thumb": "http://127.0.0.1:9000/file/201806191848372325.jpg?rules=thumb",
        "original": "http://127.0.0.1:9000/file/201806191848372325.jpg?rules=original"
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
image  | string | 图片名称
thumb | string | 缩略图路径 
original | string | 原图路径



## 发送通知

```
请求地址：/v1/notice/?username={username}

请求类型：POST
```

#### 请求参数

字段   |   是否必选    |   字段类型   |   字段说明
------  |  --------- | ----------- |  -----------
username | true | string | 用户名，作为param参数调用
schoolId | true | string | 学校ID
classIds | true | string | 班级ID，多个以逗号","隔开
content | true | string | 通知内容

#### 返回结果

*** 返回值为空 ***


## 向班级相册添加图片

```
请求地址：/v1/picture/?username={username}

请求类型：POST
```

#### 请求参数

字段   |   是否必选    |   字段类型   |   字段说明
------  |  --------- | ----------- |  -----------
username | true | string | 用户名，作为param参数调用
schoolId | true | string | 学校ID 
classIds | true | string | 班级ID，多个以逗号","隔开
titles | true | string | 多张图片的标题，以逗号","隔开
images | true | string | 多张图片的路径，以逗号","隔开
blockId | true | int | 班牌区块ID，1-小黑板；2-班级之星；3-主窗口

#### 返回结果

*** 返回值为空 ***


## 查询我发布的通知列表

```
请求地址：/v1/notice/{username}/notices?page={page}&limit={limit}

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
username | true | string | 发布人用户名
page | false | int | 分页页数 
limit | false | int | 每页显示条数

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 1,
        "schoolId": "10010001",
        "schoolName": "中国儿童早教基地",
        "classIds": "1001000110010002,1001000110010010,1001000110011001,1001000110011002",
        "classNames": "周六(2)班,周六(1)班,平时(1)班,平时(2)班",
        "content": "发送一条学校通知",
        "publishUsername": "18790591074",
        "publishName": "系统管理员",
        "beginTime": "2018-05-05 09:00:00",
        "endTime": "2018-06-09 09:00:00",
        "createTime": "2018-05-29 14:17:44",
        "updateTime": "2018-05-29 14:20:13",
        "deleted": 0
    }
]

```

#### 返回参数
字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
schoolId  | string | 学校ID
schoolName | string | 学校名称 
classIds | string | 班级ID，多个以逗号隔开
classNames | string | 班级名称，多个以逗号隔开
content | string | 通知内容
publishUsername | string | 发布人用户名
publishName | string | 发布人姓名
beginTime | string | 展示开始时间
endTime | string | 展示结束时间
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是



## 查询我发布的图片列表

```
请求地址：/v1/picture/{username}/pictures?page={page}&limit={limit}

请求类型：GET
```

#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
username | true | string | 发布人用户名
page | false | int | 分页页数 
limit | false | int | 每页显示条数

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 1,
        "schoolId": "10010001",
        "schoolName": "中国儿童早教基地",
        "classIds": "1001000110010002,1001000110010010,1001000110011001,1001000110011002",
        "classNames": "周六(2)班,周六(1)班,平时(1)班,平时(2)班",
        "title": "图片修改1",
        "image": "/upload/image1.jpg",
        "publishUsername": "18790591074",
        "publishName": "系统管理员",
        "createTime": "2018-05-22 06:24:43",
        "updateTime": "2018-05-22 06:28:38"
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | ID
schoolId  | string | 学校ID
schoolName | string | 学校名称 
classIds | string | 班级ID，多个以逗号隔开
classNames | string | 班级名称，多个以逗号隔开
title | string | 文章标题
image | string | 文章内容
publishUsername | string | 发布人用户名
publishName | string | 发布人姓名
createTime | string | 创建时间
updateTime | string | 修改时间

## 我的消息对话

*   学生刷卡拍照和家长在app发给学生的留言

```
请求地址：/v1/message/myMessages?username={username}&page={page}&limit={limit}

请求类型：GET
```
#### 请求参数

字段   |   是否必选    |   字段类型   |字段说明
------  |  -----------|-------------|-----------
username | true | string | 用户名
page | false | int | 分页页数 
limit | false | int | 每页显示条数

#### 返回结果

*** JSON示例 ***

```

[
    {
        "id": 1,
        "schoolId": "10010001",
        "classId": "1001000110010002",
        "senderUsername": "1001150925154536025",
        "senderName": "安辰朗",
        "receiverUsername": "1001150925154537031",
        "receiverName": "张桐赫",
        "msgType": 1,
        "msgSource": 1,
        "readStatus": 0,
        "readTime": "",
        "createTime": "2018-05-22 10:41:42",
        "updateTime": "2018-05-22 10:41:42",
        "deleted": 0,
        "msgContent": "这是发送为班牌的文本消息"
    }
]

```

#### 返回参数

字段    |   字段类型   |字段说明
-----------|-------------|-----------
id | int | 菜单ID
schoolId  | string | 学校ID
classId | string | 班级ID 
senderUsername | string | 发送人username
senderName | string | 发送人姓名
receiverUsername | string | 接收人username
receiverName | string | 接收人姓名
msgType | string | 消息类型：1-文本消息；2-图片消息；默认1
msgSource | string | 消息发送平台：1-APP；2-电子班牌；默认1
readStatus | int | 是否已读：0-未读；1-已读；默认0
readTime | string | 读取时间
createTime | string | 创建时间
updateTime | string | 修改时间
deleted | int | 是否删除：0-否；1-是
msgContent | string | 消息内容：文本消息是文本内容，图片消息是图片路径