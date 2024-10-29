## 取消发货订单

### 功能介绍
> 该接口功能是可以取消一条还未出库的发货订单。  
 
### URI
> DELETE /open/api/v1/del_out_order/{order_no}

### 请求消息
- 请求参数  
  
  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | order_no | true | String | BSD平台订单号 |


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
