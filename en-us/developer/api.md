---

## API Usage Instructions

1. All APIs listed in this document support HTTP calls.
2. The domain for API calls is: `open.4s12580.com`.
3. API calls require authentication. Please add the request parameter `appkey` to the API call URL (case-sensitive, please use lowercase). You can obtain your `appkey` on the application information page after logging into the console.
4. For the specific request syntax of each API, including URI, Header, query parameters (including appkey), Post parameters, and return parameters, please refer to the detailed description of each API.
5. All API URLs, parameters, and returned fields involved in this document must strictly match the defined case and data types.

> Last updated: 2025/08/07 by Honsen

---

### 1. Get Device Basic Information

```
GET /open/v1/getdevicebaseinfo
```

**Parameters**

| Field      | Type | Description                   |
| --------- | ------| --------------------  |
| **appkey**    | string| API request APPKEY        |
| **device_id** | string| Device ID, fill in IMEI  |

**Return Result**

| Field       | Type  | Description                            |
| ---------- | -------------- | ---------------------- |
| **error**  | integer | Error code, 0 success, non-0 failure        |
| **reason** | string   | Message                         |
| **result** | object | Result                    |

**result**

| Field                  | Type               | Description                                                           |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **active_time**         | string           | Device activation time                                                   |
| **brand**             | string            | Device model                                                        |
| **camera_channel**    | array      | List of enabled channel numbers, in integer array format                            |
| **camera_count**       | integer            | Number of device cameras                                                |
| **create_time**      | string             | Device creation time                                                    |
| **device_form** | integer | Device physical form, stored by bit. When multiple forms coexist, get value by bit. 0x01: Wired Locator, 0x02: Wireless Locator, 0x04: OBD, 0x08: Recorder, 0x16: Rearview Mirror, 0x32: Large Screen Vehicle Unit   |
| **device_id**   | string  | Device ID, fill in IMEI                                           |
| **device_name**| string  | Device name                                                        |
| **factory**   | string    | Device manufacturer                                                       |
| **iccid**     | string    | SIM card ICCID                                                     |
| **network_type** | integer  | Network type, 0-2G, 1-3G, 2-4G, 3-5G                              |
| **ops_state**  | integer   | Device operational status, 0-Normal, 3-Not Activated, 4-Service Expired Pending Renewal, 6-Suspended, 7-Renewed Pending Online Activation, 8-Unused, 9-Cancelled, Other statuses unused  |
| **typeid**     | integer    | Device type ID                                                   |
| **update_time** | string    | Device modification time                                                 |
| **total_space** | integer    | SD card total capacity (unit: MB)                                                 |
| **used_space** | integer    | SD card used capacity (unit: MB)                                                 |


### 2. Get Device Online Status

```
GET /open/v1/getdeviceonlinestatus
```

**Parameters**

| Field                  | Type               | Description                      |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **appkey**     | string| API request APPKEY        |
| **device_id**  | string| Device ID, fill in IMEI  |

**Return Result**

| Field                  | Type               | Description                      |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **error**  | integer | Error code                                                           |
| **reason**  | string | Message                                                             |
| **result** | object | Result         |

**result**

| Field                  | Type               | Description                      |
| --------------------------------| --------- | ------------------------------------------------------------  |
| **device_id**  | string| Device ID, fill in IMEI            |
| **isonline**   | integer| Whether device is online, 0-Offline, 1-Online  |


### 3. Get Device Live Video Monitoring (Live Streaming) Viewer List

```
GET /open/v1/getdevicelivestatus
```

**Parameters**

| Field                       | Type    | Description           |
| ----------------------------- | ------- | -------------------- |
| **appkey**     | string| API request APPKEY         |
| **channel**    | integer| Viewing channel number            |
| **device_id**  | string| Device ID, fill in IMEI   |

**Return Result**

| Field                    | Type    | Description                                                       |
| --------------------------| ------------------------------------------------------------ | -----------  |
| **error**  | integer  | Error code                                                           |
| **reason** | string   | Message                                                             |
| **result**  | object | Result         |

**result**

Get device live video monitoring (live streaming) viewer list result

| Field                     | Type       | Description                                                                |
| ------------------------------| ------------------------------------------------------------  | -------------------- |
| **channel**    | integer | Viewing channel number                                                                 |
| **device_id**  | string | Device ID, fill in IMEI                                                        |
| **total**      | integer | Total current viewers                                                             |
| **watch_list** | array | Viewer list              |

**watch_list**

Viewer list structure

| Field          | Type                  | Description                           |
| ------------------------------- | -------------------------------------------- | ------- |
| **client_code** | integer | Stream pulling user code                                  |
| **is_watching** | integer | Whether currently watching                                  |
| **start_time**  | string | Watch start time                                   |
| **stop_time**   | string | Watch end time, if currently watching, this field is empty   |

### 4. Get Device Audio/Video Properties

```
GET /open/v1/GetDeviceLiveProperty
```

**Parameters**

| Field                         | Type | Description           |
| ----------------------------- | -------------------- | ------ |
| **device_id**  | string| Device ID, fill in IMEI  |

**Return Result**

| Field                | Type       | Description                                                       |
| -------------------------- | ----------- | ----------------------------------------------------------- |
| **error**   | integer| Error code                                                           |
| **reason**  | string| Message                                                              |
| **result**  | object | Result         |

**result**

| Field                        | Type        | Description                                                                                   |
| ----------------------------------- | -------------------------------------- | ------------------------------------------------------------ |
| **camera**         | array | Camera information                              |
| **device_name**    | string   | Device name                                                                                     |
| **isSupportLive**  | integer  | Whether live video monitoring is supported: 1-Yes, 0-No                                                        |
| **isSupportReplay**| integer  | Whether historical video playback is supported: 1-Yes, 0-No                                                             |
| **maxLiveChannel** | integer   | Maximum number of channels supporting live video monitoring simultaneously                                                      |

**camera**

| Field                       | Type          | Description                                                                                  |
| ----------------------------------- | -------------------------------------- | ------------------------------------------------------------ |
| **channel**   | integer | Camera channel number                        |
| **name** | string| Camera channel name  |



### 5. Get Device Historical Trip List

```
POST /open/v1/GetTravelList
```

**Parameters**

| Field                      | Type     | Description                                                         |
| ------------------------------ | --------------------------------------- | --------------------------------- |
| **begin_time**  | string | Query start time, format: yyyy-MM-dd HH:mm:ss                            |
| **device_id**   | string  | Device ID, fill in IMEI                                              |
| **end_time**    | string | Query end time, format: yyyy-MM-dd HH:mm:ss                            |
| **page_info**   | object | Pagination parameter                                |

**page_info**

Pagination information

| Field                         | Type  | Description                       |
| ----------------------------- | -------------------------------- | ------- |
| **page_num**   | integer | Page number, starting from 1                 |
| **page_size**  | integer| Page size                          |



**Return Result**

| Field                     | Type   | Description                                                        |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer| Error code                                                             |
| **reason**  | string | Message                                                               |
| **result**  | object | Get trip list  |

**result**

| Field                       | Type   | Description                                                         |
| ----------------------------- | ------------ | ------------------------------------------------------------ |
| **list**       | array | Trip information list  |
| **page_info**  | object | Pagination information      |

**list**

| Field                          | Type     | Description                               |
| ---------------------------------- | --------------------------------------- | ------- |
| **avg_speed**       | integer | Trip average speed, unit km/h                  |
| **celerate**        | string| Rapid acceleration                                    |
| **decelerate**      | string| Rapid deceleration                                    |
| **drive_score**     | integer | Current trip driving score                        |
| **max_speed**       | integer| Maximum speed, unit km/h                        |
| **over_speed**      | string| Over-speed value                                  |
| **start_address**   | string| Trip start address description                          |
| **start_lat**       | string| Trip start latitude, WGS84 coordinate system                 |
| **start_lon**       | string| Trip start longitude, WGS84 coordinate system                 |
| **start_time**      | string| Trip start time, format: yyyy-MM-dd HH:mm:ss   |
| **stop_acc**        | string| Number of times vehicle stopped without engine off                            |
| **stop_address**    | string| Trip end address description                          |
| **stop_lat**        | string | Trip end latitude, WGS84 coordinate system                |
| **stop_lon**        | string| Trip end longitude, WGS84 coordinate system                 |
| **stop_time**       | string| Trip stop time, format: yyyy-MM-dd HH:mm:ss   |
| **total_time**      | string| Total trip time, unit: H                        |
| **travel_id**       | string| Trip ID                                    |
| **travel_mileage**  | string| Trip mileage, unit: km                         |
| **travel_oil**      | string| Trip fuel consumption, unit: L                         |

**page_info**

Pagination information

| Field      | Type| Description         |
| --------- | -------- | ------- |
| **total** | integer| Total records  |



### 6. Get Device Latest Trip Information

```
POST /open/v1/GetCurrentTravel
```

**Parameters**

| Field                          | Type | Description                    |
| ----------------------------- | -------------------- | ---------------- |
| **device_id**  | array | Device ID, fill in IMEI, string array format |



**Return Result**



| Field                  | Type      | Description                                                       |
| -------------------------- | ----------- | ------------------------------------------------------------ |
| **error**   | integer| Error code                                                            |
| **reason**  | string | Message                                                              |
| **result**  | array | Trip information     |

**result**

| Field                        | Type        | Description                                        |
| ---------------------------------- | ----------------------------------------- | --------------- |
| **avg_speed**     | integer   | Trip average speed, unit km/h                             |
| **complete**      | integer  | Whether completed: 0-Incomplete, 1-Complete                       |
| **max_speed**     | integer  | Maximum speed when engine off, unit km/h                        |
| **pos_count**     | integer  | Number of tracks uploaded in this trip                             |
| **remark**        | string   | Remark information, indicating trip start/stop related information                 |
| **start_lat**     | double  | Trip start latitude, WGS84 coordinate system                |
| **start_lon**     | double   | Trip start longitude, WGS84 coordinate system               |
| **start_mileage** | double  | Trip start total mileage                             |
| **start_time**    | string  | Trip start time, format: yyyy-MM-dd HH:mm:ss             |
| **stop_lat**      | double  | Trip engine off latitude, WGS84 coordinate system                |
| **stop_lon**      | double  | Trip engine off longitude, WGS84 coordinate system                |
| **stop_time**     | string  | Trip engine off time, format: yyyy-MM-dd HH:mm:ss           |
| **travel_mileage** | integer  | Current trip mileage (unit: m)                             |
| **travel_period**  | integer  | Current trip duration (unit: seconds)                            |



### 7. Get Device Real-time Location Information

```
POST /open/v1/GetRealtimeTrackList
```

**Parameters**

| Field                     | Type          | Description                                                             |
| ---------------------------------- | ------------------------------------------------------------ | ---------------- |
| **device_id**     | array | Device ID, fill in IMEI, string array format                             |
| **map_coord_type** | integer | Map coordinate system: 0-WGS84 (default), 1-BD09 (Baidu Map), 2-GCJ02 (AutoNavi Map, Tencent Map)           |



**Return Result**

| Field                  | Type      | Description                                                        |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer  | Error code                                                           |
| **reason**  | string | Message                                                               |
| **result**  | array | Real-time track information  |

**result**

| Field                        | Type             | Description                  |
| --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **acc**         | integer           | ACC status (0-Engine off, 1-Start)                                                                                         |
| **alarm_desc**       | string    | Recent alarm detailed description                                                                                              |
| **alarm_flag**      | integer     | Whether device is currently in alarm status: 0-No alarm, 1-Alarm status                                                                     |
| **alarm_type**       | string      | Recent alarm type Chinese description             |
| **altitude**     | integer             | Altitude, unit m               |
| **beidou_signal**   | integer      | Number of Beidou satellites                                                                                                      |
| **city_name**     | string           | Current city name                                                                                                |
| **device_id**      | string       | Device ID, fill in IMEI                                                                                               |
| **direct**       | integer         | Direction                                                                                                              |
| **driving_status**    | integer     | Current vehicle driving status: 0-Engine off, 1-Start                                                                                 |
| **etc**           | object   | ETC status information                                                  |
| **gps_flag**          | integer       | Current positioning identifier (0: GPS positioning, 2: Base station positioning, 3: WiFi positioning)                                                             |
| **gps_lat**       | double           | Current GPS positioning latitude, WGS84 coordinate system                                                                           |
| **gps_lon**      | double          | Current GPS positioning longitude, WGS84 coordinate system                                                                             |
| **gps_signal**    | integer         | Number of GPS satellites                                                                                                      |
| **gps_time**       | string         | Current GPS positioning time                                                                                                  |
| **gsm_signal**      | integer      | GSM signal strength                                                                                                       |
| **is_online**       | integer      | Current device online status: 0-Offline, 1-Online                                                                                  |
| **lbs_lat**         | double        | Recent base station positioning latitude, WGS84 coordinate system                                                                         |
| **lbs_lon**       | double         | Recent base station positioning longitude, WGS84 coordinate system                                                                          |
| **lbs_time**        | string        | Recent base station positioning time                                                                                               |
| **mileage**     | integer          | Current vehicle total mileage (unit: m)                                                                                         |
| **oil_num**        | integer       | Fuel level                                                                                                              |
| **province_name**    | string       | Current province name                                                                                                   |
| **rcv_time**      | string       | Device latest data reception time, format yyyy-MM-dd HH:mm:ss                                                                      |
| **region_name**     | string       | Current administrative region name                                                                                                |
| **speed**        | integer          | Speed, unit km/h                                                                                                    |
| **status_desc**     | string      | Status description                                                                                                           |
| **target_gps_lat**    | double      | Current GPS positioning latitude, request parameter map_coord_type specifies target coordinate system                                                   |
| **target_gps_lon**   | double      | Current GPS positioning longitude, request parameter map_coord_type specifies target coordinate system                                                    |
| **target_lbs_lat**   | double      | Recent base station positioning latitude, request parameter map_coord_type specifies target coordinate system                                                 |
| **target_lbs_lon**   | double    | Recent base station positioning longitude, request parameter map_coord_type specifies target coordinate system                                                   |
| **target_wifi_lat**  | double     | Recent WiFi positioning latitude, request parameter map_coord_type specifies target coordinate system                                                  |
| **target_wifi_lon**  | double    | Recent WiFi positioning longitude, request parameter map_coord_type specifies target coordinate system                                                   |
| **theday_init_mileage** | integer  | Total mileage as of 00:00 on current day (unit: m). Use total mileage minus theday_init_mileage to get current day's mileage                                                      |
| **voltage**     | integer          | Battery voltage                                                                                                          |
| **wifi_lat**      | double          | Recent WiFi positioning latitude, WGS84 coordinate system                                                                         |
| **wifi_lon**      | double          | Recent WiFi positioning longitude, WGS84 coordinate system                                                                         |
| **wifi_time**    | string         | Recent WiFi positioning time                                                                                                 |
|**temperature** | array | Temperature, unit: °C, double array format |
|**humidity** | array | Humidity, unit: %RH, double array format |

**etc**

| Field              | Type                   | Description                          |
| ------------------------------------ | ---------------------------------- | ------- |
| **bind_state**      | integer  | ETC binding status: 0-Unbound, 1-Bound  |
| **elec_state**       | integer | OBU tag battery status: 0-Weak battery, 1-Normal    |
| **fault_state**      | integer | ETC fault status (0: Fault, 1: Normal)     |
| **hardware_version** | string  | ETC hardware version number                       |
| **lpn**               | string | ETC bound license plate number                   |
| **obu_id**            | string| ETC bound OBU ID                    |
| **software_version**  | string| ETC software version number                        |



### 8. Get Device Historical Location Information

```
POST /open/v1/GetHistoryTrackList
```

**Parameters**

| Field                     | Type            | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ | ------- |
| **device_id**    | string   | Device ID, fill in IMEI                                           |
| **start_time**     | string | Start time, format yyyy-MM-dd HH:mm:ss                               |
| **end_time**    | string    | End time, format yyyy-MM-dd HH:mm:ss                               |
| **exact**     | integer      | 0: No filter, 2: Filter base station positioning, 3: Filter all non-GPS positioning                   |
| **limit**    | integer        | Maximum number of tracks sorted by time in ascending order                               |
| **map_coord_type** | integer | Map coordinate system: 0-WGS84 (default), 1-BD09 (Baidu Map), 2-GCJ02 (AutoNavi Map, Tencent Map)  |
| **speed_limit**    | integer | Speed filter: -1-No filter, 0-Tracks with speed less than 5km/h will be filtered, Greater than 0-Tracks with speed less than this value will be filtered  |



**Return Result**

| Field                     | Type    | Description                                                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| **error**   | integer | Error code                                                            |
| **reason**  | string | Message                                                               |
| **result**  | array | Historical track information  |

**result**

| Field                     | Type      | Description                                          |
| ------------------------------ | ------------------------------------------ | --------------- |
| **bd_lat**      | double| Latitude after Baidu Map correction                        |
| **bd_lon**      | double| Longitude after Baidu Map correction                        |
| **direct**      | integer| Direction                                                |
| **gps_time**    | string| Positioning time, format yyyy-MM-dd HH:mm:ss                     |
| **id**          | integer| Device record ID                                          |
| **lat**         | double| Latitude, WGS84 coordinate system                           |
| **lon**         | double| Longitude, WGS84 coordinate system                           |
| **mileage**     | double| Total mileage (unit: km)                          |
| **pos_mode**    | string| Positioning mode                                             |
| **rcv_time**    | string| Reception time, format yyyy-MM-dd HH:mm:ss                     |
| **speed**       | integer| Speed, unit km/h                                      |
| **status**      | string| Status description                                             |
| **target_lat**  | double| Latitude, request parameter map_coord_type specifies target coordinate system  |
| **target_lon**  | double | Longitude, request parameter map_coord_type specifies target coordinate system |



### 9. Remote Snapshot

```
POST /open/v1/snap
```

**Parameters**



| Field                           | Type     | Description                                                                  |
| ----------------------------------- | --------------------- | ------------------------------------------------------------ |
| **appkey**          | string | API request APPKEY                                                               |
| **channel**         | integer | Channel number                                                                      |
| **client_code**     | string | Client identification code                                                                 |
| **device_id**       | string | Device ID, fill in IMEI                                                         |
| **image_params**    | object | Image snapshot parameters           |
| **notify_callback** | string  | Snapshot result callback address                                                            |
| **type**            | integer  | Snapshot type: 0-Image, 1-Video                                                      |
| **video_params**    | object | Video snapshot parameters                                |

**image_params**

| Field                  | Type         | Description                                                    |
| ------------------------------ | ------------------------------------------------------------ | ------- |
| **count**    | integer   | Number of snapshots                                                      |
| **interval**  | integer  | Snapshot interval, unit: seconds                                             |
| **resolution** | integer | Image resolution: 1-240\*320 (default), 2-320\*480, 3-360\*640, 4-480\*800, 5-640\*960, 6-720\*1280  |

**video_params**

| Field                        | Type   | Description     |
| ------------------------------ | ------------- | ------- |
| **duration**    | integer| Duration, unit: seconds  |
| **resolution**  | string| Resolution          |



**Return Result**



| Field                     | Type   | Description                                                             |
| -------------------------- | ------------------------------ | ----------------------------------------------- |
| **error**   | integer| Error code, 0-Success, non-0 indicates snapshot failure                                          |
| **reason**  | string | Message                                                                    |
| **result**  | object | Specific content returned when snapshot is successful          |

**result**

Content returned by image/video snapshot

| Field                         | Type    | Description                                                        |
| -------------------------------- | ----------- | ------------------------------------------------------------ |
| **device_state**  | object | Device status     |
| **snap_event**    | object | Snapshot event                 |

**device_state**

Device status, returned when snapshot fails

| Field                     | Type           | Description                                                           |
| ---------------------------------- | -------------------------------------------- | ------- |
| **acc** 
