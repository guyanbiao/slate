---
title: OBD接口文档

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - routes

search: true
---

# 概述

每个请求需要包含以下三个请求，下文具体接口不在重复

字段 | 必须 | 描述
--------- | ------- | -----------
appid | 是| appid
timestamps | 是 | UNIX时间戳
sign | 签名| 

timestamps是发起请求时候的

# 设备信息

## 获取车辆主设备信息

> 服务器响应:

```json

{
  "plate_no":"粤B7K01W",
  "obd_meters":24732,
  "fuel_remained":72,
  "battery_voltage":9.941,
  "lng":"113.447022",
  "lat": "23.145117"
}

```

一个车辆可以有多个设备，但只有且只有一个主设备

### HTTP Request

`GET /api/obd/devices/query`

### 参数

字段 | 必须 | 描述
--------- | ------- | -----------
plate_no | 是 |  车牌号


### 响应描述

字段 | 描述
--------- | ------- 
obd_meters | 仪表盘公里数
fuel_remained | 剩余油量(百分比，40 表示 40%)
battery_voltage | 电瓶电压(伏特)
lng | 经度
lat | 纬度

## 获取车辆全部设备

> 服务器响应:

```json
[
  {
    "device_type": "locator"
    "is_main_device": true 
    "plate_no":"粤B7K01W",
    "obd_meters":24732,
    "fuel_remained":72,
    "battery_voltage":9.941,
    "lng":"113.447022",
    "lat": "23.145117"
  }
]
```

### HTTP Request

`GET /api/obd/devices/query_all`

### 参数

字段 | 必须 | 描述
--------- | ------- | -----------
plate_no | 是 |  车牌号


### 响应描述

字段 | 描述
--------- | ------- 
device_type | 设备类型(locator: 定位器, obd: OBD设备)
is_main_device |  主设备表示
imei | 设备唯一表示
obd_meters | 仪表盘公里数
fuel_remained | 剩余油量(百分比，40 表示 40%)
battery_voltage | 电瓶电压(伏特)
lng | 经度
lat | 纬度
