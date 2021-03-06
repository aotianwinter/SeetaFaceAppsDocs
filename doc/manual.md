# 中科视拓人脸识别系统用户手册

## 1.功能目录

* 系统信息
	
	* 系统配置
	
* 人员信息
    * 字段管理
    * 人员管理
    
* 设备信息
    * 设备管理
    * 设备组管理
    * 流媒体管理
    * 时间管理
    
* 记录信息
    * 通行记录
    * 日志记录
    
    


## 2.系统展示
![](./image/login.jpg)

 <center>登录界面</center>

![](./image/notify.png)

<center>设备状态变更提醒</center>

系统会监控设备状态，设备状态变更时会上报提醒。例：设备离线、摄像头异常、应用显示异常。




### 2.1 系统信息
#### 2.1.1 系统配置
查看系统配置：

![20190905141220](./image/list.png)



<center>图 2-1-2 查看配置参数</center>

编辑系统配置：

![20190905141443](./image/system.png)

<center>图 2-1-2 编辑配置参数</center>

1.服务器地址：后台服务器回调地址（错误地址会导致照片信息、日志上报等功能无法正常使用）；


示例一：http://192.168.0.8:9090  

示例二：https://seeta.aibuilding.com

2.开放云地址：人脸识别开放云地址，填写正确地址可启用人脸识别功能。


填写格式：`http://<api_key>:<secret_key>@ip:port/params`

示例一：http://127.0.0.1:9180/seetacloud/cpp/detect 

示例二：https://api_key:secret_key@cloud.seetatech.com/api/face/detect


3.设备展示字段：绑定字段后，安卓硬件会显示该字段信息；
4.IC卡: 绑定字段后，填写正确的IC卡后，用户可以刷IC卡
5.身份证：绑定字段后，人员可以在人证一体机上刷身份证进行人员1:1识别。
6.二维码：绑定相关字段后，人员刷二维码后进行人脸识别验证；

### 2.2 人员信息

#### 2.2.1 字段管理
动态管理人员信息字段。

![](image/add_field.png)

<center>图 2-2-1-1 添加字段 </center>

![](image/del_field.png)

<center>图 2-2-1-1 删除字段 </center>

删除字段时，需要输入删除的字段的名称，进行二次确认。

#### 2.2.2 人员管理

管理系统内人员信息，可以添加、编辑、删除人员、查看二维码信息。
![](image/user_list.png)



点击二维码按钮：会自动生成二维码图片,点击下载按钮，可以下载二维码
<br>
![](image/qr_code.png)

人员信息有三部分组成：**动态字段信息、权限（设备、设备组）、照片**。
动态字段：字段管理中添加的字段属性信息；
权限：支持该人员识别的特定设备或设备组；

![](image/edit_member.png)

<center>图 2-2-2-1 编辑人员信息 </center>


> 照片建议规格：

    * 人脸区域大于100*100且无遮挡、五官清晰；
    * 建议人脸左右调度<20°，上下偏转< 15°；
<img src="image/member.jpg" width="25%">

<center>图 2-2-2-2 照片示例 </center>

### 2.3 设备信息

#### 2.3.1 设备管理

目前支持的设备类型：门禁机、人证一体机、智能网关

管理后台具有增加、编辑、应答和批量升级设备功能。可通过设备名称和设备编号可查询设备信息。

![](image/device_list.jpg)

<center>图 2-3-1-1 设备列表 </center>

系统默认显示设备名称、设备编码、设备类型、设备状态。

设备状态：

- 绿色：设备正常运行
- 红色：设备离线

添加：设备中的编码为前接入设备管理平台的设备。
![](image/add_device.png)

<center>图 2-3-1-2 添加设备 </center>

编辑：门禁机、人证一体机 类型的设备，可编辑流媒体参数。智能网关类型设备，则可增减流媒体

![](image/edit_device_params.png)

<center>图 2-3-1-2 编辑设备(1) </center>

>上报地址：设备识别结果的第三方上报地址
>
>设备屏保：关闭时，设备将会一直处于识别界面

![](image/edit_camera_params.png)

<center>图 2-3-1-2 编辑设备(2) </center>

> 核心流参数详情：
>
> 1:n验证阈值：识别类型为 比对搜索，二维码人脸识别时，得分低于此阈值的记录将验证不通过
>
> 1:1验证阈值：识别类型为 认证对比，认证鉴权时，得分低于此阈值的记录将验证不通过
>
> 最小清晰度：抓拍照片的最小清晰度阈值，低于此阈值的照片将被过滤
>
> 最小人脸宽度：抓拍照片人脸的最小宽度，低于此阈值的照片将被过滤
>
> 最大人脸角度：抓拍照片的人脸左右，上下偏转角度，高于此阈值的照片将被过滤
>
> 上报未识别人员：当此开关开启时，识别未通过的记录也将会存储在通行记录中



应答：检测设备声音、补光灯、摄像头状态。点击“应答”按钮，设备补光灯亮起并发出滴滴声音。

删除：删除设备后，设备中的信息（人员信息、设备参数、时间模板）都会清空。

升级：可选中多台设备，上传apk文件，对设备进行升级。（低于设备当前版本的apk将会升级失败）



#### 2.3.2 设备组管理

组管理具有添加、编辑和删除组的功能。
设备组规则：

1. 每一台设备只隶属一个组，不支持跨组。
2. 清空组中的设备后才可以删除组
3. 将设备添加入设备组后，设备组的参数将会覆盖原本设备参数

![](image/group.png)

<center>图 2-3-2-1 设备组列表 </center>

#### 2.3.3 流媒体管理

管理智能网关所需要的IP摄像头的RTSP流地址、摄像头类型、时间模板。

![](image/add_stream.png)

<center>图 2-3-3-1 添加流媒体 </center>

#### 2.3.4 时间管理
统一管理设备允许和禁止通行的时间。

![](image/time_template.png)

<center>图 2-3-4-1 添加时间模板 </center>

通行日期区间：系统允许的通行时间段（精确到日）；
停用日期区间：对于通行时间段内，指定不可通行的时间段；
通行时间区间：每天允许的通行时间（精确到秒）
去除周六日：开启后，排除通行日期区间内所有周六日，人员无法进行人脸识别。
特殊通行日期： 当系统开启周六日后，人员不可认识，如需要人员通行，可选择为特殊时间；



### 2.4. 记录信息

#### 2.4.1 通行记录
通行记录为设备人脸识别的结果汇总，记录设备名称、设备编号、底库照片、现场识别照片、相似度、是否通通行时间。

![通行记录](image/record.png)

<center>图 2-4-1-1 通行记录 </center>

导出：导出当前页面的通行记录到excel表格

![](image/export_record.png)

<center>图 2-4-1-2 导出通行记录 </center>

统计：统计每个人员的每日最早和最晚的通行记录时间，并导出到excel表格

![](image/exporthistory.png)

<center>图 2-4-1-3 统计人员每日早晚通行 </center>

#### 2.4.2 日志记录

记录系统内设备运行和异常日志。可通过设备编码和日期联合查询设备日志记录。
日志记录包含设备名称、设备编码、内容和记录时间等核心信息。
![](image/error_log.png)

<center>图 2-4-2-1 日志记录 </center>
