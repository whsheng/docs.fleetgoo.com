
## API Usage Instructions

1.  All the APIs listed in this document support HTTP calls.
2.  The domain name for API calls is: ``open.4s12580.com``.
3.  API calls require authorization. Please add the request parameter `appkey` (case-sensitive, please use lowercase) to the URL of the API call. You can obtain your `appkey` on the application information page after logging into the console.
4.  For the specific request syntax of each API, including the URI, Header, Query parameters (including appkey), Post parameters, and return parameters, please refer to the detailed description of each API.
5.  All API URLs, parameters, and return fields involved in this document must strictly match the defined case and data types.

> Last Updated: 2025/08/07 by Honsen

---

## 1. Get Device Basic Information
**Endpoint:** `GET /open/v1/getdevicebaseinfo`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code, 0 for success, non-zero for failure |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| active_time | string | Device activation time |
| brand | string | Device model |
| camera_channel | array | List of enabled channel numbers (integer array) |
| camera_count | integer | Number of cameras on the device |
| create_time | string | Device creation time |
| device_form | integer | Device physical form (bitwise storage):<br>0x01: Wired tracker<br>0x02: Wireless tracker<br>0x04: OBD<br>0x08: Recorder<br>0x16: Rearview mirror<br>0x32: Large screen infotainment |
| device_id | string | Device ID (IMEI) |
| device_name | string | Device name |
| factory | string | Device manufacturer |
| iccid | string | SIM card ICCID |
| network_type | integer | Network type: 0-2G, 1-3G, 2-4G, 3-5G |
| ops_state | integer | Device operational status:<br>0-Normal<br>3-Not activated<br>4-Service expired, renewal pending<br>6-Suspended<br>7-Renewed, pending activation<br>8-Not used<br>9-Cancelled<br>Other values: unused |
| typeid | integer | Device type ID |
| update_time | string | Device modification time |
| total_space | integer | Total SD card capacity (MB) |
| used_space | integer | Used SD card capacity (MB) |

---

## 2. Get Device Online Status
**Endpoint:** `GET /open/v1/getdeviceonlinestatus`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| isonline | integer | Device online status: 0-offline, 1-online |

---

## 3. Get Device Live Video Viewing List

**Endpoint:** `GET /open/v1/getdevicelivestatus`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| channel | integer | Viewing channel number |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | integer | Viewing channel number |
| device_id | string | Device ID (IMEI) |
| total | integer | Current total number of viewers |
| watch_list | array | Viewing list |

**Watch List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| client_code | integer | Streaming user code |
| is_watching | integer | Whether currently watching |
| start_time | string | Viewing start time |
| stop_time | string | Viewing end time (empty if currently watching) |

---

## 4. Get Device Audio/Video Properties
**Endpoint:** `GET /open/v1/GetDeviceLiveProperty`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| camera | array | Camera information |
| device_name | string | Device name |
| isSupportLive | integer | Supports live video streaming: 1-Yes, 0-No |
| isSupportReplay | integer | Supports video playback: 1-Yes, 0-No |
| maxLiveChannel | integer | Maximum number of concurrent live video channels |

**Camera Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | integer | Camera channel number |
| name | string | Camera channel name |

---

## 5. Get Device Historical Trip List
**Endpoint:** `POST /open/v1/GetTravelList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| device_id | string | Device ID (IMEI) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| page_info | object | Pagination parameters |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Trip list result |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Trip information list |
| page_info | object | Pagination information |

**Trip List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| avg_speed | integer | Average speed (km/h) |
| celerate | string | Hard acceleration events |
| decelerate | string | Hard deceleration events |
| drive_score | integer | Driving score for this trip |
| max_speed | integer | Maximum speed (km/h) |
| over_speed | string | Speeding events |
| start_address | string | Trip start address description |
| start_lat | string | Trip start latitude (WGS84) |
| start_lon | string | Trip start longitude (WGS84) |
| start_time | string | Trip start time (format: yyyy-MM-dd HH:mm:ss) |
| stop_acc | string | Number of stops with engine running |
| stop_address | string | Trip end address description |
| stop_lat | string | Trip end latitude (WGS84) |
| stop_lon | string | Trip end longitude (WGS84) |
| stop_time | string | Trip stop time (format: yyyy-MM-dd HH:mm:ss) |
| total_time | string | Total trip duration (hours) |
| travel_id | string | Trip ID |
| travel_mileage | string | Trip mileage (km) |
| travel_oil | string | Trip fuel consumption (L) |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 6. Get Device Current Trip Information
**Endpoint:** `POST /open/v1/GetCurrentTravel`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | array | Device ID (IMEI) - string array |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Trip information |

**Result Object** 

| Field | Type | Description |
| :--- | :--- | :--- |
| avg_speed | integer | Average speed (km/h) |
| complete | integer | Completion status: 0-incomplete, 1-complete |
| max_speed | integer | Maximum speed at trip end (km/h) |
| pos_count | integer | Number of track points uploaded during this trip |
| remark | string | Remarks (indicating trip start/stop information) |
| start_lat | double | Trip start latitude (WGS84) |
| start_lon | double | Trip start longitude (WGS84) |
| start_mileage | double | Total mileage at trip start |
| start_time | string | Trip start time (format: yyyy-MM-dd HH:mm:ss) |
| stop_lat | double | Trip end latitude (WGS84) |
| stop_lon | double | Trip end longitude (WGS84) |
| stop_time | string | Trip end time (format: yyyy-MM-dd HH:mm:ss) |
| travel_mileage | integer | Trip distance (meters) |
| travel_period | integer | Trip duration (seconds) |

---

## 7. Get Device Real-time Location Information
**Endpoint:** `POST /open/v1/GetRealtimeTrackList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | array | Device ID (IMEI) - string array |
| map_coord_type | integer | Map coordinate system:<br>0-WGS84 (default)<br>1-BD09 (Baidu)<br>2-GCJ02 (Gaode/Tencent) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Real-time track information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| acc | integer | ACC status (0-off, 1-on) |
| alarm_desc | string | Latest alarm details |
| alarm_flag | integer | Device alarm status: 0-not alarming, 1-alarming |
| alarm_type | string | Latest alarm type description |
| altitude | integer | Altitude (meters) |
| beidou_signal | integer | Number of BeiDou satellites |
| city_name | string | Current city name |
| device_id | string | Device ID (IMEI) |
| direct | integer | Direction |
| driving_status | integer | Vehicle status: 0-off, 1-running |
| etc | object | ETC status information |
| gps_flag | integer | Current positioning method:<br>0-GPS<br>2-Cell tower<br>3-WiFi |
| gps_lat | double | Current GPS latitude (WGS84) |
| gps_lon | double | Current GPS longitude (WGS84) |
| gps_signal | integer | Number of GPS satellites |
| gps_time | string | Current GPS time |
| gsm_signal | integer | GSM signal strength |
| is_online | integer | Device online status: 0-offline, 1-online |
| lbs_lat | double | Latest cell tower latitude (WGS84) |
| lbs_lon | double | Latest cell tower longitude (WGS84) |
| lbs_time | string | Latest cell tower positioning time |
| mileage | integer | Current total vehicle mileage (meters) |
| oil_num | integer | Fuel level |
| province_name | string | Current province name |
| rcv_time | string | Latest data reception time (format: yyyy-MM-dd HH:mm:ss) |
| region_name | string | Current administrative region name |
| speed | integer | Speed (km/h) |
| status_desc | string | Status description |
| target_gps_lat | double | GPS latitude in target coordinate system |
| target_gps_lon | double | GPS longitude in target coordinate system |
| target_lbs_lat | double | Cell tower latitude in target coordinate system |
| target_lbs_lon | double | Cell tower longitude in target coordinate system |
| target_wifi_lat | double | WiFi latitude in target coordinate system |
| target_wifi_lon | double | WiFi longitude in target coordinate system |
| theday_init_mileage | integer | Total mileage at 00:00 of the day (meters) |
| voltage | integer | Battery voltage |
| wifi_lat | double | Latest WiFi latitude (WGS84) |
| wifi_lon | double | Latest WiFi longitude (WGS84) |
| wifi_time | string | Latest WiFi positioning time |
| temperature | array | Temperature (°C) - double array |
| humidity | array | Humidity (%RH) - double array |

**ETC Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| bind_state | integer | ETC binding status: 0-not bound, 1-bound |
| elec_state | integer | OBU battery status: 0-low, 1-normal |
| fault_state | integer | ETC fault status: 0-fault, 1-normal |
| hardware_version | string | ETC hardware version |
| lpn | string | Bound license plate number |
| obu_id | string | Bound OBU ID |
| software_version | string | ETC software version |

---

## 8. Get Device Historical Location Information
**Endpoint:** `POST /open/v1/GetHistoryTrackList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| start_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| exact | integer | Filtering:<br>0-no filter<br>2-filter cell tower positioning<br>3-filter all non-GPS positioning |
| limit | integer | Maximum number of track points (ascending by time) |
| map_coord_type | integer | Map coordinate system:<br>0-WGS84 (default)<br>1-BD09 (Baidu)<br>2-GCJ02 (Gaode/Tencent) |
| speed_limit | integer | Speed filter:<br>-1-no filter<br>0-filter speeds < 5km/h<br>>0-filter speeds < specified value |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Historical track information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| bd_lat | double | Baidu map corrected latitude |
| bd_lon | double | Baidu map corrected longitude |
| direct | integer | Direction |
| gps_time | string | Positioning time (format: yyyy-MM-dd HH:mm:ss) |
| id | integer | Device record ID |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |
| mileage | double | Total mileage (km) |
| pos_mode | string | Positioning method |
| rcv_time | string | Reception time (format: yyyy-MM-dd HH:mm:ss) |
| speed | integer | Speed (km/h) |
| status | string | Status description |
| target_lat | double | Latitude in target coordinate system |
| target_lon | double | Longitude in target coordinate system |

---

## 9. Remote Snapshot
**Endpoint:** `POST /open/v1/snap`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| channel | integer | Channel number |
| client_code | string | Client identification code |
| device_id | string | Device ID (IMEI) |
| image_params | object | Image snapshot parameters |
| notify_callback | string | Snapshot result callback URL |
| type | integer | Snapshot type: 0-image, 1-video |
| video_params | object | Video snapshot parameters |

**Image Parameters**

| Field | Type | Description |
| :--- | :--- | :--- |
| count | integer | Number of snapshots |
| interval | integer | Snapshot interval (seconds) |
| resolution | integer | Image resolution:<br>1-240\*320 (default)<br>2-320\*480<br>3-360\*640<br>4-480\*800<br>5-640\*960<br>6-720\*1280 |

**Video Parameters**

| Field | Type | Description |
| :--- | :--- | :--- |
| duration | integer | Duration (seconds) |
| resolution | string | Resolution |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code, 0-success, non-zero-failure |
| reason | string | Message |
| result | object | Snapshot result details |

**Result Object  (Success)** 

| Field | Type | Description |
| :--- | :--- | :--- |
| device_state | object | Device status |
| snap_event | object | Snapshot event |

**Device State Object (Failure)**

| Field | Type | Description |
| :--- | :--- | :--- |
| direct | integer | Direction |
| driving_status | integer | Vehicle status: 0-off, 1-running |
| gps_lat | double | Current GPS latitude (WGS84), or last known if offline |
| gps_lon | double | Current GPS longitude (WGS84), or last known if offline |
| gps_signal | integer | Number of GPS satellites |
| gps_time | string | Current GPS time (format: yyyy-MM-dd HH:mm:ss), or last known if offline |
| is_online | integer | Device online status: 0-offline, 1-online |
| speed | integer | Speed (km/h) |

**Snapshot Event Object (Success)**

| Field | Type | Description |
| :--- | :--- | :--- |
| event_id | integer | Snapshot event ID (unique identifier) |

---

## 10. Get Historical Snapshot List by Time Range
**Endpoint:** `POST /open/v1/GetHistorySnapList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | string | Camera channel number |
| device_id | string | Device ID (IMEI) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| page_info | object | Pagination parameters |
| start_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| user_id | integer | User ID |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Historical snapshot result |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Historical snapshot list |
| page_info | object | Pagination information |

**List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | string | Camera channel number |
| create_time | string | Creation time (format: yyyy-MM-dd HH:mm:ss) |
| event_id | integer | Snapshot event ID (unique identifier) |
| event_time | string | Snapshot completion time (format: yyyy-MM-dd HH:mm:ss) |
| event_type | integer | Event type:<br>101-Image snapshot<br>102-Vibration alarm<br>103-Video snapshot<br>10001-Timed snapshot<br>10002-Distance-based snapshot |
| image_url | array | Image snapshot result URLs (string array) |
| pos | object | Position |
| shoot_time | string | Snapshot time (format: yyyy-MM-dd HH:mm:ss) |
| source | string | Snapshot request source |
| thumb_url | string | Video thumbnail URL |
| vedio_url | string | Video snapshot result URL |

**Position Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| direct | integer | GPS direction |
| gps_time | string | GPS positioning time (format: yyyy-MM-dd HH:mm:ss) |
| lat | double | GPS latitude (WGS84) |
| lng | double | GPS longitude (WGS84) |
| speed | integer | GPS speed (km/h) |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 11. Get Historical Snapshot Details by ID
**Endpoint:** `GET /open/v1/GetSnapByID`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| event_id | integer | Snapshot event ID (unique identifier) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Historical snapshot details |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | string | Camera channel number |
| create_time | string | Creation time (format: yyyy-MM-dd HH:mm:ss) |
| event_id | integer | Snapshot event ID (unique identifier) |
| event_time | string | Snapshot completion time (format: yyyy-MM-dd HH:mm:ss) |
| event_type | integer | Event type:<br>101-Image snapshot<br>102-Vibration alarm<br>103-Video snapshot |
| image_url | array | Image snapshot result URLs (string array) |
| pos | object | Position |
| shoot_time | string | Snapshot time (format: yyyy-MM-dd HH:mm:ss) |
| source | string | Snapshot request source |
| thumb_url | string | Video thumbnail URL |
| vedio_url | string | Video snapshot result URL |

**Position Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| direct | integer | GPS direction |
| gps_time | string | GPS positioning time (format: yyyy-MM-dd HH:mm:ss) |
| lat | double | GPS latitude (WGS84) |
| lng | double | GPS longitude (WGS84) |
| speed | integer | GPS speed (km/h) |

---

## 12. Get Administrative Region by Coordinates
**Endpoint:** `POST /open/v1/GetLngLatArea`

**Parameters** 

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | GPS latitude (WGS84) |
| lng | double | GPS longitude (WGS84) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| city | string | City name |
| province | string | Province name |
| region | string | District name |

---

## 13. Query SIM Card Detailed Information
**Endpoint:** `POST /open/v1/GetSimDetail`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| iccid | string | ICCID number |
| imsi | string | IMSI number |
| sim | string | SIM card number |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | SIM card information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| active_pg_name | string | Package name |
| active_pg_status | integer | Gift package real-name status: 1-activate to get package, 0-no package |
| active_pg_way | integer | Gift package method: 1-personal, 2-mobile |
| amount_usage | double | Period data usage (KB) |
| app_package_list | array | Application list |
| expire_date | string | Expiration time (format: yyyy-MM-dd HH:mm:ss) |
| first_active | string | First activation time (format: yyyy-MM-dd HH:mm:ss) |
| flowleft_time | string | Data synchronization time |
| iccid | string | SIM card ICCID |
| imei | string | Bound device IMEI |
| imsi | string | SIM card IMSI |
| is_reset | integer | Whether reset |
| last_active | string | Last activation time (format: yyyy-MM-dd HH:mm:ss) |
| month_usage | double | Monthly usage (KB) |
| network_speed | string | Network speed: High, Medium, Low |
| norealname_renewals | integer | Allow renewal without real-name: 0-no, 1-yes |
| package | string | Package name |
| package_info | string | Package information |
| package_period | integer | Package period (days) |
| package_usage | double | Package usage (KB) |
| packagesn | integer | Package serial number |
| packageupdate_time | string | Package update time (format: yyyy-MM-dd HH:mm:ss) |
| period_months | integer | Package period (months) |
| realname_status | integer | SIM card real-name status:<br>0-not real-name<br>1-real-name<br>2-pending review |
| realname_term | string | Real-name certification validity period |
| sim | string | SIM card number |
| status | integer | Card status:<br>0-stock<br>1-testable<br>2-activatable<br>3-activated<br>4-deactivated<br>5-expired<br>6-cancelled<br>7-replaced |
| status_desc | string | Card status description |
| surplus_period | integer | Remaining days |
| surplus_usage | double | Remaining data (KB) |
| system_time | string | System time |
| total_surplus_usage | double | Total remaining data (KB) |
| total_usage | double | Historical usage (KB) |

**Application Package List**

| Field | Type | Description |
| :--- | :--- | :--- |
| amountUsage | double | Period data usage (KB) |
| appName | string | Application group name |
| expireTime | string | Expiration time (format: yyyy-MM-dd HH:mm:ss) |
| flowLeftValue | double | Remaining usage (KB) |
| living_realname | integer | Live real-name status: 1-face verification, 0-normal |
| periodEndTime | string | Period end time (format: yyyy-MM-dd HH:mm:ss) |
| periodStartTime | string | Period start time (format: yyyy-MM-dd HH:mm:ss) |
| surplusPeriod | integer | Remaining days |

---

## 14. Batch Query SIM Card Information
**Endpoint:** `POST /open/v1/GetSimDetails`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| iccid | array | ICCID numbers (string array) |
| imsi | array | IMSI numbers (string array) |
| sim | array | SIM card numbers (string array) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | SIM card information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| amount_usage | double | Period data usage (KB) |
| expire_date | string | Expiration time (format: yyyy-MM-dd HH:mm:ss) |
| first_active | string | First activation time (format: yyyy-MM-dd HH:mm:ss) |
| iccid | string | SIM card ICCID |
| imei | string | Bound device IMEI |
| imsi | string | SIM card IMSI |
| last_active | string | Last activation time (format: yyyy-MM-dd HH:mm:ss) |
| month_usage | double | Monthly usage (KB) |
| package | string | Package name |
| packagesn | integer | Package serial number |
| realname_status | integer | Real-name status:<br>0-not real-name<br>1-real-name<br>2-pending review |
| sim | string | SIM card number |
| status | integer | SIM card status:<br>0-stock<br>1-testable<br>2-activatable<br>3-activated<br>4-deactivated<br>5-expired<br>6-cancelled<br>7-replaced |
| status_desc | string | SIM card status description |
| surplus_period | integer | Remaining days |
| surplus_usage | double | Remaining data (KB) |
| total_usage | double | Historical usage (KB) |

---

## 15. Get Device Parameter Settings List
**Endpoint:** `GET /open/v1/GetDeviceParamList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Settings list |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| setList | array | Parameter settings list |
| typeName | string | Device type name |

**Set List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| cmdType | string | Command type |
| enable | string | Enabled status: 1-enabled, 0-disabled |
| interactionType | string | Interaction type |
| range | array | Option list |
| setTitle | string | Title |
| settingName | string | Parameter name |
| uiType | string | Interface type |
| value | string | Parameter value |

**Range Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| Key | string | Option key |
| Value | string | Option value |

---

## 16. Save Device Single Parameter Setting
**Endpoint:** `GET /open/v1/SetDeviceParam`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| param_type | string | Parameter type (from GetDeviceParamList) |
| param_value | string | Parameter value (from GetDeviceParamList) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 17. Transparent Transmission of Device Single Parameter Setting
**Endpoint:** `POST /open/v1/SendDeviceParamCmd`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| command_content | string | Transparent transmission command content |
| device_id | string | Device ID (IMEI) |

**Response**  
| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 18. Get Device Historical Video List
**Endpoint:** `GET /open/v1/getvideolist`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| channel | integer | Camera channel |
| device_id | string | Device ID (IMEI) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| format | string | File format (e.g., MP4, AVI) |
| storage_type | integer | Storage type:<br>1-local<br>2-cloud<br>3-local and cloud |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| video_list | array | Result list |

**Video List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | string | Video start time (format: yyyy-MM-dd HH:mm:ss) |
| channel | integer | Camera channel number |
| cloud_url | string | Cloud storage URL (for storage types 1 and 2) |
| duration | integer | Video duration (seconds) |
| end_time | string | Video end time (format: yyyy-MM-dd HH:mm:ss) |
| file_modify_time | string | File last modification time (format: yyyy-MM-dd HH:mm:ss) |
| file_size | integer | File size (bytes) |
| format | string | File format suffix (e.g., MP4, AVI) |
| index_id | integer | File index ID |
| local_file_name | string | Local file name on device |
| local_file_path | string | Local file path on device |
| storage_type | integer | Storage type:<br>0-device local storage<br>1-cloud storage<br>3-both local and cloud storage |

---

## 19. Get Purchased Cloud Storage Package Information
**Endpoint:** `GET /open/v1/cloudStorage/userPackageInfo`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| buy_time | string | Purchase time |
| cloud_recorder_package | object | Recorder package configuration |
| event_package | object | Event package configuration |
| live_package | object | Live package configuration |
| package_desc | string | Package description |
| package_id | integer | Purchased package ID |
| package_subtitle | string | Package subtitle |
| package_title | string | Package name |
| package_type | integer | Package type:<br>0-normal<br>1-add-on<br>2-expansion |
| parking_snap_package | object | Parking snapshot package configuration |
| save_live_package | object | Save live package configuration |
| snap_package | object | Snapshot package configuration |
| state | integer | Package status:<br>0-not activated<br>1-activated<br>2-expired |
| track_package | object | Track package configuration |
| travel_package | object | Trip package configuration |
| user_package_id | integer | Package ID (linked to op_user_package.id) |

**Cloud Recorder Package**

| Field | Type | Description |
| :--- | :--- | :--- |
| active_time | string | Activation time |
| effect_time | string | Effective time |
| expired_time | string | Package expiration time |
| package_remaining_time | integer | Remaining package time |
| period | integer | Package validity period (days) |
| total_mileage | integer | Total mileage |
| total_play_duration | integer | Cloud recorder video playback duration |
| used_mileage | integer | Used mileage within package |

**Common Package Configuration**

(Event, Save Live, Snapshot, Track, Trip packages)
| Field | Type | Description |
| :--- | :--- | :--- |
| active_time | string | Activation time |
| business_type | integer | Package type:<br>1-image<br>2-video<br>3-event<br>4-trip<br>5-track |
| effect_time | string | Effective time |
| expired_time | string | Package expiration time |
| package_remaining_time | integer | Remaining package time |
| search_duration | integer | Snapshot viewing duration |

**Live Package**

| Field | Type | Description |
| :--- | :--- | :--- |
| active_time | string | Activation time |
| effect_time | string | Effective time |
| expired_time | string | Package expiration time |
| live_duration | integer | Cloud recorder video playback duration |
| live_interval | integer | Live duration (seconds) |
| live_limit_times | integer | Live limit times |
| package_remaining_time | integer | Remaining package time |
| pause_time | string | Pause time |

**Parking Snapshot Package**

| Field | Type | Description |
| :--- | :--- | :--- |
| active_time | string | Activation time |
| effect_time | string | Effective time |
| expired_time | string | Package expiration time |
| package_remaining_time | integer | Remaining package time |
| search_duration | integer | Snapshot duration |

---

## 20. Query Cloud Storage Timeline
**Endpoint:** `POST /open/v1/cloudStorage/getTimeLine`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | integer | Start time (UNIX timestamp) |
| channel | integer | Camera channel number:<br>-1: all channels<br>>-1: specific channel<br>(When channel=-1, returned channel will also be -1) |
| cur_date | string | Playback date (format: yyyy-MM-dd) |
| device_id | string | Device ID (IMEI) |
| duration | integer | Total video duration (minutes) |
| end_time | integer | End time (UNIX timestamp) |
| sliding_type | integer | Slide type:<br>0-slide left<br>1-slide right<br>(Used only for slide queries) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | integer | Previous query start time (UNIX timestamp) |
| end_time | integer | Previous query end time (UNIX timestamp) |
| imei | string | Device IMEI |
| time_lines | array | List information |

**Time Lines Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | integer | Camera channel number |
| end | integer | End time (UNIX timestamp) |
| start | integer | Start time (UNIX timestamp) |
| thumb_url | string | Thumbnail URL |

---

## 21. Retrieve Cloud Storage File List
**Endpoint:** `POST /open/v1/cloudStorage/getIndex`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | integer | Start time (UNIX timestamp) |
| channel | integer | Camera channel number |
| device_id | string | Device ID (IMEI) |
| end_time | integer | End time (UNIX timestamp) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| indexes | array | List information |

**Indexes Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| channel | integer | Camera channel number |
| end_time | integer | End time (UNIX timestamp) |
| file_size | integer | File size (bytes) |
| frame_cnt | integer | Total video frames |
| id | integer | ID |
| meta_data_url | string | Structured metadata OSS path |
| meta_end_time | integer | Video frame end timestamp (milliseconds) |
| meta_start_time | integer | Video frame start timestamp (milliseconds) |
| play_duration | integer | Playback duration (milliseconds) |
| start_time | integer | Start time (UNIX timestamp) |
| thumb_url | string | Thumbnail URL |
| url | string | Video file URL |

---

## 22. Query Cloud Storage Video Calendar
**Endpoint:** `POST /open/v1/cloudStorage/getCalendar`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| month | string | Query month (format: yyyy-MM) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | List information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| date | string | Date (format: yyyy-MM-dd) |
| event_count | integer | Number of events |
| is_enable | bool | Valid status: 0-invalid, 1-valid |
| video_duration | integer | Video duration (minutes) |

---

## 23. Query Cloud Storage Event Tag List
**Endpoint:** `GET /open/v1/cloudStorage/getVideoLabel`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| device_id | string | Device ID (IMEI) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| event_id | integer | Event ID |
| gps_time | string | GPS time (format: YYYY-MM-dd HH:mm:ss) |
| label_desc | string | Label description |
| label_sub_type | integer | Label sub-type:<br>0-hard acceleration<br>1-hard deceleration<br>2-hard turn<br>23-video lock<br>24-ADAS alarm event |
| label_type | integer | Label type: 1-cloud storage |
| rcv_time | string | Reception time (format: YYYY-MM-dd HH:mm:ss) |
| start_lat | double | Event start latitude (WGS84) |
| start_lon | double | Event start longitude (WGS84) |
| start_time | string | Start time (format: YYYY-MM-dd HH:mm:ss) |
| stop_lat | double | Event end latitude (WGS84) |
| stop_lon | double | Event end longitude (WGS84) |
| stop_time | string | Stop time (format: YYYY-MM-dd HH:mm:ss) |

---

## 24. Add Video Recording Task
**Endpoint:** `POST /open/v1/UploadVideoRecordingParams`

**Parameters** 

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | integer | Start time (UNIX timestamp) |
| channel | integer | Recording task camera channel number |
| device_id | string | Device ID (IMEI) |
| end_time | integer | End time (UNIX timestamp) |
| query_time | integer | Query time (UNIX timestamp) |
| state | integer | Task status:<br>0-empty<br>1-unprocessed<br>2-processing failed<br>3-processing successful |
| task_type | integer | Recording type:<br>0-video<br>1-image |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| seq | string | Query sequence number |

---

## 25. Query Video Recording Task
**Endpoint:** `POST /open/v1/GetVideoRecordingResult`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| seq | string | Query sequence number |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | integer | Start time (UNIX timestamp) |
| channel | integer | Recorded file camera channel number |
| device_id | string | Device ID (IMEI) |
| end_time | integer | End time (UNIX timestamp) |
| image_url | array | Screenshot image paths (string array) |
| state | integer | Task status:<br>0-empty<br>1-unprocessed<br>2-processing failed<br>3-processing successful |
| task_type | integer | Recording type:<br>0-video<br>1-image |
| video_url | string | Video file URL |

---

## 26. Device Firmware Upgrade Command
**Endpoint:** `POST /open/v1/DeviceFirmwareUpgrage`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| imei | string | Device IMEI |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 27. Text to Speech
**Endpoint:** `POST /open/v1/TextToSpeech`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| content | string | Text content for speech |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 28. Query Device Mileage by Day
**Endpoint:** `POST /open/v1/GetDeviceMileage`

**Description**

1. Query range is within the last three months
2. Results are displayed day by day
3. Days without data are not returned

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| end_date | string | End date (format: yyyy-MM-dd) |
| start_date | string | Start date (format: yyyy-MM-dd) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| mileage | double | Device mileage (km) |
| travel_day | string | Travel date (format: yyyy-MM-dd) |

---

## 29. Query Device Warning List
**Endpoint:** `GET /open/v1/GetDeviceWarnings`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| warningList | array | Warning list |

**Warning List Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| code | integer | Warning code:<br>0x000a-SD card error<br>0x000b-camera error |
| reason | string | Warning reason |

---

## 30. Set Geofence
**Endpoint:** `POST /open/v1/SetFence`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| fence_name | string | Fence name |
| fence_type | integer | Fence type:<br>0-circular<br>1-polygon<br>7-road maintenance route |
| flag | integer | Trigger alarm type:<br>0-enter fence<br>1-exit fence<br>2-enter/exit fence<br>3-cancel |
| circle | object | Circular fence information (valid when fence_type=0) |
| polygon_coord_list | array | Polygon fence coordinate list (valid when fence_type=1) |
| line_coord_list | array | Road maintenance route fence coordinate list (valid when fence_type=7) |
| remark | string | Remarks |

**Circle Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |
| radius | integer | Circular fence radius (meters) |

**Polygon Coordinate List**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |

**Line Coordinate List**
| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| fence_id | integer | Fence ID |

---

## 31. Delete Geofence
**Endpoint:** `POST /open/v1/DelFence`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| fence_id | integer | Fence ID |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 32. Update Geofence
**Endpoint:** `POST /open/v1/UpdateFence`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| fence_id | integer | Fence ID |
| device_id | string | Device ID (IMEI) |
| fence_name | string | Fence name |
| fence_type | integer | Fence type:<br>0-circular<br>1-polygon<br>7-road maintenance route |
| flag | integer | Trigger alarm type:<br>0-enter fence<br>1-exit fence<br>2-enter/exit fence<br>3-cancel |
| circle | object | Circular fence information (valid when fence_type=0) |
| polygon_coord_list | array | Polygon fence coordinate list (valid when fence_type=1) |
| line_coord_list | array | Road maintenance route fence coordinate list (valid when fence_type=7) |
| remark | string | Remarks |

**Circle Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |
| radius | integer | Circular fence radius (meters) |

**Polygon Coordinate List**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |

**Line Coordinate List**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 33. Query Geofence
**Endpoint:** `POST /open/v1/GetFence`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| fence_id | integer | Fence ID (optional):<br>- If not provided, query all fences bound to this device<br>- If provided, query information for this fence ID (no information returned if device not bound to this fence) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Result data |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| fence_id | integer | Fence ID |
| device_id | string | Device ID (IMEI) |
| fence_name | string | Fence name |
| fence_type | integer | Fence type:<br>0-circular<br>1-polygon<br>7-road maintenance route |
| flag | integer | Trigger alarm type:<br>0-enter fence<br>1-exit fence<br>2-enter/exit fence<br>3-cancel |
| circle | object | Circular fence information (valid when fence_type=0) |
| polygon_coord_list | array | Polygon fence coordinate list (valid when fence_type=1) |
| line_coord_list | array | Road maintenance route fence coordinate list (valid when fence_type=7) |
| remark | string | Remarks |
| create_date | string | Creation time (format: yyyy-MM-dd HH:mm:ss) |
| update_date | string | Update time (format: yyyy-MM-dd HH:mm:ss) |

**Circle Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |
| radius | integer | Circular fence radius (meters) |

**Polygon Coordinate List**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |

**Line Coordinate List**

| Field | Type | Description |
| :--- | :--- | :--- |
| lat | double | Latitude (WGS84) |
| lon | double | Longitude (WGS84) |

---

## 34. Query ETC Charging Information List
**Endpoint:** `POST /open/v1/GetEtcCharging`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| page_info | object | Pagination parameters |
| start_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | ETC charging information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | ETC charging list |
| page_info | object | Pagination information |

**List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| deduction_amount | integer | ETC deduction amount (cents) |
| deduction_time | string | Deduction time (format: yyyy-MM-dd HH:mm:ss) |
| e_ecn | string | Entry/exit toll network number |
| e_ets | string | Entry/exit toll station number |
| etcat | integer | Transaction antenna type:<br>0xa1-entry<br>0xa2-exit |
| lane_number | string | Lane number |
| lpn | string | License plate number |
| net_time | string | Real-time network time (format: yyyy-MM-dd HH:mm:ss) |
| status_flag | integer | Transaction status flag:<br>0x00-OK<br>0x01-ERR |
| transaction_type | integer | Transaction type:<br>0x81-closed toll road transaction<br>0x90-other closed applications |
| vin | string | VIN |
| weight | integer | Truck total weight (kg) |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 35. Query ETC Gantry Information List
**Endpoint:** `POST /open/v1/GetEtcGantry`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| page_info | object | Pagination parameters |
| start_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response** 

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Gantry information result |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Gantry information list |
| page_info | object | Pagination information |

**List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| actual_amount | integer | Cumulative actual amount (cents) |
| billing_mileage | integer | Cumulative billing mileage (meters) |
| card_balance | integer | Card balance (cents) |
| card_type | integer | Card type:<br>0x17-account card<br>0x16-prepaid card |
| etcat | integer | Transaction antenna type: 0xa3-closed gantry antenna |
| gantry_number | string | Gantry number |
| lpn | string | License plate number |
| obu_status | integer | OBU status:<br>0x00-OK<br>Bit0-battery low=1<br>Bit1-card not present=1 |
| pass_time | string | Passage time |
| receivable_amount | integer | Cumulative receivable amount (cents) |
| status_flag | integer | Transaction status flag:<br>0x00-OK<br>0x01-ERR |
| transaction_type | integer | Transaction type: 0x80-toll road free flow |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 36. Get ETC-OBU Information
**Endpoint:** `POST /open/v1/EtcObu`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Get OBU result |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| obu_id | integer | OBU ID |

---

## 37. Query ETC-OBU Response Information
**Endpoint:** `POST /open/v1/GetEtcObu`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| obu_id | integer | OBU ID |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | OBU response result |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| contract_num | string | Contract number |
| electricity | integer | Battery level (mV) |
| obu_id | integer | Returned OBU ID |
| obu_mac | string | OBU MAC address |
| obu_sn | string | OBU serial number |
| query_status | integer | Query status: 1-success, others-failure |
| seq | string | Response sequence number |
| version | string | Version number |

---

## 38. Bind Vehicle Information
**Endpoint:** `POST /open/v1/BindVehicleDevice`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| drive_name | string | Driver name |
| drive_phone | string | Driver phone number |
| vehicle_name | string | License plate number |
| shelf_code | string | Vehicle identification number (VIN) |
| vehicle_bind_date | string | Binding time |
| is_update | bool | Whether to update when device already bound to vehicle information (default: false) |
| emergency_contact_phone_1 | string | Emergency contact phone 1 |
| emergency_contact_phone_2 | string | Emergency contact phone 2 |
| emergency_contact_phone_3 | string | Emergency contact phone 3 |
| store_bind | integer | Whether bound to store: 0-do not display store binding, 1-bound to store, 2-not bound to store |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | string | Empty |

---

## 39. Get Account Device ID List
**Endpoint:** `GET /open/v1/GetAccountDeviceList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Account device information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Account device ID list (string array) |
| page_info | object | Pagination information |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 40. Get Road Damage List
**Endpoint:** `POST /open/v1/GetRoadDamageList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| begin_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| device_id | string | Device ID (IMEI) |
| damage_type | array | Road damage types (integer array)<br>(If no parameters are provided, query all road damages by default) |
| map_coord_type | integer | Map coordinate system:<br>0-WGS84 (default)<br>1-BD09 (Baidu)<br>2-GCJ02 (Gaode/Tencent) |
| page_info | object | Pagination parameters |

**Road Damage Enum**

| Code | Description |
| :--- | :--- |
| 400 | Asphalt road - pothole |
| 411 | Asphalt road - alligator cracking |
| 415 | Crack repair |
| 422 | Asphalt road - transverse cracking |
| 423 | Asphalt road - longitudinal cracking |
| 424 | Concrete road - broken slab |
| 425 | Landslide |
| 426 | Debris |
| 427 | Snapshot damage |
| 428 | Asphalt road - block cracking |
| 429 | Water accumulation |
| 430 | Manhole cover height difference |
| 431 | Concrete road - corner break |
| 432 | Hump |
| 433 | Concrete road - line cracking |
| 434 | Concrete road - pothole |
| 435 | Patch |
| 436 | Shoulder damage |
| 437 | Asphalt pavement - loose |
| 438 | Poor greenery maintenance |
| 439 | Road obstacle |
| 440 | Subsidence |
| 441 | Road occupation construction |
| 442 | Fallen tree |
| 443 | Sign - greenery obstruction |
| 444 | Road - bollard - reflective strip damage |
| 445 | Road - separator column damage |
| 446 | Road - separator column - reflective film damage |
| 447 | Crash barrel - damage |
| 448 | Crash barrel - reflective film damage |
| 449 | Municipal guardrail - damage |
| 450 | Road - bollard - damage |
| 451 | Tree painting |
| 452 | Separator column aging |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Road damage information |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Account device list |
| page_info | object | Pagination information |

**List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID |
| province | string | Province name |
| city | string | City name |
| region | string | District name |
| recognition_time | string | Recognition time (format: yyyy-MM-dd HH:mm:ss) |
| image_url | array | Image URLs |
| damage_type | string | Road damage type |
| gps_lat | double | Latitude (WGS84) |
| gps_lon | double | Longitude (WGS84) |
| target_lat | double | Latitude in target coordinate system |
| target_lon | double | Longitude in target coordinate system |
| image_coordinate | array | Image coordinate list |

**Image Coordinate Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| x | integer | Image coordinate x-axis |
| y | integer | Image coordinate y-axis |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 41. Wake Up Device
**Endpoint:** `GET /open/v1/WakeUpDevice`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 42. Get Album List
**Endpoint:** `POST /open/v1/GetAlbumList`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| search_type | string | Search type (default: -1)<br>0-all<br>1-snapshot images<br>2-snapshot videos<br>3-live cloud storage<br>4-driving warning<br>5-vibration alarm<br>6-engine-off snapshot<br>7-SOS<br>8-cloud storage files |
| channel | string | Camera channel number |
| time_type | string | Time type (default: day)<br>day-today<br>week-week<br>month-month<br>year-year |
| event_id | string | Event ID |
| event_type | string | Event type |
| page_info | object | Pagination parameters |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Album information |

**Result Object** 

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Album list |
| page_info | object | Pagination information |

**List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| album_id | string | Album ID |
| thumb_url | string | Thumbnail URL |
| url | string | File URL |
| event_time | string | Event time |
| channel | integer | Camera channel number |
| channel_name | string | Camera name |
| event_id | string | Event ID |
| event_type | integer | Event type |
| event_name | string | Event name |
| file_type | integer | File type: 0-image, 1-video |
| gps_lat | double | GPS latitude (WGS84) |
| gps_lng | double | GPS longitude (WGS84) |
| image_list | array | Image list |
| video_list | array | Video list |
| city | string | City |
| create_time | string | Creation time |
| update_time | string | Update time |

**Image List & Video List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| url | string | File URL |
| thumb_url | string | Thumbnail URL |
| timestamp | string | Timestamp |
| channel | string | Camera channel number |
| channel_name | string | Camera name |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 43. Delete Album File
**Endpoint:** `POST /open/v1/DelAlbumFile`


**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| album_id | array | Album IDs (integer array) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | string | Result |

---

## 44. Get Address from Coordinates
**Endpoint:** `GET /open/v1/GetOverseasAddress`

**Headers**

| Field | Type | Description |
| :--- | :--- | :--- |
| language | string | zh-cn Chinese, en English |

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| appkey | string | Request APPKEY |
| lat | double | Latitude |
| lng | double | Longitude |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | string | Result |

---

## 45. Get Device Stop Details
**Endpoint:** `POST /open/v1/GetDeviceStopDetail`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| start_time | string | Start time (format: yyyy-MM-dd HH:mm:ss) |
| end_time | string | End time (format: yyyy-MM-dd HH:mm:ss) |
| map_coord_type | integer | Map coordinate system:<br>0-WGS84 (default)<br>1-BD09 (Baidu)<br>2-GCJ02 (Gaode/Tencent) |
| page_info | object | Pagination parameters |

 **Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| page_num | integer | Page number (starts from 1) |
| page_size | integer | Page size |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | array | Device stop details |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| list | array | Device stop details list |
| page_info | object | Pagination information |

**List Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| device_name | string | Device name |
| start_time | string | Stop start time (format: yyyy-MM-dd HH:mm:ss) |
| end_time | string | Stop end time (format: yyyy-MM-dd HH:mm:ss) |
| gps_lat | double | GPS latitude (WGS84) |
| gps_lon | double | GPS longitude (WGS84) |
| target_lat | double | Latitude in target coordinate system |
| target_lon | double | Longitude in target coordinate system |
| duration | integer | Stop duration (minutes) |
| address | string | Stop location |

**Page Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| total | integer | Total record count |

---

## 46. Set Device Event Video Upload Type
**Endpoint:** `GET /open/v1/SetDeviceEventUploadType`


**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| type | string | Upload type:<br>0-disable upload<br>1-upload images<br>2-upload videos<br>3-upload images and videos |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | string | Result |

---

## 47. Update Device Information
**Endpoint:** `POST /open/v1/UpdateDeviceInfo`



**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| device_info | string | Device information (JSON string) |

**Device Info Object**

| Field | Type | Description |
| :--- | :--- | :--- |
| device_name | string | Device name |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | string | Result |

---

## 48. Cut Fuel and Power
**Endpoint:** `POST /open/v1/CutFuelPower`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| switch | integer | 0: restore fuel/power, 1: cut fuel/power |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 49. Check if Package Has Been Claimed
**Endpoint:** `POST /open/v1/ClaimPackage`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |
| result | object | Result |

**Result Object**  

| Field | Type | Description |
| :--- | :--- | :--- |
| is_activated | bool | Whether activated: true-activated, false-not activated |

---

## 50. Format Device SD Card
**Endpoint:** `POST /open/v1/FormatSDCard`

**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |

---

## 51. Set Device Recording Sound
**Endpoint:** `POST /open/v1/SetDeviceRecordSound`


**Parameters**  

| Field | Type | Description |
| :--- | :--- | :--- |
| device_id | string | Device ID (IMEI) |
| record_switch | integer | Recording switch: 0-off, 1-on |

**Response**  

| Field | Type | Description |
| :--- | :--- | :--- |
| error | integer | Error code |
| reason | string | Message |