## 更新退货订单的退款金额

### 功能介绍
> 该接口功能是确认退款金额后，需要通过BSD平台将退款信息更新到第三方ERP平台。  
 
### URI
> POST /open/api/v1/update_order_refund

### 请求消息
- 请求参数  
  
  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | order_no | true | String | 订单号 |
  | other_order_no | false | String | 第三方平台售后订单号 |
  | currency | true | String | 退款金额币种，目前只支持人民币(CNY)、美元(USD)、加元(CAD) |
  | amount | true | Float | 退款金额 |
  | tax_rate | false | Float | 税率%，取值范围：0~100，默认为0 |


- 请求示例
  ```json
  {
    "order_no": "39fbc9a5-c730-2090-5d18-xxxx",
    "other_order_no": "xxxx",
    "currency": "USD",
    "amount": 134.3,
    "tax_rate": 0
  }
  ```

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
