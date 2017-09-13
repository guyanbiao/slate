#路径
## 获取路径

> 服务器响应:

```json
{
  average_speed: "2.14",
  begin_at: "2017-09-12 15:59:41",
  end_at: "2017-09-12 15:59:41",
  id: 2395461,
  plate_no: "粤B1L79Q",
  remote_route_id: 2517619,
  total_driving_time: "5分36秒",
  total_gas: 0.23,
  total_millage: 0.2,
}
```
查询以行程开始时间为准，每次返回20条记录，某个页码没有数据返不足20的时候说明这是最后一页

### HTTP Request

`GET /api/obd/routes`

### 参数

字段 | 必须 | 描述| 默认值
--------- | ------- | -----------| -----------
plate_no | 是 |  车牌号 | -
begin_at | 否 |  查找发生在改时间之前的行程 | 请求发生的时刻
page | 否 | 页码| 1

### 响应描述

字段 | 描述
--------- | ------- 
average_speed | 平均时速
begin_at | 行程开始时间
end_at | 行程结束时间
id | 行程ID
total_driving_time | 行程总时长
total_gas | 行程消耗油量(L)
total_millage | 行程总里程

## 获取行程详情

> 服务器响应:

```json
{
  "average_speed": "15.61",
  "begin_at": "2017-09-12 10:48:47",
  "end_at": "2017-09-12 11:01:27",
  "gas_phk": "22.73",
  "highest_speed": 49,
  "obd_meters": 13769,
  "plate_no": "粤B1L79Q",
  "prev_route_id": 2513182,
  "next_route_id": 2513605,
  "total_driving_time": "12分41秒",
  "total_gas": 0.75,
  "total_millage": 3.3,
  "points": [
    {lng: "113.21", lat: "23.11", gcj02_lng: "113.22", gcj02_lat: "23.113"}
  ]
}
```
gcj02_lng, gcj02_lat 是火星坐标, 是用算法粗略计算得到的，需要精确计算火星坐标学要高精度的纠偏数据库，20G左右。lng, lat 是gps 采集的原始坐标，即WSG84

### HTTP Request

`GET /api/obd/routes/:route_id`

### 参数

字段 | 必须 | 描述| 默认值
--------- | ------- | -----------| -----------
route_id | 是 |  行程ID |  即从行程列表接口中得到的路径ID

### 响应描述

字段 | 描述
--------- | ------- 
average_speed | 平均时速(km/h)
begin_at | 行程开始时间
end_at | 行程结束时间
gas_phk | 百公里油耗(L/100km)
highest_speed | 最高时速(km/h)
obd_meters | 仪表盘公里数(km)
prev_route_id | 上一个行程ID
next_route_id | 下一个行程ID
total_driving_time | 行驶时间
total_gas| 总油耗(L)
total_millage | 行程公里数(km)
points | 行程中点的集合，array
points[lng] | 经度
points[lat] | 纬度
points[gcj02_lng] | 火星经度
points[gcj02_lat] | 火星纬度
