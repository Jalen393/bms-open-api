## 更新售后订单状态

### 功能介绍
> 该接口功能是确认**换货**和**维修**售后订单的下一步操作  
 
### URI
> POST /open/api/v1/update_order_status

### 请求消息
- 请求参数  
  
  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | order_no | true | String | 订单号 |
  | other_order_no | false | String | 第三方平台售后订单号 |
  | type | true | Integer | 操作：1同意换货 2拒绝换货 3保内维修 4保外维修 5不维修 6报废 |
  | user_note | false | String | 备注 |
  | info | false | Array[Object] | 同意换货时指定的物品信息 |
  | &emsp;&emsp;sku | false | String | 产品SKU，[SKU前缀介绍](../README.md#SKU前缀介绍) |
  | &emsp;&emsp;sku_num | false | Integer | 发出数量 |
   **注：** `不维修`会把用户的机器原路退回，`同意换货`需要指定给用户换哪些货及对应的数量


- 请求示例
  ```json
  {
    "type": 1,
    "order_no": "xxxT0021",
    "other_order_no": "xxxx",
    "user_note": "xxxx",
    "info": [
      {
        "sku": "NEW_9.01.0075",
        "sku_num": 1
      },
      {
        "sku": "MR_9.01.0093",
        "sku_num": 1
      }
    ]
  }
  ```

### 响应消息
- 响应参数
  
  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | String | 响应详细数据 |
  
- 响应示例
  ```json
  {
      "code": 200,
      "message": "Success",
      "data": ""
  }
  ```
