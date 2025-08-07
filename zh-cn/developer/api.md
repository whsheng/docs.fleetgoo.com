## API 使用说明

1. 本文档中列出的所有API均支持HTTP调用。  
2. API调用的域名为：``open.4s12580.com``。  
3. API调用需要授权。请在API调用的URL中添加请求参数`appkey`（区分大小写，请使用小写）。您可在登录控制台后，在应用信息页面获取您的`appkey`。  
4. 每个API的具体请求语法，包括URI、Header、查询参数（含appkey）、Post参数及返回参数，请参见各API的详细说明。  
5. 本文档中涉及的所有API URL、参数和返回字段必须严格匹配定义的大小写和数据类型。

> 最后更新: 2025/08/07 by Honsen

---



### 1. 获取设备基本信息

```
GET /open/v1/getdevicebaseinfo
```

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **appkey**    | string| 接口请求APPKEY        |
| **device_id** | string| 设备ID，填写IMEI即可  |

**返回结果**

| 字段       | 类型  | 说明                            |
| ---------- | -------------- | ---------------------- |
| **error**  | integer | 错误码，0成功，非0失败        |
| **reason** | string   | 提示                         |
| **result** | object | 结果                    |

**result**

| 字段                  | 类型               | 说明                                                           |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **active_time**         | string           | 设备激活时间                                                   |
| **brand**             | string            | 设备型号                                                        |
| **camera_channel**    | array      | 已经启用的通道号列表,integer数组格式                            |
| **camera_count**       | integer            | 设备摄像头个数                                                |
| **create_time**      | string             | 设备创建时间                                                    |
| **device_form** | integer | 设备物理形态，按位存储，多种形态并存时按位取值，0x01:有线定位器, 0x02:无线定位器, 0x04:OBD, 0x08:记录仪, 0x16:后视镜, 0x32:大屏车机   |
| **device_id**   | string  | 设备ID，填写IMEI即可                                           |
| **device_name**| string  | 设备名称                                                        |
| **factory**   | string    | 设备厂家                                                       |
| **iccid**     | string    | Sim卡ICCID                                                     |
| **network_type** | integer  | 网络制式，0-2G, 1-3G, 2-4G, 3-5G                              |
| **ops_state**  | integer   | 设备运营状态，0-正常状态 3-未开通 4-服务已过期待续费 6-报停 7-已续费待上线激活 8-未使用 9-已销户 其他状态未使用  |
| **typeid**     | integer    | 设备类型ID                                                   |
| **update_time** | string    | 设备修改时间                                                 |
| **total_space** | integer    | SD卡总容量（单位：MB）                                                 |
| **used_space** | integer    | SD卡已使用容量（单位：MB）                                                 |


### 2. 获取设备在线状态

```
GET /open/v1/getdeviceonlinestatus
```

**参数**

| 字段                  | 类型               | 说明                      |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **appkey**     | string| 接口请求APPKEY        |
| **device_id**  | string| 设备ID，填写IMEI即可  |

**返回结果**

| 字段                  | 类型               | 说明                      |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **error**  | integer | 错误码                                                           |
| **reason**  | string | 提示                                                             |
| **result** | object | 结果         |

**result**

| 字段                  | 类型               | 说明                      |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **device_id**  | string| 设备ID，填写IMEI即可            |
| **isonline**   | integer| 设备是否在线， 0-离线，1-在线  |


### 3. 获取设备正在实时视频监控(直播）的观看列表

```
GET /open/v1/getdevicelivestatus
```

**参数**

| 字段                       | 类型    | 说明           |
| ----------------------------- | ------- | -------------------- |
| **appkey**     | string| 接口请求APPKEY         |
| **channel**    | integer| 观看通道号            |
| **device_id**  | string| 设备ID，填写IMEI即可   |

**返回结果**

| 字段                    | 类型    | 说明                                                       |
| --------------------------| ------------------------------------------------------------ | -----------  |
| **error**  | integer  | 错误码                                                           |
| **reason** | string   | 提示                                                             |
| **result**  | object | 结果         |

**result**

获取设备正在实时视频监控(直播)的观看列表结果

| 字段                     | 类型       | 说明                                                                |
| ------------------------------| ------------------------------------------------------------  | -------------------- |
| **channel**    | integer | 观看通道号                                                                 |
| **device_id**  | string | 设备ID，填写IMEI即可                                                        |
| **total**      | integer | 当前观看总人数                                                             |
| **watch_list** | array | 观看列表              |

**watch_list**

观看列表结构

| 字段          | 类型                  | 说明                           |
| ------------------------------- | -------------------------------------------- | ------- |
| **client_code** | integer | 拉流用户代码                                  |
| **is_watching** | integer | 是否正在观看                                  |
| **start_time**  | string | 观看开始时间                                   |
| **stop_time**   | string | 观看结束时间，如果当前正在观看，则此字段为空   |

### 4.获取设备的音视频属性

```
GET /open/v1/GetDeviceLiveProperty
```

**参数**

| 字段                         | 类型 | 说明           |
| ----------------------------- | -------------------- | ------ |
| **device_id**  | string| 设备ID，填写IMEI即可  |

**返回结果**

| 字段                | 类型       | 说明                                                       |
| -------------------------- | ----------- | ----------------------------------------------------------- |
| **error**   | integer| 错误码                                                           |
| **reason**  | string| 提示                                                              |
| **result**  | object | 结果         |

**result**

| 字段                        | 类型        | 说明                                                                                   |
| ----------------------------------- | -------------------------------------- | ------------------------------------------------------------ |
| **camera**         | array | 摄像头信息                              |
| **device_name**    | string   | 设备名称                                                                                     |
| **isSupportLive**  | integer  | 是否支持实时视频监控(直播)：1-是,0-否                                                        |
| **isSupportReplay**| integer  | 是否支持历史视频回放：1-是，0-否                                                             |
| **maxLiveChannel** | integer   | 同时支持实时视频监控(直播)的最大通道数                                                      |

**camera**

| 字段                       | 类型          | 说明                                                                                  |
| ----------------------------------- | -------------------------------------- | ------------------------------------------------------------ |
| **channel**   | integer | 摄像头通道号                        |
| **name** | string| 摄像头通道名称  |



### 5. 获取设备历史行程列表

```
POST /open/v1/GetTravelList
```

**参数**

| 字段                      | 类型     | 说明                                                         |
| ------------------------------ | --------------------------------------- | --------------------------------- |
| **begin_time**  | string | 查询开始时间，格式：yyyy-MM-dd HH:mm:ss                            |
| **device_id**   | string  | 设备ID，填写IMEI即可                                              |
| **end_time**    | string | 查询结束时间，格式：yyyy-MM-dd HH:mm:ss                            |
| **page_info**   | object | 分页参数                                |

**page_info**

分页信息

| 字段                         | 类型  | 说明                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |



**返回结果**

| 字段                     | 类型   | 说明                                                        |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer| 错误码                                                             |
| **reason**  | string | 提示                                                               |
| **result**  | object | 获取行程列表  |

**result**

| 字段                       | 类型   | 说明                                                         |
| ----------------------------- | ------------ | ------------------------------------------------------------ |
| **list**       | array | 行程信息列表  |
| **page_info**  | object | 分页信息      |

**list**

| 字段                          | 类型     | 说明                               |
| ---------------------------------- | --------------------------------------- | ------- |
| **avg_speed**       | integer | 行程平均速度，单位km/h                  |
| **celerate**        | string| 急加速                                    |
| **decelerate**      | string| 急减速                                    |
| **drive_score**     | integer | 本次行程驾驶评分                        |
| **max_speed**       | integer| 最大速度,单位km/h                        |
| **over_speed**      | string| 超速速度                                  |
| **start_address**   | string| 行程开始地址说明                          |
| **start_lat**       | string| 行程开始纬度，WGS84坐标系                 |
| **start_lon**       | string| 行程开始经度，WGS84坐标系                 |
| **start_time**      | string| 行程开始时间，格式：yyyy-MM-dd HH:mm:ss   |
| **stop_acc**        | string| 停车未熄火次数                            |
| **stop_address**    | string| 行程结束地址说明                          |
| **stop_lat**        | string | 行程结束纬度，WGS84坐标系                |
| **stop_lon**        | string| 行程结束经度，WGS84坐标系                 |
| **stop_time**       | string| 行程停止时间，格式：yyyy-MM-dd HH:mm:ss   |
| **total_time**      | string| 行程总时间,单位：H                        |
| **travel_id**       | string| 行程ID                                    |
| **travel_mileage**  | string| 行程里程,单位：km                         |
| **travel_oil**      | string| 行程油耗，单位：L                         |

**page_info**

分页信息

| 字段      | 类型| 说明         |
| --------- | -------- | ------- |
| **total** | integer| 总记录数  |



### 6. 获取设备最近一条行程信息

```
POST /open/v1/GetCurrentTravel
```

**参数**

| 字段                          | 类型 | 说明                    |
| ----------------------------- | -------------------- | ---------------- |
| **device_id**  | array | 设备ID，填写IMEI即可,string数组格式 |



**返回结果**



| 字段                  | 类型      | 说明                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**   | integer| 错误码                                                            |
| **reason**  | string | 提示                                                              |
| **result**  | array | 行程信息     |

**result**

| 字段                        | 类型        | 说明                                        |
| ---------------------------------- | ----------------------------------------- | --------------- |
| **avg_speed**     | integer   | 行程平均速度,单位km/h                             |
| **complete**      | integer  | 是否已经完成 0-未完成 1-完成                       |
| **max_speed**     | integer  | 行程熄火的最大速度,单位km/h                        |
| **pos_count**     | integer  | 此行程内上传的轨迹数量                             |
| **remark**        | string   | 备注信息，标示行程启动熄火相关信息                 |
| **start_lat**     | double  | 行程开始的纬度，WGS84坐标系                |
| **start_lon**     | double   | 行程开始的经度，WGS84坐标系               |
| **start_mileage** | double  | 行程开始总里程                             |
| **start_time**    | string  | 行程开始时间，格式：yyyy-MM-dd HH:mm:ss             |
| **stop_lat**      | double  | 行程熄火的纬度，WGS84坐标系                |
| **stop_lon**      | double  | 行程熄火的经度，WGS84坐标系                |
| **stop_time**     | string  | 行程熄火的时间，格式：yyyy-MM-dd HH:mm:ss           |
| **travel_mileage** | integer  | 本次行程里程(单位：m)                             |
| **travel_period**  | integer  | 本次行程时长(单位：秒)                            |



### 7. 获取设备实时位置信息

```
POST /open/v1/GetRealtimeTrackList
```

**参数**

| 字段                     | 类型          | 说明                                                             |
| ---------------------------------- | ------------------------------------------------------------ | ---------------- |
| **device_id**     | array | 设备ID，填写IMEI即可,string数组格式                             |
| **map_coord_type** | integer | 地图坐标系：0-WGS84(默认),1-BD09(百度地图), 2-GCJ02(高德地图、腾讯地图）           |



**返回结果**

| 字段                  | 类型      | 说明                                                        |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer  | 错误码                                                           |
| **reason**  | string | 提示                                                               |
| **result**  | array | 实时轨迹信息  |

**result**

| 字段                        | 类型             | 说明                  |
| --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **acc**         | integer           | acc状态（0-熄火,1-启动）                                                                                         |
| **alarm_desc**       | string    | 最近的报警内容详细说明                                                                                              |
| **alarm_flag**      | integer     | 设备当前是否处于报警状态 0：非报警 1：报警状态                                                                     |
| **alarm_type**       | string      | 最近的报警类型中文说明             |
| **altitude**     | integer             | 海拔，单位m               |
| **beidou_signal**   | integer      | 北斗卫星颗数                                                                                                      |
| **city_name**     | string           | 当前所在城市名称                                                                                                |
| **device_id**      | string       | 设备ID，填写IMEI即可                                                                                               |
| **direct**       | integer         | 方向                                                                                                              |
| **driving_status**    | integer     | 当前车辆行驶状态 0：熄火 1：启动                                                                                 |
| **etc**           | object   | ETC状态信息                                                  |
| **gps_flag**          | integer       | 当前定位标识（0：gps定位 2：基站定位 3：wifi定位）                                                             |
| **gps_lat**       | double           | 当前GPS定位纬度，WGS84坐标系                                                                           |
| **gps_lon**      | double          | 当前GPS定位经度，WGS84坐标系                                                                             |
| **gps_signal**    | integer         | GPS卫星颗数                                                                                                      |
| **gps_time**       | string         | 当前GPS定位时间                                                                                                  |
| **gsm_signal**      | integer      | GSM信号强度                                                                                                       |
| **is_online**       | integer      | 当前设备在线状态 0：离线 1：在线                                                                                  |
| **lbs_lat**         | double        | 最近的基站定位纬度，WGS84坐标系                                                                         |
| **lbs_lon**       | double         | 最近的基站定位经度，WGS84坐标系                                                                          |
| **lbs_time**        | string        | 最近的基站定位时间                                                                                               |
| **mileage**     | integer          | 当前车辆总里程（单位：m）                                                                                         |
| **oil_num**        | integer       | 油量                                                                                                              |
| **province_name**    | string       | 当前所在省名称                                                                                                   |
| **rcv_time**      | string       | 设备最新的数据接收时间,格式yyyy-MM-dd HH:mm:ss                                                                      |
| **region_name**     | string       | 当前所在行政区名称                                                                                                |
| **speed**        | integer          | 速度,单位km/h                                                                                                    |
| **status_desc**     | string      | 状态说明                                                                                                           |
| **target_gps_lat**    | double      | 当前GPS定位纬度，请求参数map_coord_type指定目标坐标系                                                   |
| **target_gps_lon**   | double      | 当前GPS定位经度，请求参数map_coord_type指定目标坐标系                                                    |
| **target_lbs_lat**   | double      | 最近的基站定位纬度，请求参数map_coord_type指定目标坐标系                                                 |
| **target_lbs_lon**   | double    | 最近的基站定位经度，请求参数map_coord_type指定目标坐标系                                                   |
| **target_wifi_lat**  | double     | 最近的wifi定位经度, 请求参数map_coord_type指定目标坐标系                                                  |
| **target_wifi_lon**  | double    | 最近的wifi定位经度，请求参数map_coord_type指定目标坐标系                                                   |
| **theday_init_mileage** | integer  | 截止当日0时总里程（单位：m），使用总里程mileage-theday_init_mileage可获取当日里程                                                      |
| **voltage**     | integer          | 电池电压                                                                                                          |
| **wifi_lat**      | double          | 最近的wifi定位纬度，WGS84坐标系                                                                         |
| **wifi_lon**      | double          | 最近的wifi定位经度，WGS84坐标系                                                                         |
| **wifi_time**    | string         | 最近的wifi定位时间                                                                                                 |
|**temperature** | array | 温度,单位：°C , double数组格式 |
|**humidity** | array | 湿度,单位：%RH, double数组格式 |

**etc**

| 字段              | 类型                   | 说明                          |
| ------------------------------------ | ---------------------------------- | ------- |
| **bind_state**      | integer  | ETC绑定标志: 0-未绑定, 1-已绑定 ）  |
| **elec_state**       | integer | OBU标签电量标志:0-电量弱, 1-正常    |
| **fault_state**      | integer | ETC故障标志 （0：故障 1：正常）     |
| **hardware_version** | string  | ETC硬件版本号                       |
| **lpn**               | string | ETC已绑定的车牌号                   |
| **obu_id**            | string| ETC已绑定的OBU ID                    |
| **software_version**  | string| ETC软件版本号                        |



### 8. 获取设备历史位置信息

```
POST /open/v1/GetHistoryTrackList
```

**参数**

| 字段                     | 类型            | 说明                                                  |
| ---------------------------------- | ------------------------------------------------------------ | ------- |
| **device_id**    | string   | 设备ID，填写IMEI即可                                           |
| **start_time**     | string | 开始时间,格式yyyy-MM-dd HH:mm:ss                               |
| **end_time**    | string    | 结束时间,格式yyyy-MM-dd HH:mm:ss                               |
| **exact**     | integer      | 0:不过滤 2:过滤基站定位 3:过滤所有非GPS定位                   |
| **limit**    | integer        | 按照时间升序排序的最大轨迹数量                               |
| **map_coord_type** | integer | 地图坐标系：0-WGS84(默认),1-BD09(百度地图), 2-GCJ02(高德地图、腾讯地图）  |
| **speed_limit**    | integer | 速度过滤 -1-不过滤 0-速度值小于5km/h的轨迹会被过滤 大于0-速度值小于此值的轨迹会被过滤  |



**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                                               |
| **result**  | array | 历史轨迹信息  |

**result**

| 字段                     | 类型      | 说明                                          |
| ------------------------------ | ------------------------------------------ | --------------- |
| **bd_lat**      | double| 百度地图纠偏后的纬度                        |
| **bd_lon**      | double| 百度地图纠偏后的经度                        |
| **direct**      | integer| 方向                                                |
| **gps_time**    | string| 定位时间,格式yyyy-MM-dd HH:mm:ss                     |
| **id**          | integer| 设备记录id                                          |
| **lat**         | double| 纬度，WGS84坐标系                           |
| **lon**         | double| 经度，WGS84坐标系                           |
| **mileage**     | double| 总里程（单位：km）                          |
| **pos_mode**    | string| 定位方式                                             |
| **rcv_time**    | string| 接收时间,格式yyyy-MM-dd HH:mm:ss                     |
| **speed**       | integer| 速度 ,单位km/h                                      |
| **status**      | string| 状态说明                                             |
| **target_lat**  | double| 纬度，请求参数map_coord_type指定目标坐标系  |
| **target_lon**  | double | 经度，请求参数map_coord_type指定目标坐标系 |



### 9. 远程抓拍

```
POST /open/v1/snap
```

**参数**



| 字段                           | 类型     | 说明                                                                  |
| ----------------------------------- | --------------------- | ------------------------------------------------------------ |
| **appkey**          | string | 接口请求APPKEY                                                               |
| **channel**         | integer | 通道号                                                                      |
| **client_code**     | string | 客户端识别码                                                                 |
| **device_id**       | string | 设备ID，填写IMEI即可                                                         |
| **image_params**    | object | 图片抓拍参数           |
| **notify_callback** | string  | 抓拍结果回调地址                                                            |
| **type**            | integer  | 抓拍类型,0图片、1视频                                                      |
| **video_params**    | object | 视频抓拍参数                                |

**image_params**

| 字段                  | 类型         | 说明                                                    |
| ------------------------------ | ------------------------------------------------------------ | ------- |
| **count**    | integer   | 抓拍张数                                                      |
| **interval**  | integer  | 抓拍间隔,单位：秒                                             |
| **resolution** | integer | 图片分辨率： 1-240\*320（默认）, 2-320\*480 , 3-360\*640 , 4-480\*800 ,5-640\*960 , 6-720\*1280  |

**video_params**

| 字段                        | 类型   | 说明     |
| ------------------------------ | ------------- | ------- |
| **duration**    | integer| 时长,单位：秒  |
| **resolution**  | string| 分辨率          |



**返回结果**



| 字段                     | 类型   | 说明                                                             |
| -------------------------- | ------------------------------ | ----------------------------------------------- |
| **error**   | integer| 错误码,0-成功，非0表示抓拍失败                                          |
| **reason**  | string | 提示                                                                    |
| **result**  | object | 抓拍成功返回的具体内容          |

**result**

图片/视频抓拍返回的内容

| 字段                         | 类型    | 说明                                                        |
| -------------------------------- | ----------- | ------------------------------------------------------------ |
| **device_state**  | object | 设备状态     |
| **snap_event**    | object | 抓拍的事件                 |

**device_state**

设备状态,当抓拍失败的时候返回

| 字段                     | 类型           | 说明                                                           |
| ---------------------------------- | ------------------------------------------------------------ | --------------- |
| **direct**     | integer      | 方向                                                                 |
| **driving_status** | integer  | 当前车辆行驶状态 0：熄火 1：启动                                     |
| **gps_lat**     | double    | 当前GPS定位纬度，WGS84坐标系如果设备离线则表示设备最后一次GPS定位纬度  |
| **gps_lon**      | double   | 当前GPS定位经度，WGS84坐标系如果设备离线则表示设备最后一次GPS定位经度  |
| **gps_signal**   | integer   | GPS卫星颗数                                                           |
| **gps_time**      | string  | 当前GPS定位时间,格式yyyy-MM-dd HH:mm:ss如果设备离线则表示设备最后一次GPS定位时间           |
| **is_online**    | integer    | 当前设备在线状态 0：离线 1：在线                                     |
| **speed**      | integer       | 速度,单位km/h                                                       |

**snap_event**

抓拍的事件,当抓拍成功的时候返回

| 字段                    | 类型     | 说明                          |
| ---------------------------- | ---------------------------------- | ------- |
| **event_id**  | integer| 抓拍事件ID，标示唯一的一次抓拍动作  |



### 10. 根据时间区间获取设备历史抓拍的照片或视频列表

```
POST /open/v1/GetHistorySnapList
```

**参数**



| 字段                    | 类型       | 说明                                                                                |
| ------------------------------ | ----------------------------------- | ------------------------------------------------------------ |
| **channel**     | string | 摄像头通道号                                                                              |
| **device_id**   | string| 设备ID，填写IMEI即可                                                                       |
| **end_time**    | string| 结束时间，格式：yyyy-MM-dd HH:mm:ss                                                        |
| **page_info**   | object | 分页参数                             |
| **start_time**  | string | 开始时间，格式：yyyy-MM-dd HH:mm:ss                                                       |
| **user_id**     | integer| 用户ID                                                                                    |


**page_info**

分页信息

| 字段                         | 类型  | 说明                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |


**返回结果**

| 字段                 | 类型       | 说明                                                     |
| -------------------------- | ----------- | ---------------------------------------------------------- |
| **error**   | integer| 错误码                                                          |
| **reason**  | string| 提示                                                             |
| **result**  | object | 历史抓拍     |

**result**

| 字段                       | 类型    | 说明                                                            |
| ----------------------------- | ---------------- | ------------------------------------------------------------ |
| **list**       | array | 历史抓拍时间列表  |
| **page_info**  | object | 分页信息                        |

**list**

| 字段                   | 类型          | 说明                                                                                            |
| ------------------------------- | ------------------------------------------------ | ------------------------------------------------------------ |
| **channel**   | string   | 抓拍摄像头通道号                                                                                        |
| **create_time** | string | 创建时间(格式：yyyy-mm-dd HH:MM:ss)                                                                     |
| **event_id**   | integer  | 抓拍事件ID，标示唯一的一次抓拍动作                                                                     |
| **event_time**  | string | 抓拍完成时间(格式：yyyy-mm-dd HH:MM:ss)                                                                 |
| **event_type** | integer  | 事件类型，101-图片抓拍 102-振动报警 103-视频抓拍 10001-定时抓拍 10002-定距抓拍                                                       |
| **image_url**   | array | 图片抓拍结果链接,string数组格式                                                                 |
| **pos**        | object | 位置                                              |
| **shoot_time**  | string   | 抓拍时间(格式：yyyy-mm-dd HH:MM:ss)                                                                   |
| **source**     | string  | 抓拍请求来源                                                                                            |
| **thumb_url**   | string | 抓拍结果视频文件缩略图链接                                                                              |
| **vedio_url**   | string | 视频抓拍结果链接                                                                                        |

**pos**

| 字段               | 类型          | 说明                                          |
| ---------------------------- | ------------------------------------------ | --------------- |
| **direct**    | integer| GPS定位方向                                         |
| **gps_time**  | string| GPS定位定位时间，格式：yyyy-MM-dd HH:mm:ss           |
| **lat**       | double| GPS定位纬度，WGS84坐标系                    |
| **lng**       | double| GPS定位经度，WGS84坐标系                    |
| **speed**     | integer | GPS定位速度，单位km/h                              |

**page_info**

分页信息

| 字段      | 类型| 说明         |
| --------- | -------- | ------- |
| **total** | integer| 总记录数  |


### 11.根据ID获取设备历史抓拍的照片或视频详细信息

```
GET /open/v1/GetSnapByID
```

**参数**

| 字段                   | 类型       | 说明                      |
| ----------------------------- | ------------------------------ | ------- |
| **device_id**  | string | 设备ID，填写IMEI即可            |
| **event_id**   | integer| 抓拍ID，标示唯一的一次抓拍动作  |

**返回结果**



| 字段                    | 类型     | 说明                                                                           |
| -------------------------- | -------------------------------------- | ------------------------------------------------------ |
| **error**   | integer| 错误码                                                                                 |
| **reason**  | string| 提示                                                                                    |
| **result**  | object | 一笔设备历史抓拍的照片或视频详情的详情  |

**result**

| 字段            | 类型    | 说明                                             |
| --------------- | ------- | ------------------------------------------------ |
| **channel**     | string  | 抓拍摄像头通道号                                 |
| **create_time** | string  | 创建时间(格式：yyyy-mm-dd HH:MM:ss)              |
| **event_id**    | integer | 抓拍事件ID，标示唯一的一次抓拍动作               |
| **event_time**  | string  | 抓拍完成时间(格式：yyyy-mm-dd HH:MM:ss)          |
| **event_type**  | integer | 事件类型，101-图片抓拍 102-振动报警 103-视频抓拍 |
| **image_url**   | array   | 图片抓拍结果链接,string数组格式                  |
| **pos**         | object  | 位置                                             |
| **shoot_time**  | string  | 抓拍时间(格式：yyyy-mm-dd HH:MM:ss)              |
| **source**      | string  | 抓拍请求来源                                     |
| **thumb_url**   | string  | 抓拍结果视频文件缩略图链接                       |
| **vedio_url**   | string  | 视频抓拍结果链接                                 |

**pos**

| 字段         | 类型    | 说明                                       |
| ------------ | ------- | ------------------------------------------ |
| **direct**   | integer | GPS定位方向                                |
| **gps_time** | string  | GPS定位定位时间，格式：yyyy-MM-dd HH:mm:ss |
| **lat**      | double  | GPS定位纬度，WGS84坐标系                   |
| **lng**      | double  | GPS定位经度，WGS84坐标系                   |
| **speed**    | integer | GPS定位速度，单位km/h                      |



### 12. 根据经纬度获取所在行政区

```
POST /open/v1/GetLngLatArea
```

**参数**



| 字段             | 类型         | 说明                  |
| ----------------------- | -------------------- | --------------- |
| **lat**  | double| GPS纬度，WGS84坐标系  |
| **lng**  | double| GPS经度，WGS84坐标系  |



**返回结果**



| 字段                | 类型       | 说明                                           |
| -------------------------- | ----------- | ----------------------------------------------- |
| **error**   | integer | 错误码                                              |
| **reason**  | string| 提示                                                  |
| **result**  | object | 结果         |

**result**

| 字段                   | 类型      | 说明  |
| ---------------------------- | ----------- | ------ |
| **city**      | string| 城市名称     |
| **province**  | string| 省份名称     |
| **region**    | string| 县区名称     |

### 13. 查询Sim卡详细信息

```
POST /open/v1/GetSimDetail
```

**参数**



| 字段                     | 类型 | 说明  |
| ------------------------- | ----------- | ------ |
| **iccid**  | string| iccid卡号    |
| **imsi**   | string | imsi卡号    |
| **sim**    | string| sim卡号      |

**返回结果**

| 字段                 | 类型       | 说明                                             |
| -------------------------- | ----------- | -------------------------------------------------- |
| **error**  | integer | 错误码                                                  |
| **reason**  | string | 提示                                                    |
| **result**  | object | 卡信息      |

**result**

| 字段               | 类型                      | 说明                                                                                                        |
| --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **active_pg_name**     | string      | 套餐名称                                                                                                        |
| **active_pg_status**  | integer      | 赠送套餐实名状态，1激活送套餐 ，0不送套餐                                                                       |
| **active_pg_way**    | integer      | 赠送套餐方式 1个人 2手机                                                                                         |
| **amount_usage**     | double     | 周期流量,单位KB                                                                                           |
| **app_package_list** | array | 应用列表                                                     |
| **expire_date**     | string      | 到期时间,格式yyyy-mm-dd HH:mm:ss                                                                                   |
| **first_active**     | string      | 首次激活,格式yyyy-mm-dd HH:mm:ss                                                                                  |
| **flowleft_time**    | string      | 流量同步时间 最近流量同步时间，精确到秒                                                                           |
| **iccid**     | string           | SIM卡ICCID                                                                                                          |
| **imei**      | string             | 绑定设备的IMEI                                                                                                    |
| **imsi**        | string           | SIM卡IMSI                                                                                                         |
| **is_reset**   | integer           | 是否清零                                                                                                          |
| **last_active**  | string         | 最近激活,格式yyyy-mm-dd HH:mm:ss                                                                                   |
| **month_usage**   | double        | 当月用量,单位KB                                                                                           |
| **network_speed**  | string      | 网络速度:  高速 中速 低速                                                                                           |
| **norealname_renewals** | integer | 未实名是否运行续费，0不允许，1允许                                                                                 |
| **package**    | string           | 套餐名称                                                                                                           |
| **package_info**  | string        | 套餐信息                                                                                                           |
| **package_period** | integer       | 套餐周期，单位：天                                                                                                |
| **package_usage**  | double      | 套餐用量,单位KB                                                                                            |
| **packagesn**   | integer         | 套餐序号                                                                                                           |
| **packageupdate_time**| string    | 套餐更新时间,格式yyyy-mm-dd HH:mm:ss                                                                               |
| **period_months**   | integer      | 套餐周期(月)套餐周期，单位：月                                                                                    |
| **realname_status** | integer      | SIM卡实名状态,0-未实名,1-已实名,2-待审核                                                                          |
| **realname_term**  | string       | 实名认证的有效期限                                                                                                 |
| **sim**     | string              | SIM卡SIM卡号                                                                                                       |
| **status**    | integer            | 卡状态, 0-库存,1-可测试,2-可激活,3-已激活,4-已停用,5-已失效,6-已注销,7-已更换                                                      |
| **status_desc**   | string        | 卡状态说明                                                                                                         |
| **surplus_period**  | integer      | 剩余天数                                                                                                          |
| **surplus_usage**  | double       | 剩余流量,单位KB                                                                                           |
| **system_time**  | string         | 系统时间                                                                                                           |
| **total_surplus_usage** | double  | 总剩余流量,单位KB                                                                                         |
| **total_usage**    | double       | 历史用量,单位KB                                                                                           |

**app_package_list**

| 字段              | 类型                   | 说明                                       |
| ----------------------------------- | ---------------------------------------- | --------------- |
| **amountUsage**     | double  | 周期流量（KB）                           |
| **appName**         | string  | 应用组名称                                        |
| **expireTime**      | string  | 到期日期,格式yyyy-mm-dd HH:mm:ss                  |
| **flowLeftValue**   | double | 剩余用量（KB）                            |
| **living_realname** | integer  | 活体实名状态 实名方式，1人脸验证，0 普通         |
| **periodEndTime**   | string  | 周期结束,格式yyyy-mm-dd HH:mm:ss                  |
| **periodStartTime** | string | 周期开始,格式yyyy-mm-dd HH:mm:ss                   |
| **surplusPeriod**   | integer | 剩余天数                                          |



### 14. 批量查询Sim卡信息

```
POST /open/v1/GetSimDetails
```



| 字段                | 类型       | 说明           |
| ------------------------- | ----------- | ---------------- |
| **iccid**  | array | iccid卡号,string数组 |
| **imsi**   | array | imsi卡号,string数组 |
| **sim**    | array | sim卡号,string数组 |



**返回结果**



| 字段                  | 类型      | 说明                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                           |
| **reason**  | string | 提示                                                              |
| **result**  | array | 卡信息       |

**result**

| 字段                   | 类型              | 说明                                                           |
| ----------------------------------- | ------------------------------------------------------------ | --------------- |
| **amount_usage**   | double    | 周期流量（KB）                                              |
| **expire_date**    | string   | 到期时间,格式yyyy-mm-dd HH:mm:ss                                      |
| **first_active**  | string    | 首次激活,格式yyyy-mm-dd HH:mm:ss                                      |
| **iccid**      | string       | SIM卡ICCID                                                            |
| **imei**        | string       | 绑定设备的IMEI                                                       |
| **imsi**      | string        | SIM卡IMSI                                                             |
| **last_active**  | string     | 最近激活时间，格式yyyy-mm-dd HH:mm:ss                                 |
| **month_usage** | double     | 当月用量（KB）                                                |
| **package**     | string     | 套餐名称                                                               |
| **packagesn**   | integer      | 套餐序号                                                             |
| **realname_status** | integer  | 实名状态,0-未实名,1-已实名,2-待审核                                  |
| **sim**       | string        | SIM卡SIM卡号                                                          |
| **status**     | integer      | SIM卡状态, 0-库存,1-可测试,2-可激活,3-已激活,4-已停用,5-已失效,6-已注销,7-已更换          |
| **status_desc**    | string   | SIM卡状态说明                                                         |
| **surplus_period**  | integer   | 剩余天数                                                            |
| **surplus_usage**    | double  | 剩余流量（KB）                                              |
| **total_usage**  | double     | 历史用量（KB）                                               |



### 15. 获取设备参数设置列表

```
GET /open/v1/GetDeviceParamList
```

**参数**

| 字段                      | 类型    | 说明           |
| ----------------------------- | -------------------- | ------ |
| **device_id**  | string| 设备ID，填写IMEI即可  |

**返回结果**



| 字段              | 类型          | 说明                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**   | integer   | 错误码                                                         |
| **reason**  | string | 提示                                                              |
| **result**  | array | 设置列表     |

**result**

| 字段                 | 类型         | 说明                                                        |
| ---------------------------- | ------------ | ------------------------------------------------------------ |
| **setList**   | array | 参数设置列表  |
| **typeName**  | string | 设备类型名称                                                       |

**setList**

| 字段                       | 类型         | 说明                                                                      |
| ----------------------------------- | ------------------------- | ------------------------------------------------------------ |
| **cmdType**          | string| 指令类型                                                                         |
| **enable**           | string| 是否启用, 1启用 、0不启用                                                        |
| **interactionType**  | string | 交互类型                                                                        |
| **range**            | array | 选项列表                   |
| **setTitle**         | string| 标题                                                                             |
| **settingName**      | string| 参数名称                                                                         |
| **uiType**           | string| 界面类型                                                                         |
| **value**            | string| 参数值                                                                           |

**range**

| 字段                   | 类型   | 说明  |
| ------------------------- | ----------- | ------ |
| **Key**    | string| 选项关键字   |
| **Value**  | string| 选项值       |



### 16. 保存设备单个参数设置

```
GET /open/v1/SetDeviceParam
```

**参数**

| 字段             | 类型               | 说明                                    |
| ------------------------------- | --------------------------------------------- | ------ |
| **device_id**  | string  | 设备ID，填写IMEI即可                           |
| **param_type**  | string | 参数类型,【获取设备参数设置列表】中的参数名称  |
| **param_value** | string | 参数值，【获取设备参数设置列表】中的参数值     |

**返回结果**



| 字段                    | 类型   | 说明   |
| -------------------------- | ----------- | ------- |
| **error**   | integer| 错误码       |
| **reason**  | string| 提示          |



### 17. 透传发送设备单个参数设置

```
POST /open/v1/SendDeviceParamCmd
```

**参数**

| 字段                        | 类型        | 说明           |
| ----------------------------------- | -------------------- | ------ |
| **command_content**  | string| 透传命令内容          |
| **device_id**        | string| 设备ID，填写IMEI即可  |

**返回结果**



| 字段             | 类型           | 说明  |
| -------------------------- | ----------- | ------- |
| **error**   | integer| 错误码       |
| **reason**  | string| 提示          |



### 18. 获取设备历史视频列表

```
GET /open/v1/getvideolist
```

**参数**

| 字段                    | 类型         | 说明                           |
| -------------------------------- | ----------------------------------- | ------- |
| **begin_time**    | string | 查询开始时间 yyyy-mm-dd hh:MM:ss     |
| **channel**       | integer| 摄像头通道                           |
| **device_id**     | string | 设备ID，填写IMEI即可                 |
| **end_time**      | string| 查询结束时间 yyyy-mm-dd hh:MM:ss      |
| **format**        | string| 文件格式,例如：MP4 、AVI              |
| **storage_type**  | integer| 存储类型,1 本地，2云端，3本地和云端  |

**返回结果**

| 字段              | 类型          | 说明                                               |
| -------------------------- | ----------- | ---------------------------------------------------- |
| **error**  | integer | 错误码                                                    |
| **reason** | string  | 提示                                                      |
| **result** | object | 结果         |

**result**

| 字段                | 类型           | 说明                                                        |
| ------------------------------ | ----------- | ------------------------------------------------------------ |
| **video_list**  | array | 结果列表     |

**video_list**

| 字段               | 类型                  | 说明                                                |
| ------------------------------------ | -------------------------------------------------------- | ------- |
| **begin_time**    | string    | 视频开始时间(格式：yyyy-mm-dd HH:MM:ss)                    |
| **channel**      | integer     | 摄像头通道号                                              |
| **cloud_url**    | string     | 存储类型为1和2时，文件云端存储的url                        |
| **duration**   | integer       | 视频时长，单位：秒                                        |
| **end_time**   | string        | 视频结束时间(格式：yyyy-mm-dd HH:MM:ss)                   |
| **file_modify_time** | string | 文件最后修改时间(格式：yyyy-mm-dd HH:MM:ss)                |
| **file_size**  | integer       | 文件大小，单位：byte                                      |
| **format**    | string        | 文件格式后缀,例如：MP4 AVI                                 |
| **index_id**  | integer        | 文件索引id                                                |
| **local_file_name** | string  | 设备本地文件名称                                           |
| **local_file_path** | string  | 设备本地文件路径                                           |
| **storage_type**  | integer    | 存储类型：0-设备本地存储 1-云端存储 3-本地和云端同时存储  |





### 19. 获取云盘已购套餐信息

```
GET /open/v1/cloudStorage/userPackageInfo
```

**参数**

| 字段                     | 类型     | 说明           |
| ----------------------------- | -------------------- | ------ |
| **device_id** | string | 设备ID，填写IMEI即可  |

**返回结果**



| 字段                | 类型       | 说明                                                        |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**  | integer | 错误码                                                            |
| **reason** | string | 提示                                                               |
| **result** | array | 结果         |

**result**

| 字段           | 类型                               | 说明                                                                                    |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------------------------ |
| **buy_time**        | string         | 购买时间;                                                                                        |
| **cloud_recorder_package** | object | 记录仪套餐配置                              |
| **event_package**    | object       | 事件套餐配置                                |
| **live_package**   | object   | 直播套餐配置                                |
| **package_desc**    | string         | 套餐详细说明;                                                                                    |
| **package_id**    | integer           | 购买的套餐ID;                                                                                   |
| **package_subtitle**   | string     | 套餐子名称，可添加更详细的说明;                                                                   |
| **package_title**    | string       | 套餐名称;                                                                                         |
| **package_type**    | integer        | 套餐类型，0-普通 1-叠加包 2-扩充包;                                                              |
| **parking_snap_package** | object | 停车抓拍套餐配置                           |
| **save_live_package**    | object | 直播即存套餐配置                            |
| **snap_package**      | object | 抓拍套餐配置                                |
| **state**        | integer           | 套餐状态, 0-未激活，1-已激活, 2已失效;                                                           |
| **track_package**   | object  | 轨迹套餐配置                                |
| **travel_package**   | object | 行程套餐配置                                |
| **user_package_id**    | integer     | 套餐ID，关联op_user_package的记录的id字段;                                                       |

**cloud_recorder_package**

记录仪套餐配置

| 字段                      | 类型                 | 说明             |
| ------------------------------------------ | --------------------- | ------- |
| **active_time**       | string      | 激活时间;               |
| **effect_time**       | string      | 生效时间;               |
| **expired_time**       | string      | 套餐过期时间;          |
| **package_remaining_time** | integer  | 套餐剩余时间          |
| **period**                | integer  | 套餐有效期，单位：天;  |
| **total_mileage**         | integer  | 总里程;                |
| **total_play_duration**   | integer   | 云记录仪视频观看时长; |
| **used_mileage**          | integer  | 套餐内已使用里程;      |

**event_package、save_live_package、snap_package、track_package、travel_package**

公共套餐配置

| 字段               | 类型                        | 说明                                |
| ------------------------------------------ | ---------------------------------------- | ------- |
| **active_time**      | string       | 激活时间;                                  |
| **business_type**      | integer     | 套餐类型   1图片,2视频,3事件,4行程,5轨迹  |
| **effect_time**     | string        | 生效时间;                                  |
| **expired_time**   | string         | 套餐过期时间;                              |
| **package_remaining_time** | integer | 套餐剩余时间                              |
| **search_duration**     | integer    | 抓拍可观看时长;                           |

**live_package**

直播套餐配置

| 字段                         | 类型               | 说明            |
| ------------------------------------------ | --------------------- | ------- |
| **active_time**            | string | 激活时间;               |
| **effect_time**            | string  | 生效时间;              |
| **expired_time**           | string | 套餐过期时间;           |
| **live_duration**          | integer | 云记录仪视频观看时长;  |
| **live_interval**          | integer  | 直播时长(单位:秒)     |
| **live_limit_times**       | integer | 直播次数               |
| **package_remaining_time** | integer | 套餐剩余时间           |
| **pause_time**             | string  | 暂停时间               |



**parking_snap_package**

抓拍套餐配置

| 字段                     | 类型   | 说明             |
| -------------------------- | ------------- | ------- |
| **active_time**           | string | 激活时间;       |
| **effect_time**           | string | 生效时间;       |
| **expired_time**          | string  | 套餐过期时间;  |
| **package_remaining_time** | integer| 套餐剩余时间   |
| **search_duration**        | integer | 抓拍时长;     |

### 20. 查询云盘时间轴

```
POST /open/v1/cloudStorage/getTimeLine
```

**参数**

| 字段                   | 类型          | 说明                                                    |
| -------------------------------- | ------------------------------------------------------------ | ------- |
| **begin_time**  | integer  | 开始时间，unix时间戳                                          |
| **channel**      | integer | 摄像头通道号: -1表示获取所有通道号，大于－1表示获取指定通道号，注意如果请求入参channel为-1时，返回结果中channel也为-1  |
| **cur_date**    | string  | 指定播放日期,格式：yyyy-mm-dd                                  |
| **device_id**    | string | 设备ID，填写IMEI即可                                           |
| **duration**   | integer   | 视频持续时长总分钟数                                          |
| **end_time**    | integer  | 结束时间，unix时间戳                                          |
| **sliding_type** | integer | 滑动类型:0向左滑动，1向右滑动 (仅用于滑动查询时使用)          |



**返回结果**



| 字段                 | 类型       | 说明                                                 |
| -------------------------- | ----------- | ------------------------------------------------------ |
| **error**   | integer  | 错误码                                                    |
| **reason**  | string | 提示                                                        |
| **result**  | object | 结果         |

**result**

云盘时间轴结果

| 字段                  | 类型          | 说明                                                                            |
| ------------------------------ | -------------------------------- | ------------------------------------------------------------ |
| **begin_time** | integer | 前次查询结果开始时间，unix时间戳                                                       |
| **end_time**   | integer    | 前次查询结果结束时间，unix时间戳                                                    |
| **imei**       | string   | 设备imei                                                      |
| **time_lines** | array | 列表信息                          |

**time_lines**

| 字段                      | 类型     | 说明          |
| ----------------------------- | ------------------- | ------- |
| **channel**   | integer | 摄像头通道号;        |
| **end**       | integer | 结束时间,UNIX时间戳  |
| **start**     | integer  | 开始时间,UNIX时间戳 |
| **thumb_url** | string | 缩略图                |



### 21. 拉取云盘文件列表

```
POST /open/v1/cloudStorage/getIndex
```

**参数**

| 字段                       | 类型    | 说明            |
| ------------------------------ | -------------------- | ------- |
| **begin_time**  | integer| 开始时间，unix时间戳  |
| **channel**     | integer| 摄像头通道号          |
| **device_id**   | string| 设备ID，填写IMEI即可   |
| **end_time**    | integer| 结束时间，unix时间戳  |



**返回结果**

| 字段                  | 类型      | 说明                                              |
| -------------------------- | ----------- | --------------------------------------------------- |
| **error**  | integer | 错误码                                                   |
| **reason** | string  | 提示                                                     |
| **result** | object | 结果        |

**result**

| 字段               | 类型             | 说明                                                               |
| ----------------------------- | -------------------- | ------------------------------------------------------------ |
| **device_id** | string | 设备ID，填写IMEI即可                                                        |
| **indexes**   | array | 列表信息              |

**indexes**

| 字段                       | 类型         | 说明                        |
| ----------------------------------- | -------------------------------- | ------- |
| **channel**          | integer | 摄像头通道号                     |
| **end_time**         | integer| 结束时间，unix时间戳              |
| **file_size**        | integer| 文件大小,字节                     |
| **frame_cnt**        | integer| 视频文件总帧数                    |
| **id**               | integer| id                                |
| **meta_data_url**    | string| 结构化元数据oss文件路径            |
| **meta_end_time**    | integer| 视频帧结束时间戳（毫秒级时间戳)   |
| **meta_start_time**  | integer| 视频帧开始时间戳（毫秒级时间戳）  |
| **play_duration**    | integer| 播放时长,毫秒                     |
| **start_time**       | integer| 开始时间，unix时间戳              |
| **thumb_url**        | string| 缩略图                             |
| **url**              | string | 视频文件URL                       |



### 22. 查询云盘视频日历

```
POST /open/v1/cloudStorage/getCalendar
```

**参数**

| 字段                   | 类型        | 说明          |
| ----------------------------- | -------------------- | ------ |
| **device_id** | string | 设备ID，填写IMEI即可  |
| **month**     | string | 查询月份,格式yyyy-mm  |



**返回结果**

| 字段                | 类型        | 说明                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**  | integer | 错误码                                                            |
| **reason**  | string | 提示                                                              |
| **result**  | array | 列表信息     |

**result**

| 字段                       | 类型         | 说明              |
| ---------------------------------- | ----------------------- | ------- |
| **date**          | string   | 日期,格式yyyy-mm-dd      |
| **event_count**   | integer  | 事件个数                 |
| **is_enable**      | bool | 是否有效，0-无效 1-有效  |
| **video_duration**   | integer | 视频时长,分钟          |

### 23. 查询云盘事件标签列表

```
GET /open/v1/cloudStorage/getVideoLabel
```

**参数**

| 字段                  | 类型         | 说明                          |
| ------------------------------ | ----------------------------------- | ------ |
| **begin_time**  | string| 开始时间，格式：yyyy-MM-dd HH:mm:ss  |
| **device_id**   | string| 设备ID，填写IMEI即可                 |
| **end_time**    | string| 结束时间，格式：yyyy-MM-dd HH:mm:ss  |



**返回结果**



| 字段                  | 类型      | 说明                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**  | integer | 错误码                                                            |
| **reason** | string   | 提示                                                             |
| **result** | array | 结果        |

**result**

| 字段                | 类型                 | 说明                                                          |
| ---------------------------------- | ------------------------------------------------------------ | --------------- |
| **event_id**     | integer    | 事件id                                                               |
| **gps_time**    | string     | GPS时间,格式： YYYY-mm-dd hh:MM:ss                                    |
| **label_desc**    | string   | 标签说明                                                              |
| **label_sub_type** | integer | 标签子类型，0  急加速,1  急减速,2 急转弯,23 视频加锁,24 ADAS报警事件          |
| **label_type**   | integer    | 标签类型,1 云盘                                                      |
| **rcv_time**    | string    | 接收时间,格式： YYYY-mm-dd hh:MM:ss                                    |
| **start_lat**   | double    | 事件开始位置纬度，WGS84坐标系                                 |
| **start_lon**    | double   | 事件开始位置经度，WGS84坐标系                                 |
| **start_time**    | string  | 开始时间,格式： YYYY-mm-dd hh:MM:ss                                    |
| **stop_lat**    | double    | 事件结束位置纬度，WGS84坐标系                                 |
| **stop_lon**    | double    | 事件结束位置经度，WGS84坐标系                                 |
| **stop_time**   | string     | 停止时间,格式： YYYY-mm-dd hh:MM:ss                                   |



### 24. 添加视频录制任务

```
POST /open/v1/UploadVideoRecordingParams
```

**参数**

| 字段             | 类型               | 说明                                        |
| ------------------------------ | ------------------------------------------------- | ------- |
| **begin_time** | integer | 开始时间戳，UNIX时间戳                             |
| **channel**    | integer  | 录制任务摄像头通道号                              |
| **device_id**  | string | 设备ID，填写IMEI即可                                |
| **end_time**   | integer | 结束时间戳，UNIX时间戳                             |
| **query_time** | integer | 查询时间戳，UNIX时间戳                             |
| **state**     | integer  | 任务状态, 0-空，1-未处理，2-处理失败，3 处理成功;  |
| **task_type**  | integer | 录制类型:0视频，1图片                              |



**返回结果**

| 字段            | 类型           | 说明                                                        |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                           |
| **reason** | string  | 提示                                                              |
| **result**  | object | 结果         |

**result**

| 字段              | 类型      | 说明  |
| ----------------------- | ----------- | ------ |
| **seq**  | string| 查询流水号   |



### 25. 查询视频录制任务

```
POST /open/v1/GetVideoRecordingResult
```

**参数**

| 字段               | 类型     | 说明  |
| ----------------------- | ----------- | ------ |
| **seq**  | string| 查询流水号   |



**返回结果**

| 字段               | 类型          | 说明                                                      |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**   | integer| 错误码                                                            |
| **reason**  | string| 提示                                                               |
| **result**  | result | 结果信息     |

**result**

| 字段               | 类型            | 说明                                                 |
| ------------------------------ | ------------------------------------------------ | ---------------- |
| **begin_time** | integer | 开始时间，UNIX时间戳         |
| **channel**   | integer  | 录制文件的摄像头通道号     |
| **device_id**  | string   | 设备ID，填写IMEI即可     |
| **end_time**  | integer  | 结束时间，UNIX时间戳    |
| **image_url** | array | 截屏图片路径string数组   |
| **state**      | integer          | 任务状态, 0-空，1-未处理，2-处理失败，3 处理成功  |
| **task_type**  | integer | 录制类型:0视频，1图片            |
| **video_url**  | string  | 视频文件URL        |



### 26. 设备固件升级指令

```
POST /open/v1/DeviceFirmwareUpgrage
```

**参数**

| 字段                | 类型      | 说明 |
| ------------------------ | ----------- | ------ |
| **imei**  | string| 设备的IMEI   |

**返回结果**

| 字段           | 类型            | 说明   |
| -------------------------- | ----------- | ------- |
| **error**   | integer| 错误码       |
| **reason**  | string | 提示         |






### 27.语音播报

```
POST /open/v1/TextToSpeech
```

**参数**



| 字段                  | 类型         | 说明          |
| ----------------------------- | -------------------- | ------ |
| **content**   | string | 语音播报的内容        |
| **device_id** | string | 设备ID，填写IMEI即可  |



**返回结果**



| 字段                 | 类型        | 说明 |
| -------------------------- | ----------- | ------- |
| **error**   | integer| 错误码       |
| **reason**  | string| 提示          |



### 28.按日查询设备的行驶里程

```
POST /open/v1/GetDeviceMileage
```

**说明**

1、查询范围是最近三个月内
2、查询结果按天为单位逐条展示
3、当天如果无数据不返回当天内容

**参数**

| 字段                | 类型            | 说明                       |
| ------------------------------ | --------------------------------- | ------ |
| **device_id**   | string| 设备ID，填写IMEI即可               |
| **end_date**    | string| 结束日期，精确到天,格式yyyy-MM-dd  |
| **start_date**  | string| 开始日期，精确到天,格式yyyy-MM-dd  |



**返回结果**



| 字段             | 类型           | 说明                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**  | integer  | 错误码                                                           |
| **reason** | string | 提示                                                               |
| **result** | array | 结果        |

**result**

| 字段                 | 类型            | 说明                        |
| ------------------------------ | -------------------------- | --------------- |
| **mileage**     | double| 设备里程，单位KM            |
| **travel_day**  | string     | 行驶日期，格式：yyyy-MM-dd      |



### 29.查询设备异常列表

```
GET /open/v1/GetDeviceWarnings
```

**参数**

| 字段                       | 类型   | 说明           |
| ----------------------------- | -------------------- | ------ |
| **device_id**  | string| 设备ID，填写IMEI即可  |

**返回结果**



| 字段                  | 类型      | 说明                                                   |
| -------------------------- | ----------- | -------------------------------------------------------- |
| **error**   | integer| 错误码                                                        |
| **reason**  | string | 提示                                                          |
| **result**  | object | 结果        |

**result**

| 字段                            | 类型                                                       |
| ------------------------------- | ------------------------------------------------------------ |
| **warningList**  | array |

**warningList**

| 字段                | 类型       | 说明                                    |
| -------------------------- | -------------------------------------------- | ------- |
| **code**   | integer | 异常编码：0x000a-SD卡异常，0x000b-摄像头异常  |
| **reason** | string | 异常原因                                       |



### 30.设置电子围栏

```
POST /open/v1/SetFence
```

**参数**


| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **device_id** | string | 设备ID，填写IMEI即可 |
| **fence_name** | string | 围栏名称 |
| **fence_type** | integer | 围栏类型（0-圆形，1-多边形，7-道路养护路线） |
| **flag** | integer | 触发围栏告警类型（0-进围栏 、 1-出围栏 、 2-进出围栏、 3-取消） |
| **circle** | object | 圆形围栏信息（围栏类型字段fence_type=0时，此字段有效） |
| **polygon_coord_list** | array | 多边形围栏的坐标点列表（围栏类型字段fence_type=1时，此字段有效） |
| **line_coord_list** | array | 道路养护路线围栏的坐标点列表（围栏类型字段fence_type=7时，此字段有效） |
| **remark** | string | 备注 |

**circle**

圆形围栏信息（围栏类型字段fence_type=0时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat**     | double| 纬度,WGS84坐标系              |
| **lon**     | double| 经度,WGS84坐标系              |
| **radius**  | integer| 圆形围栏的半径值（单位：米）          |

**polygon_coord_list**

多边形围栏的坐标点列表（围栏类型字段fence_type=1时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat**  | double| 纬度,WGS84坐标系  |
| **lon**  | double| 经度,WGS84坐标系  |

**line_coord_list**

道路养护路线围栏的坐标点列表（围栏类型字段fence_type=7时，此字段有效）

| 字段    | 类型   | 说明             |
| ------- | ------ | ---------------- |
| **lat** | double | 纬度,WGS84坐标系 |
| **lon** | double | 经度,WGS84坐标系 |


**返回结果**


| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **error**   | integer    | 错误码 |
| **reason** | string     | 提示 |
| **result**   | object | 结果 |

**result**

设置围栏结果

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **fence_id**  | integer| 围栏ID       |



### 31.删除电子围栏

```
POST /open/v1/DelFence
```

**参数**

| 字段                       | 类型    | 说明           |
| ----------------------------- | -------------------- | ------- |
| **device_id** | string | 设备ID，填写IMEI即可   |
| **fence_id**  | integer | 围栏ID                |

**返回结果**

| 字段                | 类型        | 说明  |
| -------------------------- | ----------- | ------- |
| **error**  | integer | 错误码       |
| **reason** | string  | 提示         |



### 32.修改电子围栏

```
POST /open/v1/UpdateFence
```

**参数**



| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **fence_id** | integer | 围栏ID |
| **device_id** | string | 设备ID，填写IMEI即可 |
| **fence_name** | string | 围栏名称 |
| **fence_type** | integer | 围栏类型（0-圆形，1-多边形，7-道路养护路线） |
| **flag** | integer | 触发围栏告警类型（0-进围栏 、 1-出围栏 、 2-进出围栏、 3-取消） |
| **circle** | object | 圆形围栏信息（围栏类型字段fence_type=0时，此字段有效） |
| **polygon_coord_list** | array | 多边形围栏的坐标点列表（围栏类型字段fence_type=1时，此字段有效） |
| **line_coord_list** | array | 道路养护路线围栏的坐标点列表（围栏类型字段fence_type=7时，此字段有效） |
| **remark** | string | 备注 |

**circle**

圆形围栏信息（围栏类型字段fence_type=0时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat**    | double  | 纬度,WGS84坐标系             |
| **lon**    | double  | 经度,WGS84坐标系             |
| **radius** | integer | 圆形围栏的半径值（单位：米） |

**polygon_coord_list**

多边形围栏的坐标点列表（围栏类型字段fence_type=1时，此字段有效）

| 字段    | 类型   | 说明             |
| ------- | ------ | ---------------- |
| **lat** | double | 纬度,WGS84坐标系 |
| **lon** | double | 经度,WGS84坐标系 |

**line_coord_list**

道路养护路线围栏的坐标点列表（围栏类型字段fence_type=7时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat** | double | 纬度,WGS84坐标系 |
| **lon** | double | 经度,WGS84坐标系 |


**返回结果**

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **error**  | integer  | 错误码      |
| **reason**  | string  | 提示        |



### 33.查询电子围栏

```
POST /open/v1/GetFence
```

**参数**



| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **device_id** | string  | 设备ID，填写IMEI即可 |
| **fence_id**  | integer | 围栏ID可选参数1、若不传递，则查询此设备所绑定的所有围栏信息2、若传递，则查询此围栏ID的信息（若该设备没有绑定此围栏则没有信息返回） |



**返回结果**

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **error** | integer     | 错误码 |
| **reason**  | string  | 提示 |
| **result** | array | 结果 |

**result**

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **fence_id** | integer | 围栏ID |
| **device_id** | string | 设备ID，填写IMEI即可 |
| **fence_name** | string | 围栏名称 |
| **fence_type** | integer | 围栏类型（0-圆形，1-多边形，7-道路养护路线） |
| **flag** | integer | 触发围栏告警类型（0-进围栏 、 1-出围栏 、 2-进出围栏、 3-取消） |
| **circle** | object | 圆形围栏信息（围栏类型字段fence_type=0时，此字段有效） |
| **polygon_coord_list** | array | 多边形围栏的坐标点列表（围栏类型字段fence_type=1时，此字段有效） |
| **line_coord_list** | array | 道路养护路线围栏的坐标点列表（围栏类型字段fence_type=7时，此字段有效） |
| **remark** | string | 备注 |
| **create_date** | string | 创建时间（格式：yyyy-MM-dd HH:mm:ss） |
| **update_date** | string | 更新时间（格式：yyyy-MM-dd HH:mm:ss） |

**circle**

圆形围栏信息（围栏类型字段fence_type=0时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat**    | double  | 纬度,WGS84坐标系 |
| **lon**    | double  | 经度,WGS84坐标系 |
| **radius** | integer | 圆形围栏的半径值（单位：米） |

**polygon_coord_list**

多边形围栏的坐标点列表（围栏类型字段fence_type=1时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat** | double | 纬度,WGS84坐标系 |
| **lon** | double | 经度,WGS84坐标系 |

**line_coord_list**

道路养护路线围栏的坐标点列表（围栏类型字段fence_type=7时，此字段有效）

| 字段 | 类型 | 说明 |
| ----------- | ----------- | ----------- |
| **lat** | double | 纬度,WGS84坐标系 |
| **lon** | double | 经度,WGS84坐标系 |

### 34.查询ETC扣费信息列表

```
POST /open/v1/GetEtcCharging
```

**参数**



| 字段                   | 类型           | 说明                                                                             |
| ------------------------------ | ----------------------------------- | ------------------------------------------------------------ |
| **device_id**  | string    | 设备ID，填写IMEI即可                                                                    |
| **end_time**   | string  | 结束时间，格式：yyyy-MM-dd HH:mm:ss                                                       |
| **page_info**  | object | 分页参数                             |
| **start_time** | string   | 开始时间，格式：yyyy-MM-dd HH:mm:ss                                                      |

**page_info**

分页信息

| 字段                         | 类型  | 说明                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |




**返回结果**



| 字段           | 类型              | 说明                                                |
| -------------------------- | ----------- | ------------------------------------------------------ |
| **error**   | integer| 错误码                                                      |
| **reason** | string   | 提示                                                       |
| **result**  | object | ETC扣费      |

**result**

| 字段               | 类型            | 说明                                                       |
| ----------------------------- | ----------- | ------------------------------------------------------------ |
| **list**     | array | ETC扣费列表  |
| **page_info** | object | 分页信息                    |

**list**

| 字段                 | 类型                  | 说明                                           |
| ------------------------------------ | ----------------------------------------------------- | ------- |
| **deduction_amount**  | integer | ETC扣费金额,单位：分                                  |
| **deduction_time**  | string  | 扣费时间,格式yyyy-MM-dd HH:mm:ss                        |
| **e_ecn**     | string        | 入/出口收费路网号                                       |
| **e_ets**    | string         | 入/出口收费站号                                         |
| **etcat**     | integer        | 交易天线类型:0xa1:入口,0xa2:出口                       |
| **lane_number**   | string     | 车道号                                                 |
| **lpn**        | string       | 车牌号码                                                |
| **net_time**     | string     | 实时网络时间,格式yyyy-MM-dd HH:mm:ss                    |
| **status_flag**   | integer    | 交易状态标志,0x00：OK,0x01：ERR                        |
| **transaction_type** | integer | 交易类型:0x81-收费公路封闭式交易、0x90-其它封闭式应用  |
| **vin**     | string          | VIN                                                     |
| **weight**   | integer         | 货车总重，单位kg                                       |

**page_info**

分页信息

| 字段      | 类型| 说明         |
| --------- | -------- | ------- |
| **total** | integer| 总记录数  |


### 35.查询ETC门架信息列表

```
POST /open/v1/GetEtcGantry
```

**参数**



| 字段                       | 类型       | 说明                                                                             |
| ------------------------------ | ----------------------------------- | ------------------------------------------------------------ |
| **device_id**   | string | 设备ID，填写IMEI即可                                                                      |
| **end_time**    | string| 结束时间，格式：yyyy-MM-dd HH:mm:ss                                                        |
| **page_info**   | object | 分页参数                             |
| **start_time**  | string | 开始时间，格式：yyyy-MM-dd HH:mm:ss                                                       |

**page_info**

分页信息

| 字段                         | 类型  | 说明                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |



**返回结果**



| 字段           | 类型               | 说明                                              |
| -------------------------- | ------------ | ---------------------------------------------------- |
| **error**   | integer   | 错误码                                                  |
| **reason**  | string  | 提示                                                      |
| **result** | object | 门架信息结果  |

**result**

门架信息结果

| 字段             | 类型              | 说明                                                        |
| ----------------------------- | ------------ | ------------------------------------------------------------ |
| **list**     | array | 门架信息列表  |
| **page_info** | object | 分页信息                     |

**list**

| 字段                   | 类型                 | 说明                                       |
| ------------------------------------- | ------------------------------------------------- | ------- |
| **actual_amount**    | integer   | 累计实收金额,单位：分                             |
| **billing_mileage**  | integer  | 累计计费里程,单位米                                |
| **card_balance**     | integer   | 卡片余额,单位：分                                 |
| **card_type**      | integer    | 卡片类型,0x17:记账卡,0x16:储值卡                   |
| **etcat**        | integer      | 交易天线类型，0xa3:封闭式门架天线                  |
| **gantry_number**  | string     | 门架编号                                           |
| **lpn**    | string            | 车牌号码                                            |
| **obu_status**    | integer     | OBU状态,0x00:OK,Bit0:电量不足为1,Bit1:卡不存在为1  |
| **pass_time**    | string      | 通过时间                                            |
| **receivable_amount**  | integer| 累计应收金额,单位：分                              |
| **status_flag**     | integer   | 交易状态标志,0x00：OK,0x01：ERR                    |
| **transaction_type**  | integer | 交易类型,0x80：收费公路自由流                      |


**page_info**

分页信息

| 字段      | 类型| 说明         |
| --------- | -------- | ------- |
| **total** | integer| 总记录数  |


### 36.获取ETC-OBU信息

```
POST /open/v1/EtcObu
```

**参数**

| 字段              | 类型            | 说明           |
| ----------------------------- | -------------------- | ------ |
| **device_id**   | string| 设备ID，填写IMEI即可 |



**返回结果**



| 字段               | 类型          | 说明                                         |
| -------------------------- | ------------- | --------------------------------------------- |
| **error**  | integer  | 错误码                                              |
| **reason** | string  | 提示                                                 |
| **result** | object | 获取Obu的结果  |

**result**

| 字段                       | 类型  |
| -------------------------- | ------- |
| **obu_id**  | integer |



### 37.查询ETC-OBU应答信息

```
POST /open/v1/GetEtcObu
```

**参数**

| 字段                  | 类型        | 说明            |
| ----------------------------- | -------------------- | ------- |
| **device_id**  | string| 设备ID，填写IMEI即可   |
| **obu_id**     | integer| obu id                |



**返回结果**

| 字段            | 类型            | 说明                                               |
| -------------------------- | ----------- | ---------------------------------------------------- |
| **error**   | integer | 错误码                                                   |
| **reason**  | string| 提示                                                       |
| **result**  | object | OBU应答结果  |

**result**

| 字段               | 类型               | 说明                |
| -------------------------------- | ------------------------- | ------- |
| **contract_num**  | string | 合同号                     |
| **electricity**   | integer| 电量,单位:mv               |
| **obu_id**         | integer | 查询返回的obu id         |
| **obu_mac**       | string  | ObuMac                    |
| **obu_sn**        | string| ObuSn                       |
| **query_status**  | integer| 查询状态,1:成功 其他:失败  |
| **seq**           | string| 应答流水                    |
| **version**       | string | 版本号                     |


### 38.绑定车辆信息

```
POST /open/v1/BindVehicleDevice
```

**参数**

| 字段                  | 类型        | 说明            |
| ----------------------------- | -------------------- | ------- |
| **device_id**  | string | 设备ID，填写IMEI即可   |
| **drive_name** | string | 车主姓名               |
| **drive_phone** | string | 车主手机号           |
| **vehicle_name** | string | 车牌号             |
| **shelf_code** | string | 车架号             |
| **vehicle_bind_date** | string | 绑定时间       |
| **is_update** | bool | 当设备绑定过车辆信息，是否更新 (默认：false) |
| **emergency_contact_phone_1** | string | 紧急联系人电话1       |
| **emergency_contact_phone_2** | string | 紧急联系人电话2       |
| **emergency_contact_phone_3** | string | 紧急联系人电话3       |
| **store_bind** | integer | 是否与店端绑定，0-不需要显示与店端绑定,1-与店端绑定，2-不与店端绑定       |

**返回结果**



| 字段               | 类型          | 说明                                         |
| -------------------------- | ------------- | --------------------------------------------- |
| **error**  | integer  | 错误码      |
| **reason** | string  | 提示   |
| **result** | string |  空 |


### 39.获取账号设备ID列表

```
GET /open/v1/GetAccountDeviceList
```

**参数**

| 字段            | 类型        | 说明            |
|---------------| -------------------- | ------- |
| **appkey**    | string | 接口请求APPKEY   |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |

**返回结果**

| 字段               | 类型          | 说明     |
| -------------------------- | ------------- |--------|
| **error**  | integer  | 错误码    |
| **reason** | string  | 提示     |
| **result** | object | 账号设备 |

**result**

| 字段            | 类型          | 说明                |
|---------------| ------------- |-------------------|
| **list**      | array | 账号设备ID列表，string数组 |
| **page_info** | object | 分页信息              |

**page_info**

分页信息

| 字段            | 类型  | 说明                      |
|---------------| -------------------------------- | ------ |
| **total**     | integer| 总记录数|


### 40.获取道路病害列表

```
POST /open/v1/GetRoadDamageList
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段              | 类型      | 说明                                                 |
|-----------------|---------|----------------------------------------------------|
| **begin_time**  | string  | 查询开始时间，格式：yyyy-MM-dd HH:mm:ss                      |
| **end_time**    | string  | 查询结束时间，格式：yyyy-MM-dd HH:mm:ss                      |
| **device_id** | string  | 设备ID，填写IMEI即可                                      |
| **damage_type** | array   | 道路病害,integer数组格式（如果未传入任何参数，则默认查询所有道路病害）                     |
| **map_coord_type** | integer | 地图坐标系：0-WGS84(默认),1-BD09(百度地图), 2-GCJ02(高德地图、腾讯地图） |
| **page_info**   | object  | 分页参数                                               |

**道路病害枚举**

| code | 说明   |
|------|------|
|400 | 沥青路_坑槽 |
|411 | 沥青路_龟裂 |
|415 | 裂缝修补 |
|422 | 沥青路_横向裂缝 |
|423 | 沥青路_纵向裂缝 |
|424 | 水泥路_破碎板 |
|425 | 山体滑坡 |
|426 | 抛洒物 |
|427 | 抓拍病害 |
|428 | 沥青路_块状裂缝 |
|429 | 积水 |
|430 | 井盖高差 |
|431 | 水泥路_板角断裂 |
|432 | 拥包 |
|433 | 水泥路_线裂 |
|434 | 水泥路_坑洞 |
|435 | 补丁 |
|436 | 路肩损坏 |
|437 | 沥青路面_松散 |
|438 | 绿化管护不善 |
| 439 | 车行道障碍物 |
| 440 | 塌陷 |
| 441 | 占道施工 |
| 442 | 路树倾倒 |
| 443 | 标志牌_绿化遮挡 |
| 444 | 车行道_车止石_反光条缺损 |
| 445 | 车行道_分隔柱损坏 |
| 446 | 车行道_分隔柱_反光膜缺损 |
| 447 | 防撞桶_损坏 |
| 448 | 防撞桶_反光膜缺损 |
| 449 | 市政护栏_缺损 |
| 450 | 车行道_车止石_损坏 |
| 451 | 乔木刷新 |
| 452 | 分割柱老化 |

**page_info**

分页信息

| 字段                         | 类型  | 说明                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |

**返回结果**

| 字段               | 类型      | 说明     |
| -------------------------- |---------|--------|
| **error**  | integer | 错误码    |
| **reason** | string  | 提示     |
| **result** | object  | 道路病害 |

**result**

| 字段            | 类型          | 说明     |
|---------------| ------------- |--------|
| **list**      | array | 账号设备列表 |
| **page_info** | object | 分页信息   |

**list**

| 字段                   | 类型     | 说明                           |
|----------------------|--------|------------------------------|
| **device_id**        | string | 设备ID                         |
| **province**         | string | 省份名称                         |
| **city**             | string | 城市名称                         |
| **region**           | string | 县区名称                         |
| **recognition_time** | string | 识别时间，格式：yyyy-MM-dd HH:mm:ss  |
| **image_url**        | array  | 图片连接                         |
| **damage_type**      | string | 道路病害                         |
| **gps_lat**          | double | 纬度,WGS84坐标系                  |
| **gps_lon**          | double | 经度,WGS84坐标系                  |
| **target_lat**       | double | 纬度，请求参数map_coord_type指定目标坐标系 |
| **target_lon**       | double | 经度，请求参数map_coord_type指定目标坐标系 |
| **image_coordinate**       | array  | 图片坐标列表                       |

**list.image_coordinate**

| 字段                   | 类型     | 说明     |
|----------------------|--------|--------|
| **x**        | integer | 图片坐标x轴 |
| **y**         | integer | 图片坐标y轴 |

**page_info**

分页信息

| 字段            | 类型  | 说明                    |
|---------------|--------------------------------|------|
| **total**     | integer| 总记录数|


### 41.唤醒设备

```
GET /open/v1/WakeUpDevice
```

**参数**

|  字段  |  类型  |  说明  |
| ------------ | ------------ | ------------ |
| appkey  |  string  | 接口请求APPKEY  |
| device_id  | string  |  设备ID，填写IMEI即可  |

**返回结果**

| 字段                     | 类型    | 说明  |
| ------------ | ------------ | ------------  |
| **error**   | integer | 错误码 |
| **reason**  | string | 提示 |


### 42.获取相册列表

```
POST /open/v1/GetAlbumList
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

|  字段  |  类型  |  说明 |
| ------------ | ------------ | ---------- |
| **device_id**  |  string  | 设备ID，填写IMEI即可 |
| **search_type**  | string  |  搜索类型 不传默认值为-1 0-全部 1-抓拍图片 2-抓拍视频 3-直播云存 4-行车预警 5-震动报警 6-熄火抓拍 7-sos 8-云盘文件 |
| **channel**  | string  | 摄像头通道号 |
| **time_type**  | string  |  时间类型 不传默认为year day当天，week一周，month一个月，year一年 |
| **event_id**   | string | 事件ID |
| **event_type**   | string | 事件类型 |
| **page_info**   | object | 分页参数 |

**page_info**

分页信息

| 字段 | 类型  | 说明        |
|------------|------------|-----------|
| **page_num** | integer | 分页页码,从1开始 |
| **page_size** | integer| 分页大小      |

**返回结果**

| 字段                     | 类型    | 说明 |
| ------------ | ------------ | ------------ |
| **error**   | integer | 错误码 |
| **reason**  | string | 提示 |
| **result**  | array | 相册信息 |

**result**

| 字段            | 类型          | 说明     |
| --------------- | ------------- |--------|
| **list**      | array | 相册列表 |
| **page_info** | object | 分页信息   |

**list**

| 字段 | 类型     | 说明               |
|---------|--------|------------------|
| **album_id** | string | 相册ID             |
| **thumb_url** | string | 缩略图url           |
| **url** | string | 文件url            |
| **event_time** | string | 事件时间             |
| **channel** | integer | 摄像头通道号              |
| **channel_name** | string | 摄像头名称           |
| **event_id** | string | 事件id             |
| **event_type** | integer | 事件类型             |
| **event_name** | string | 事件名称             |
| **file_type** | integer | 文件类型 0-图片 1-视频   |
| **gps_lat** | double | GPS定位纬度,WGS84坐标系 |
| **gps_lng** | double | GPS定位经度,WGS84坐标系 |
| **image_list** | array | 图片列表             |
| **video_list** | array | 视频列表             |
| **city** | string | 城市               |
| **create_time** | string | 创建时间             |
| **update_time** | string | 更新时间             |

**list.image_list && list.video_list**

| 字段 | 类型 | 说明 |
|---------|---------|--------|
| **url** | string| 文件url |
| **thumb_url** | string| 缩略图url |
| **timestamp** | string| 时间戳 |
| **channel** | string| 摄像头通道号 |
| **channel_name** | string| 摄像头名称 |

**page_info**

| 字段 | 类型      | 说明 |
|------------|---------|------------|
| **total** | integer | 总记录数|



### 43.删除相册文件

```
POST /open/v1/DelAlbumFile
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

|  字段  |  类型  | 说明                |
| ------------ | ------------ |-------------------|
| **device_id**  | string  | 设备ID，填写IMEI即可     |
| **album_id**  | array  | 相册id，integer数组格式  |

**返回结果**

| 字段                     | 类型    | 说明  |
| ------------ | ------------ |-----|
| **error**   | integer | 错误码 |
| **reason**  | string | 提示  |
| **result**  | string | 结果  |


### 44.通过经纬度坐标解析地址

```
GET /open/v1/GetOverseasAddress
```

**Header**

| 字段 | 类型     | 说明             |
|-----|--------|----------------|
| **language**  | string | zh-cn 中文，en 英文 |

**参数**

| 字段         |  类型  | 说明                |
|------------|------------|------------|
| **appkey**  | string | 接口请求APPKEY   |
| **lat**    | double  | 纬度  |
| **lng**    | double  | 经度  |

**返回结果**

| 字段                     | 类型    | 说明  |
| ------------ | ------------ |-----|
| **error**   | integer | 错误码 |
| **reason**  | string | 提示  |
| **result**  | string | 结果  |


### 45.获取设备停留明细

```
POST /open/v1/GetDeviceStopDetail
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **device_id** | string| 设备ID，填写IMEI即可|
| **start_time** | string | 开始时间，格式：yyyy-MM-dd HH:mm:ss|
| **end_time**   | string | 结束时间，格式：yyyy-MM-dd HH:mm:ss|
| **map_coord_type** | integer | 地图坐标系：0-WGS84(默认),1-BD09(百度地图), 2-GCJ02(高德地图、腾讯地图）|
| **page_info**   | object | 分页参数|

**page_info**

分页信息

| 字段                         | 类型  | 说明                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | 分页页码,从1开始                 |
| **page_size**  | integer| 分页大小                          |

**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                                               |
| **result**  | array | 设备停留明细信息  |

**result**

| 字段            | 类型          | 说明     |
|---------------| ------------- |--------|
| **list**      | array | 设备停留明细列表 |
| **page_info** | object | 分页信息   |

**list**

| 字段                   | 类型      | 说明     |
|----------------------|---------|--------|
| **device_id**   | string  | 设备ID，填写IMEI即可 |
| **device_name**| string  | 设备名称 |
| **start_time**| string  | 停留开始时间,格式：yyyy-MM-dd HH:mm:ss |
| **end_time**| string  | 停留结束时间,格式：yyyy-MM-dd HH:mm:ss |
| **gps_lat**| double  | GPS定位纬度,WGS84坐标系 |
| **gps_lon**| double  | GPS定位经度,WGS84坐标系 |
| **target_lat**  | double| 纬度，请求参数map_coord_type指定目标坐标系  |
| **target_lon**  | double | 经度，请求参数map_coord_type指定目标坐标系 |
| **duration**| integer  | 停留时长单位为分钟 |
| **address**| string  | 停留位置 |

**page_info**

| 字段            | 类型  | 说明                      |
|---------------| -------------------------------- | ------ |
| **total**     | integer| 总记录数|



### 46.设置设备的事件视频上报方式

```
GET /open/v1/SetDeviceEventUploadType
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **device_id** | string| 设备ID，填写IMEI即可|
| **type** | string | 上报类型：0-关闭上报 1-上报图片 2-上报视频 3-上报图片和视频 |

**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                                               |
| **result**  | string | 结果  |




### 47.更新设备信息

```
POST /open/v1/UpdateDeviceInfo
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **device_id** | string| 设备ID，填写IMEI即可|
| **device_info** | string | 设备信息 |

**device_info**

| 字段                   | 类型      | 说明     |
|----------------------|---------|--------|
| **device_name**| string  | 设备名称 |

**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                                               |
| **result**  | string | 结果  |


### 48.断油断电设置

```
POST /open/v1/CutFuelPower
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **device_id** | string| 设备ID，填写IMEI即可|
| **switch** | integer | 0：恢复油电, 1：断油电 |



**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                                               |


### 49.查看是否领取过套餐

```
POST /open/v1/ClaimPackage
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **device_id** | string| 设备ID，填写IMEI即可|




**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                             |
| **result**  | object | 提示                                                               |

**result**

| 字段                   | 类型      | 说明     |
|----------------------|---------|--------|
| **is_activated** | bool  | 是否已激活，true-已激活，false-未激活 |


### 50.设备SD卡格式化

```
POST /open/v1/FormatSDCard
```

**Header**

| 字段 | 类型     | 说明 |
|-----|--------| ---- |
| **appkey**  | string | 接口请求APPKEY   |

**参数**

| 字段      | 类型 | 说明                   |
| --------- | ------| --------------------  |
| **device_id** | string | 设备ID，填写IMEI即可|


**返回结果**

| 字段                     | 类型    | 说明                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | 错误码                                                            |
| **reason**  | string | 提示                                             |


### 51.设置设备录像是否开启声音

```
POST /open/v1/SetDeviceRecordSound
```

**Header**

| 字段 | 类型 | 说明 |
| ----- | ----- | ----- |
| **appkey** | string | 接口请求APPKEY |

**参数**

| 字段 | 类型 | 说明 |
| --------- | ------| --------------------  |
| **device_id** | string | 设备ID，填写IMEI即可 |
| **record_switch** | integer | 录音开关，0-关闭，1-开启 |

**返回结果**

| 字段                     | 类型    | 说明 |
| ------------ | ------------ | ------------ |
| **error**   | integer | 错误码 |
| **reason**  | string | 提示 |