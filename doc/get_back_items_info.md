## 获取寄出的物品信息

### 功能介绍

> 该接口主要功能是查询寄出的物品信息。

### URI

> GET /open/api/v1/get_back_items_info

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
    |---|---|---|---|
  | order_no | true | String | 订单号 |
  | other_order_no | false | String | 第三方平台售后订单号 |

- 请求示例
  ```json
  {
    "order_no": "1026-WH21032xxxx",
    "other_order_no": "xxxx"
  }
  ```

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
    |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Array\[Object\] | 返回数据 |
  | &emsp;&emsp;name | String | 产品名称 |
  | &emsp;&emsp;skuCode | String | 产品编码 |
  | &emsp;&emsp;snCode | Array | sn |
  | &emsp;&emsp;num | String | 数量 |



- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": [
      {
        "name": "S50维修机",
        "skuCode": "RP_S50",
        "snCode": ["xxxxx"],
        "num": 1
      }
    ]
  }
  ```
