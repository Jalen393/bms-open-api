## 获取售后单创建结果状态

### 功能介绍

> 该接口主要功能是查询异常创建的售后单是否成功，还可以用来根据第三方平台订单号查询BSD平台订单号。

### URI

> GET /open/api/v1/get_order_status

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | order_no | false | String | BSD订单号 |
  | other_order_no | false | String | 第三方平台售后订单号 |
  *注意：* 参数order_no和other_order_no必填其一


- 请求示例
  ```json
  {
    "order_no": "xxxxxxx",
    "other_order_no": "xxxx"
  }
  ```

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Object | 返回数据 |
  | &emsp;&emsp;order_no | String | bsd平台订单号 |
  | &emsp;&emsp;other_order_no | String | 第三方平台订单号 |
  | &emsp;&emsp;status | Integer | 订单状态：1任务提交成功，2创建中，3创建失败，4创建成功 |
  | &emsp;&emsp;code | Integer | 订单创建结果code，[参考code说明](../README.md#接口返回code说明) |
  | &emsp;&emsp;message | String | 订单创建结果提示信息 |


- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": {
      "order_no": "39fc692e-b212-681d-c165-xxxxx",
      "other_order_no": "xxxxx",
      "status": 4,
      "code": 200,
      "message": "Success"
    }
  }
  ```
