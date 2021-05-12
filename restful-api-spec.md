RESTful API Spec
===

## General APIs

**GAPI-01** Login API [[Spec]](#gapi-01-login-api)  
```
[POST] /v1/identity/login
```
**GAPI-02** Me API [[Spec]](#gapi-02-me-api)  
```
[GET] /v1/identity/me
```
**GAPI-11** Add device API [[Spec]](#gapi-11-add-device-api)  
```
[POST] /v1/devices
```
**GAPI-12** List device API [[Spec]](#gapi-12-list-device-api)  
```
[GET] /v1/devices
```
**GAPI-13** View device API [[Spec]](#gapi-13-view-device-api)  
```
[GET] /v1/devices/:device-id
```
**GAPI-14** Update device API [[Spec]](#gapi-14-update-device-api)  
```
[PATCH] /v1/devices/:device-id
```
**GAPI-15** Register device API [[Spec]](#gapi-15-register-device-api)  
```
[POST] /v1/devices/:device-id/register
```
**GAPI-16** Activate device API [[Spec]](#gapi-16-activate-device-api)  
```
[POST] /v1/devices/:device-id/activate
```
**GAPI-17** Inactivate device API [[Spec]](#gapi-17-inactivate-device-api)  
```
[POST] /v1/devices/:device-id/inactivate
```
**GAPI-18** Plug device API [[Spec]](#gapi-18-plug-device-api)  
```
[POST] /v1/devices/:device-id/plug
```
**GAPI-19** Unplug device API [[Spec]](#gapi-19-unplug-device-api)  
```
[POST] /v1/devices/:device-id/unplug
```
**GAPI-21** Control device API [[Spec]](#gapi-21-control-device-api)  
```
[POST] /v1/devices/:device-id/control
```
**GAPI-22** Control multiple devices API [[Spec]](#gapi-22-control-multiple-devices-api)  
```
[POST] /v1/control
```
**GAPI-31** Add tag API [[Spec]](#gapi-31-add-tag-api)
```
[PUT] /v1/tags/:tagName
```
**GAPI-32** Remove tag API [[Spec]](#gapi-32-remove-tag-api)
```
[DELETE] /v1/tags/:tagName
```
**GAPI-33** Get tags API [[Spec]](#gapi-33-get-tags-api)
```
[GET] /v1/tags
```
**GAPI-34** Apply tag on devices API [[Spec]](#gapi-34-apply-tag-on-devices-api)  
```
[POST] /v1/tags/:tagName/apply
```
**GAPI-35** Unapply tag on devices API [[Spec]](#gapi-35-unapply-tag-on-devices-api)
```
[POST] /v1/tags/:tagName/unapply
```
**GAPI-36** Clear tag on all devices API [[Spec]](#gapi-36-clear-tag-on-all-devices-api)
```
[POST] /v1/tags/:tagName/clear
```
**GAPI-41** Connection rate dashboard API [[Spec]](#gapi-41-connection-rate-dashboard-api)
```
[GET] /v1/dashboard/connection
```
**GAPI-51** List device metric record API [[Spec]](#gapi-51-list-device-metric-record-api)
```
[GET] /v1/devices/:device-id/metricRecords
```

Authorization: use a specify API key on request header for authorization.  
```
/* Authorization for users */
Authorization=Bearer token.for.auth
/* Authorization for apps */
Authorization=ApiKey token.for.auth
```

### GAPI-01 Login API
`[POST]` `/v1/identity/login`  
request.header  
```
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
{
  /* 帳號*/
  "username":"test@test.com", // string
  /* 密碼 */
  "password":"12345678", // string
}
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
  /* 資料 */
  "data": {
    /* 存取令牌 */
    "accessToken": "j.w.t"
  },
}
```

### GAPI-02 Me API
`[GET]` `/v1/identity/me`  
request.header  
```
Authorization=Bearer token.for.auth
Content-Type=application/json
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
  /* 資料 */
  "data": {
    /* 識別碼 */
    "id": "53bcac05-9faa-4c11-b1fa-212592342eb2",
    /* 名稱 */
    "name": "Testman",
    /* 帳號*/
    "username": "test@test.com",
    /* 註冊時間 */
    "registeredAt": 1567783326,
    /* 啟用標記 */
    "isActive": true,
  },
}
```

### GAPI-11 Add device API
`[POST]` `/v1/devices`  
request.header  
```
Authorization=ApiKey token.for.auth
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
{
  /* 識別碼 */
  "id": "OR00000000000001", // string
  /* 密碼 */
  "secret": "the-secret", // string
  /* 序列號 */
  "serialNumber": "OR00000000000001", // string
  /* 通訊種類 */
  "connType": "nbiot", // (optional) 'nbiot' | 'lora'
  /* 通訊角色 */
  "connRole": "master", // (optional) 'master' | 'slave'
  /* MCU 版本 */
  "mcuVer": "v1.0", // (optional) null | string
  /* 通訊版本 */
  "connVer": "Ublox v5.06", // (optional) null | string
  /* IMEI 碼 */
  "imei": "490154203237518", // (optional) null | string
  /* IMSI 碼 */
  "imsi": "46697123456789", // (optional) null | string
  /* MSISDN 碼 */
  "msisdn": "886987654321", // (optional) null | string
  /* MAC 位址 */
  "macAddr": "FF:FF:FF:FF:FF:FF", // (optional) null | string
  /* 經緯度 */
  "coordinates": [121.2988393, 24.9931178], // (optional) [longitude as number, latitude as number]
  /* 描述 */
  "description": "桃園市政府前第一棵樹旁", // (optional) null | string
  /* 燈桿 */
  "pole": "pole-01", // (optional) null | string
  /* 燈具瓦數 */
  "lampWatt": 200, // (optional) null | number
}
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
  /* 資料 */
  "data": {
    /* 識別碼 */
    "id": "OR00000000000001", // string
    /* 序列號 */
    "serialNumber": "OR00000000000001", // string
    /* 通訊種類 */
    "connType": "nbiot", // 'nbiot' | 'lora'
    /* 通訊角色 */
    "connRole": "master", // 'master' | 'slave'
    /* MCU 版本 */
    "mcuVer": "v1.0", // null | string
    /* 通訊版本 */
    "connVer": "Ublox v5.06", // null | string
    /* IMEI 碼 */
    "imei": "490154203237518", // null | string
    /* IMSI 碼 */
    "imsi": "46697123456789", // null | string
    /* MSISDN 碼 */
    "msisdn": "886987654321", // null | string
    /* MAC 位址 */
    "macAddr": "FF:FF:FF:FF:FF:FF", // null | string
    /* 經緯度 */
    "coordinates": [121.2988393, 24.9931178], // [longitude as number, latitude as number]
    /* 描述 */
    "description": "桃園市政府前第一棵樹旁", // null | string
    /* 燈桿 */
    "pole": "pole-01", // null | string
    /* 燈具瓦數 */
    "lampWatt": 200, // null | number
    /* 標籤 */
    "tags": [], // string[]
    /* 註冊時間 */
    "registeredAt": null, // null | timestamp as number
    /* 啟用標記 */
    "isActive": true, // boolean
    /* 最近控制時間 */
    "lastCmdTime": null, // null | timestamp as number
    /* 最近資料時間 */
    "lastDataTime": null, // null | timestamp as number
  },
}
```

### GAPI-12 List device API
`[GET]` `/v1/devices`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
request.query  
```
isRegistered=false // (optional) boolean
isActive=false // (optional) boolean
isUntagged=true // (optional) boolean
tags=tag-01,tag-02,tag-03 // (optional)
polygon=[[121.1,25.1],[121.2,25.2],[121.3,25.3],[121.4,25.4],[121.1,25.1]] // (optional)
lastDataTimeBefore=1571043544 (optional) timestamp as number
lastDataTimeAfter=1567512821 (optional) timestamp as number
fields=state,metrics // (optional) '' | 'state' | 'metrics'
pageSize=100 // (optional) number
page=3 // (optional) number
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
  /* 分頁 */
  "paging": {
    "pageSize": 100,
    "page": 3,
    "totalCount": 500,
    "totalPages": 5,
  },
  /* 資料 */
  "data": [
    {
      /* 識別碼 */
      "id": "OR00000000000001", // string
      /* 序列號 */
      "serialNumber": "OR00000000000001", // string
      /* 通訊種類 */
      "connType": "nbiot", // 'nbiot' | 'lora'
      /* 通訊角色 */
      "connRole": "master", // 'master' | 'slave'
      /* MCU 版本 */
      "mcuVer": "v1.0", // null | string
      /* 通訊版本 */
      "connVer": "Ublox v5.06", // null | string
      /* IMEI 碼 */
      "imei": "490154203237518", // null | string
      /* IMSI 碼 */
      "imsi": "46697123456789", // null | string
      /* MSISDN 碼 */
      "msisdn": "886987654321", // null | string
      /* MAC 位址 */
      "macAddr": "FF:FF:FF:FF:FF:FF", // null | string
      /* 經緯度 */
      "coordinates": [121.2988393, 24.9931178], // [longitude as number, latitude as number]
      /* 描述 */
      "description": "桃園市政府前第一棵樹旁", // null | string
      /* 燈桿 */
      "pole": "pole-01", // null | string
      /* 燈具瓦數 */
      "lampWatt": 200, // null | number
      /* 標籤 */
      "tags": ["tagNmae1", "tagName2"], // string[]
      /* 註冊時間 */
      "registeredAt": 1567512821, // null | timestamp as number
      /* 啟用標記 */
      "isActive": false, // boolean
      /* 最近控制時間 */
      "lastCmdTime": 1567512821, // null | timestamp as number
      /* 最近資料時間 */
      "lastDataTime": 1567512821, // null | timestamp as number
      /* 狀態 (show up when request fields includes state) */
      "state": {
        /* 預期狀態 */
        "desired": {
          /* 亮度 */
          "brightness": 100, // % as number
          /* 排程 */
          "schedule": [
            {
              /* 時間 */
              "time": "00:00", // HH:MM as string
              /* 亮度 */
              "brightness": 80, // % as number
            },
          ],
          /* 回報延時 */
          "reportDelay": 300, // seconds as number
          /* 回報間隔 */
          "reportInterval": 600, // seconds as number
        },
        /* 回報狀態 */
        "reported": {
          /* 亮度 */
          "brightness": 100, // null | % as number
          /* 排程 */
          "schedule": [
            {
              /* 時間 */
              "time": "00:00", // HH:MM as string
              /* 亮度 */
              "brightness": 80, // % as number
            },
          ],
          /* 回報延時 */
          "reportDelay": 300, // null | seconds as number
          /* 回報間隔 */
          "reportInterval": 600, // null | seconds as number
        },
      },
      /* 感測值 (show up when request fields includes metrics) */
      "metrics": {
        /* 時間戳記 */
        "timestamp": 1567512821, // timestamp as number
        /* 電壓 */
        "voltage": 219.89, // null | V as number
        /* 電流 */
        "current": 43.938, // null | mA as number
        /* 功率因數 */
        "powerFactor": 0.675, // null | number
        /* 功率 */
        "power": 6.521, // null | W as number
        /* 基地台識別碼 */
        "cellId": "51565945", // null | string
        /* RSSI */
        "rssi": -77, // null | dbm as number
        /* RSRP */
        "rsrp": -98.1, // null | dbm as number
        /* RSRQ */
        "rsrq": -22, // null | db as number
        /* SNR */
        "snr": 37, // null | dB as null | number
        /* 溫度 */
        "temperature": 19.65, // null | Celsius degree as number
        /* 流明 */
        "lumen": 332, // null | L as number
        /* X 軸 */
        "xAxis": -0.031, // null | number
        /* Y 軸 */
        "yAxis": 0.004, // null | number
        /* Z 軸 */
        "zAxis": -0.965, // null | number,
      },
    },
  ],
}
```

### GAPI-13 View device API
`[GET]` `/v1/devices/:device-id`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
request.query
```
fields=state,metrics // (optional) '' | 'state' | 'metrics'
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'NOT_FOUND' | 'FAILED'
  /* 資料 */
  "data": {
    /* 識別碼 */
    "id": "OR00000000000001", // string
    /* 序列號 */
    "serialNumber": "OR00000000000001", // string
    /* 通訊種類 */
    "connType": "nbiot", // 'nbiot' | 'lora'
    /* 通訊角色 */
    "connRole": "master", // 'master' | 'slave'
    /* MCU 版本 */
    "mcuVer": "v1.0", // null | string
    /* 通訊版本 */
    "connVer": "Ublox v5.06", // null | string
    /* IMEI 碼 */
    "imei": "490154203237518", // null | string
    /* IMSI 碼 */
    "imsi": "46697123456789", // null | string
    /* MSISDN 碼 */
    "msisdn": "886987654321", // null | string
    /* MAC 位址 */
    "macAddr": "FF:FF:FF:FF:FF:FF", // null | string
    /* 經緯度 */
    "coordinates": [121.2988393, 24.9931178], // [longitude as number, latitude as number]
    /* 描述 */
    "description": "桃園市政府前第一棵樹旁", // null | string
    /* 燈桿 */
    "pole": "pole-01", // null | string
    /* 燈具瓦數 */
    "lampWatt": 200, // null | number
    /* 標籤 */
    "tags": ["tagNmae1", "tagName2"], // string[]
    /* 註冊時間 */
    "registeredAt": 1567512821, // null | timestamp as number
    /* 啟用標記 */
    "isActive": false, // boolean
    /* 最近控制時間 */
    "lastCmdTime": 1567512821, // null | timestamp as number
    /* 最近資料時間 */
    "lastDataTime": 1567512821, // null | timestamp as number
    /* 狀態 (show up when request fields includes state) */
    "state": {
      /* 預期狀態 */
      "desired": {
        /* 亮度 */
        "brightness": 100, // % as number
        /* 排程 */
        "schedule": [
          {
            /* 時間 */
            "time": "00:00", // HH:MM as string
            /* 亮度 */
            "brightness": 80, // % as number
          },
        ],
        /* 回報延時 */
        "reportDelay": 300, // seconds as number
        /* 回報間隔 */
        "reportInterval": 600, // seconds as number
      },
      /* 回報狀態 */
      "reported": {
        /* 亮度 */
        "brightness": 100, // null | % as number
        /* 排程 */
        "schedule": [
          {
            /* 時間 */
            "time": "00:00", // HH:MM as string
            /* 亮度 */
            "brightness": 80, // % as number
          },
        ],
        /* 回報延時 */
        "reportDelay": 300, // null | seconds as number
        /* 回報間隔 */
        "reportInterval": 600, // null | seconds as number
      },
    },
    /* 感測值 (show up when request fields includes state) */
    "metrics": {
      /* 時間戳記 */
      "timestamp": 1567512821, // timestamp as number
      /* 電壓 */
      "voltage": 219.89, // null | V as number
      /* 電流 */
      "current": 43.938, // null | mA as number
      /* 功率因數 */
      "powerFactor": 0.675, // null | number
      /* 功率 */
      "power": 6.521, // null | W as number
      /* 基地台識別碼 */
      "cellId": "51565945", // null | string
      /* RSSI */
      "rssi": -77, // null | dbm as number
      /* RSRP */
      "rsrp": -98.1, // null | dbm as number
      /* RSRQ */
      "rsrq": -22, // null | db as number
      /* SNR */
      "snr": 37, // null | dB as null | number
      /* 溫度 */
      "temperature": 19.65, // null | Celsius degree as number
      /* 流明 */
      "lumen": 332, // null | L as number
      /* X 軸 */
      "xAxis": -0.031, // null | number
      /* Y 軸 */
      "yAxis": 0.004, // null | number
      /* Z 軸 */
      "zAxis": -0.965, // null | number,
    },
  },
}
```

### GAPI-14 Update device API
`[PATCH]` `/v1/devices/:device-id`  
request.header  
```
Authorization=Bearer token.for.auth
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
{
  /* MCU 版本 */
  "mcuVer": "v1.0", // (optional) null | string
  /* 通訊版本 */
  "connVer": "Ublox v5.06", // (optional) null | string
  /* IMEI 碼 */
  "imei": "490154203237518", // (optional) null | string
  /* IMSI 碼 */
  "imsi": "46697123456789", // (optional) null | string
  /* MSISDN 碼 */
  "msisdn": "886987654321", // (optional) null | string
  /* MAC 位址 */
  "macAddr": "FF:FF:FF:FF:FF:FF", // (optional) null | string
  /* 經緯度 */
  "coordinates": [121.2988393, 24.9931178], // (optional) [longitude as number, latitude as number]
  /* 描述 */
  "description": "桃園市政府前第一棵樹旁", // (optional) null | string
  /* 燈桿 */
  "pole": "pole-01", // (optional) null | string
  /* 燈具瓦數 */
  "lampWatt": 200, // (optional) null | number
}
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
  /* 資料 */
  "data": {
    /* 識別碼 */
    "id": "OR00000000000001", // string
    /* 序列號 */
    "serialNumber": "OR00000000000001", // string
    /* 通訊種類 */
    "connType": "nbiot", // 'nbiot' | 'lora'
    /* 通訊角色 */
    "connRole": "master", // 'master' | 'slave'
    /* MCU 版本 */
    "mcuVer": "v1.0", // null | string
    /* 通訊版本 */
    "connVer": "Ublox v5.06", // null | string
    /* IMEI 碼 */
    "imei": "490154203237518", // null | string
    /* IMSI 碼 */
    "imsi": "46697123456789", // null | string
    /* MSISDN 碼 */
    "msisdn": "886987654321", // null | string
    /* MAC 位址 */
    "macAddr": "FF:FF:FF:FF:FF:FF", // null | string
    /* 經緯度 */
    "coordinates": [121.2988393, 24.9931178], // [longitude as number, latitude as number]
    /* 描述 */
    "description": "桃園市政府前第一棵樹旁", // null | string
    /* 燈桿 */
    "pole": "pole-01", // null | string
    /* 燈具瓦數 */
    "lampWatt": 200, // null | number
    /* 標籤 */
    "tags": ["tagNmae1", "tagName2"], // string[]
    /* 註冊時間 */
    "registeredAt": 1567512821, // null | timestamp as number
    /* 啟用標記 */
    "isActive": false, // boolean
    /* 最近控制時間 */
    "lastCmdTime": 1567512821, // null | timestamp as number
    /* 最近資料時間 */
    "lastDataTime": 1567512821, // null | timestamp as number
  },
}
```

### GAPI-15 Register device API
`[POST]` `/v1/devices/:device-id/register`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-16 Activate device API
`[POST]` `/v1/devices/:device-id/activate`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-17 Inactivate device API
`[POST]` `/v1/devices/:device-id/inactivate`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-18 Plug device API
`[POST]` `/v1/devices/:device-id/plug`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
request.body (JSON)  
```json5
{
  /* 經緯度 */
  "coordinates": [121.2988393, 24.9931178], // [longitude as number, latitude as number]
  /* 描述 */
  "description": "桃園市政府前第一棵樹旁", // null | string
  /* 燈桿 */
  "pole": "pole-01", // string
  /* 燈具瓦數 */
  "lampWatt": 200, // number
}
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-19 Unplug device API
`[POST]` `/v1/devices/:device-id/unplug`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-21 Control device API
`[POST]` `/v1/devices/:device-id/control`
request.header  
```
Authorization=Bearer token.for.auth
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
/* 適用於「調控」控制指令 */
{
  /* 種類 */
  "type": "DIMMING", // 'DIMMING'
  /* 內容 */
  "payload": {
    "brightness": 100, // % as number
  },
}

/* 適用於「設定排程」控制指令 */
{
  /* 種類 */
  "type": "SET_SCHEDULE", // 'SET_SCHEDULE'
  /* 內容 */
  "payload": [
    {
      /* 時間 */
      "time": "00:00", // HH:MM as string
      /* 亮度 */
      "brightness": 80, // % as number
    },
    {
      /* 時間 */
      "time": "01:00", // HH:MM as string
      /* 亮度 */
      "brightness": 90, // % as number
    },
    {
      /* 時間 */
      "time": "02:00", // HH:MM as string
      /* 亮度 */
      "brightness": 100, // % as number
    },
  ],
}

/* 適用於「重新啟動」控制指令 */
{
  /* 種類 */
  "type": "REBOOT", // 'REBOOT'
}

/* 適用於「立即回報」控制指令 */
{
  /* 種類 */
  "type": "REPORT", // 'REPORT'
}

/* 適用於「設定回報延時」控制指令 */
{
  /* 種類 */
  "type": "SET_REPORT_DELAY", // 'SET_REPORT_DELAY'
  /* 內容 */
  "payload": 300, // seconds as number
}

/* 適用於「設定回報間隔」控制指令 */
{
  /* 種類 */
  "type": "SET_REPORT_INTERVAL", // 'SET_REPORT_INTERVAL'
  /* 內容 */
  "payload": 600, // seconds as number
}
```
response.body
```json5
{
  /* 代碼 */
  "code": "ACCEPTED" // 'ACCEPTED' | 'FAILED'
}
```

### GAPI-22 Control multiple devices API
`[POST]` `/v1/control`
request.header  
```
Authorization=Bearer token.for.auth
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
{
  "deviceIds": [],
  "tags": [],

  /* 適用於「調控」控制指令 */
  /* 種類 */
  "type": "DIMMING", // 'DIMMING'
  /* 內容 */
  "payload": {
    "brightness": 100, // % as number
  },

  /* 適用於「設定排程」控制指令 */
  /* 種類 */
  "type": "SET_SCHEDULE", // 'SET_SCHEDULE'
  /* 內容 */
  "payload": [
    {
      /* 時間 */
      "time": "00:00", // HH:MM as string
      /* 亮度 */
      "brightness": 80, // % as number
    },
    {
      /* 時間 */
      "time": "01:00", // HH:MM as string
      /* 亮度 */
      "brightness": 90, // % as number
    },
    {
      /* 時間 */
      "time": "02:00", // HH:MM as string
      /* 亮度 */
      "brightness": 100, // % as number
    },
  ],

  /* 適用於「重新啟動」控制指令 */
  /* 種類 */
  "type": "REBOOT", // 'REBOOT'

  /* 適用於「立即回報」控制指令 */
  /* 種類 */
  "type": "REPORT", // 'REPORT'

  /* 適用於「設定回報延時」控制指令 */
  /* 種類 */
  "type": "SET_REPORT_DELAY", // 'SET_REPORT_DELAY'
  /* 內容 */
  "payload": 300, // seconds as number

  /* 適用於「設定回報間隔」控制指令 */
  /* 種類 */
  "type": "SET_REPORT_INTERVAL", // 'SET_REPORT_INTERVAL'
  /* 內容 */
  "payload": 600, // seconds as number
}
```

### GAPI-31 Add tag API
`[PUT]` `/v1/tags/:tagName`  
request.header  
```
Authorization=ApiKey token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-32 Remove tag API
`[DELETE]` `/v1/tags/:tagName`  
request.header  
```
Authorization=ApiKey token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-33 Get tags API
`[GET]` `/v1/tags`  
request.header  
```
Authorization=ApiKey token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
  "data": ["tag-01", "tag-02"], // string[]
}
```

### GAPI-34 Apply tag on devices API
`[POST]` `/v1/tags/:tagName/apply`  
request.header  
```
Authorization=ApiKey token.for.auth
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
{
  /* 標籤名稱 */
  "deviceIds": ["deviceId-01", "deviceId-02"], // string[]
}
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-35 Unapply tag on devices API
`[POST]` `/v1/tags/:tagName/unapply`  
request.header  
```
Authorization=ApiKey token.for.auth
Content-Type=application/json
Accept=application/json
```
request.body (JSON)  
```json5
{
  /* 標籤名稱 */
  "deviceIds": ["deviceId-01", "deviceId-02"], // string[]
}
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-36 Clear tag on all devices API
`[POST]` `/v1/tags/:tagName/clear`  
request.header  
```
Authorization=ApiKey token.for.auth
Accept=application/json
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'FAILED'
}
```

### GAPI-41 Connection rate Dashboard API
`[GET]` `/v1/dashboard/connection`  
request.header  
```
Authorization=ApiKey token.for.auth
Accept=application/json
```
request.query  
```
tags=tag-01,tag-02,tag-03 // (optional)
isUntagged=true // (optional) boolean
basetime=1571043544 (optional) timestamp as number
```
response.body (JSON)  
```json5
{
  "code": "OK", // 'OK' | 'FAILED'
  "data": {
    "totalCount": 1000,
    "isConnectedCount": 997,
    "rate": 99.70
  }
}
```

### GAPI-51 List device metric record API
`[GET]` `/v1/devices/:device-id/metricRecords`  
request.header  
```
Authorization=Bearer token.for.auth
Accept=application/json
```
request.query
```
before=1571043544 // (optional) timestamp as number
after=1567512821 // (optional) timestamp as number
sort=earliest // (optional) 'earliest' | 'latest'
pageSize=100 // (optional) number
page=3 // (optional) number
```
response.body (JSON)   
```json5
{
  /* 回應代碼 */
  "code": "OK", // 'OK' | 'NOT_FOUND' | 'FAILED'
  /* 分頁 */
  "paging": {
    "pageSize": 100,
    "page": 3,
    "totalCount": 500,
    "totalPages": 5,
  },
  /* 資料 */
  "data": [
    {
      /* 時間戳記 */
      "timestamp": 1567512821, // timestamp as number
      /* 亮度 */
      "brightness": 80, // null | % as number
      /* 電壓 */
      "voltage": 219.89, // null | V as number
      /* 電流 */
      "current": 43.938, // null | mA as number
      /* 功率因數 */
      "powerFactor": 0.675, // null | number
      /* 功率 */
      "power": 6.521, // null | W as number
      /* 基地台識別碼 */
      "cellId": "51565945", // null | string
      /* RSSI */
      "rssi": -77, // null | dbm as number
      /* RSRP */
      "rsrp": -98.1, // null | dbm as number
      /* RSRQ */
      "rsrq": -22, // null | db as number
      /* SNR */
      "snr": 37, // null | dB as null | number
      /* 溫度 */
      "temperature": 19.65, // null | Celsius degree as number
      /* 流明 */
      "lumen": 332, // null | L as number
      /* X 軸 */
      "xAxis": -0.031, // null | number
      /* Y 軸 */
      "yAxis": 0.004, // null | number
      /* Z 軸 */
      "zAxis": -0.965, // null | number,
    }
  ],
}
```


## Hooks (for Everlight only)

**HOOK-01** Device creating hook  
```
[POST] http://your.server/your/path
```
**HOOK-02** Telemetry reporting hook  
```
[POST] http://your.server/your/path
```

Verification: use a signature with HMAC (SHA-1) algorithm on request header for verification.  
```ts
/* Verify signature (example for Node.js) */
import crypto from 'crypto';
function hookHandler(req: HttpRequest, res: HttpResponse) {
  const hmac = crypto.createHmac('sha1', SECRET);
  const digest = hmac.update(req.body).digest('hex');
  if (req.header['X-ORingnet-Signature'] === digest) {
    // The received payload is verified.
  }
}
```

### HOOK-01 Device creating hook
`[POST]` `http://your.server/your/path`  
request.header  
```
X-ORingnet-Signature=signature
Content-Type=application/json
```
request.body (JSON)   
```json5
{
  /* 識別碼 */
  "id": "OR00000000000001", // string
  /* 序列號 */
  "serialNumber": "OR00000000000001", // string
  /* 通訊種類 */
  "connType": "nbiot", // 'nbiot' | 'lora'
  /* 通訊角色 */
  "connRole": "master", // 'master' | 'slave'
  /* MCU 版本 */
  "mcuVer": "v1.0", // null | string
  /* 通訊版本 */
  "connVer": "Ublox v5.06", // null | string
  /* IMEI 碼 */
  "imei": "490154203237518", // null | string
  /* IMSI 碼 */
  "imsi": "46697123456789", // null | string
  /* MSISDN 碼 */
  "msisdn": "886987654321", // null | string
  /* MAC 位址 */
  "macAddr": "FF:FF:FF:FF:FF:FF", // null | string
  /* 經緯度 */
  "coordinates": [121.2988393, 24.9931178], // [longitude as number, latitude as number]
  /* 描述 */
  "description": "桃園市政府前第一棵樹旁", // null | string
  /* 燈桿 */
  "pole": "pole-01", // null | string
  /* 燈具瓦數 */
  "lampWatt": 200, // null | number
  /* 標籤 */
  "tags": [], // string[]
  /* 註冊時間 */
  "registeredAt": 1567512821, // null | timestamp as number
  /* 啟用標記 */
  "isActive": true, // boolean
}
```

### HOOK-02 Telemetry reporting hook
`[POST]` `http://your.server/your/path`  
request.header  
```
X-ORingnet-Signature=signature
Content-Type=application/json
```
request.body (JSON)  
```json5
{
  /* 裝置 */
  "device": {
    /* 識別碼 */
    "id": "OR00000000000001", // string
  },
  /* 時間 */
  "time": 1564469672, // UNIX timestamp as number
  /* 感測值 */
  "metrics": {
    /* 亮度 */
    "brightness": 80, // null | % as number
    /* 電壓 */
    "voltage": 219.89, // null | V as number
    /* 電流 */
    "current": 43.938, // null | mA as number
    /* 功率因數 */
    "powerFactor": 0.675, // null | number
    /* 功率 */
    "power": 6.521, // null | W as number
    /* 基地台識別碼 */
    "cellId": "51565945", // null | string
    /* RSSI */
    "rssi": -77, // null | dbm as number
    /* RSRP */
    "rsrp": -98.1, // null | dbm as number
    /* RSRQ */
    "rsrq": -22, // null | db as number
    /* SNR */
    "snr": 37, // null | dB as null | number
    /* 溫度 */
    "temperature": 19.65, // null | Celsius degree as number
    /* 流明 */
    "lumen": 332, // null | L as number
    /* X 軸 */
    "xAxis": -0.031, // null | number
    /* Y 軸 */
    "yAxis": 0.004, // null | number
    /* Z 軸 */
    "zAxis": -0.965, // null | number
  },
}
```
