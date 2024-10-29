## 获取发货的物流状态信息

### 功能介绍

> 该接口主要功能是获取发货的物流状态信息和获取物流标签，让用户实时知道当前包裹的物流状态。

### URI

> GET /open/api/v1/get_logistics_status

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
    |---|---|---|---|
  | order_no | true | String | 订单号 |
  | other_order_no | false | String | 第三方平台售后订单号 |
  | type | true | Integer | 类型：1.返厂物流信息，2.寄出物流信息 |

- 请求示例
  ```json
  {
    "type": 2,
    "order_no": "39fbfce8-9a63-0941-eb13-xxxx",
    "other_order_no": "xxxx"
  }
  ```

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述                                                                             |
    |---|--------------------------------------------------------------------------------|---|
  | code | Integer | 响应结果                                                                           |
  | message | String | 响应信息                                                                           |
  | data | Object | Data                                                                           |
  | &emsp;&emsp;express_status | Integer | 物流状态：1.RECENT 2.超时取消 3.异常 4.UNKNOWN 5.DELIVERED 6.TRANSIT 7.FAILURE 8.RETURNED |
  | &emsp;&emsp;express_no | String | 物流单号                                                                           |
  | &emsp;&emsp;tracking_url | String | 物流详细信息查询链接                                                                     |
  | &emsp;&emsp;label_url | String | 物流标签信息链接                                                                       |
  | &emsp;&emsp;carrier_code | String | 物流选择：货运商，目前美国已签约的货运商包括`fedex`/`usps`/`ups`                                     |
  | &emsp;&emsp;service_code | String | 物流选择：货运服务，详细信息参考[ServiceCode](../README.md#物流方及服务种类信息(ServiceCode))            |
  | &emsp;&emsp;tracking_historys | Array\[Object\] | 物流运输详细信息                                                                       |
  | &emsp;&emsp;&emsp;&emsp;status | String | 物流状态                                                                           |
  | &emsp;&emsp;&emsp;&emsp;status_details | String | 物流状态详情                                                                         |
  | &emsp;&emsp;&emsp;&emsp;country | String | 国家                                                                             |
  | &emsp;&emsp;&emsp;&emsp;state | String | 州/省                                                                            |
  | &emsp;&emsp;&emsp;&emsp;city | String | 城市                                                                             |
  | &emsp;&emsp;&emsp;&emsp;status_time | String | 物流状态更新时间                                                                       |


- 响应示例
  ```json
  {
      "code": 200,
      "message": "",
      "data": {
          "express_status": 5,
          "tracking_url": "https://tools.usps.com/go/TrackConfirmAction_input?origTrackNum=9400111969000940000011",
          "express_no": "0257d57ec73b11eaae15c5a7b1d71778",
          "label_url": "https://ezeeship.com/api/ezeeship-api/shipment/printLabel?objectId=0257d57ec73b11eaae15c5a7b1d71778",
          "carrier_code": "usps",
          "service_code": "ups_second_day_air_am",
          "tracking_historys": [
            {
              "status": "DELIVERED",
              "status_details": "Delivered, Front Door/Porch",
              "country": "US",
              "state": "MD",
              "city": "DAVIDSONVILLE",
              "status_time": "2020-12-02 07:29:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "Arrived at Post Office",
              "country": "US",
              "state": "MD",
              "city": "DAVIDSONVILLE",
              "status_time": "2020-12-02 04:17:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "Departed USPS Regional Facility",
              "country": "US",
              "state": "",
              "city": "LINTHICUM HEIGHTS MD DISTRIBUTION CENTER",
              "status_time": "2020-12-01 23:02:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "Arrived at USPS Regional Destination Facility",
              "country": "US",
              "state": "",
              "city": "LINTHICUM HEIGHTS MD DISTRIBUTION CENTER",
              "status_time": "2020-12-01 14:40:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "In Transit to Destination",
              "country": "US",
              "state": "MD",
              "city": "On its way to DAVIDSONVILLE",
              "status_time": "2020-12-01 09:41:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "In Transit to Destination",
              "country": "US",
              "state": "MD",
              "city": "On its way to DAVIDSONVILLE",
              "status_time": "2020-11-30 09:41:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "In Transit to Destination",
              "country": "US",
              "state": "MD",
              "city": "On its way to DAVIDSONVILLE",
              "status_time": "2020-11-29 09:41:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "Arrived at USPS Regional Origin Facility",
              "country": "US",
              "state": "",
              "city": "PHILADELPHIA PA NETWORK DISTRIBUTION CENTER",
              "status_time": "2020-11-28 18:41:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "In Transit to Destination",
              "country": "US",
              "state": "MD",
              "city": "On its way to DAVIDSONVILLE",
              "status_time": "2020-11-28 09:57:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "Departed Post Office",
              "country": "US",
              "state": "PA",
              "city": "ALLENTOWN",
              "status_time": "2020-11-27 21:57:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "USPS picked up item",
              "country": "US",
              "state": "PA",
              "city": "ALLENTOWN",
              "status_time": "2020-11-27 16:23:00"
            },
            {
              "status": "TRANSIT",
              "status_details": "Pre-Shipment Info Sent to USPS, USPS Awaiting Item",
              "country": "",
              "state": "",
              "city": "",
              "status_time": "2020-11-26 00:00:00"
            }
          ]

      }
  }
  ```
