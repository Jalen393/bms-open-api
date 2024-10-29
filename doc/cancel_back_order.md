## 取消售后服务订单

### 功能介绍
> 该接口功能是可以取消一条还未入库的回邮单，或者取消还未发货的出库单。  
 
### URI
> PUT /open/api/v1/cancel_back_order/{order_no}

### 请求消息
- 请求参数  
  
  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | order_no | true | String | BSD平台订单号 |
  | type | false | Integer | 类型：1-回邮单，2-出库单，不填-由系统自动判断是回邮单还是出库单 |


### 响应消息
- 响应参数
  
  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  
- 响应示例
  ```json
  {
      "code": 200,
      "message": "Success"
  }
  ```
