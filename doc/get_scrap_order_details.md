## 获取指定时间段内报废机器详情

### 功能介绍

> 该接口主要功能是获取指定时间段内报废机器详情。

### URI

> GET /open/api/v1/get_scrap_order_details

### 请求消息

- 请求参数

| 参数    | 是否必填  | 参数类型   | 描述                          |
|-------|-------|--------|-----------------------------|
| start | false | String | 起始时间，例如：2022-01-01 00:00:00 |
| end   | false | String | 结束时间，例如：2022-01-31 23:59:59 |

- 请求示例
  ```json
  {
    "start": "2022-01-01 00:00:00",
    "end": "2022-01-31 23:59:59"
  }
  ```

### 响应消息

- 响应参数

| 参数                         | 参数类型            | 描述      |
|----------------------------|-----------------|---------|
| code                       | Integer         | 响应结果    |
| message                    | String          | 响应信息    |
| data                       | Array\[Object\] | 返回数据    |
| &emsp;&emsp;warehouse_name | String          | 服务中心名称  |
| &emsp;&emsp;order_no       | String          | 报废订单号   |
| &emsp;&emsp;sku            | String          | 报废产品SKU |
| &emsp;&emsp;sku_name       | String          | 报废产品名称  |
| &emsp;&emsp;model          | String          | 报废产品型号  |
| &emsp;&emsp;num            | Integer         | 报废数量    |
| &emsp;&emsp;end_time       | String          | 报废时间    |
| &emsp;&emsp;created_at     | String          | 订单创建时间  |


- 响应示例
  ```json
  {
    "code": 200,
    "message": "Success",
    "data": [
        {
            "warehouse_name": "USCA001",
            "order_no": "1026-SC211215213",
            "sku": "RV_S50",
            "sku_name": "S50翻新机",
            "model": "Roborock-S50",
            "num": 1,
            "end_time": "2021-12-24 13:55:01",
            "created_at": "2021-12-15 23:04:43"
        },
        {
            "warehouse_name": "USCA001",
            "order_no": "1026-SC211223217",
            "sku": "RV_S50",
            "sku_name": "S50翻新机",
            "model": "Roborock-S50",
            "num": 1,
            "end_time": "2021-12-24 13:53:30",
            "created_at": "2021-12-23 20:00:07"
        }
    ]
  }
  ```
