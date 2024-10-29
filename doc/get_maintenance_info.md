## 获取维修结果信息

### 功能介绍

> 该接口主要功能是查询订单的维修结果信息。

### URI

> GET /open/api/v1/get_maintenance_info

### 请求消息

- 请求参数

| 参数             | 是否必填  | 参数类型   | 描述         |
|----------------|-------|--------|------------|
| order_no       | true  | String | 订单号        |
| other_order_no | false | String | 第三方平台售后订单号 |

- 请求示例
  ```json
  {
    "order_no": "BSR23xxxx",
    "other_order_no": "xxxx"
  }
  ```

### 响应消息

- 响应参数

| 参数                                     | 参数类型            | 描述             |
|----------------------------------------|-----------------|----------------|
  | code                                   | Integer         | 响应结果           |
  | message                                | String          | 响应信息           |
  | data                                   | Array\[Object\] | 返回数据           |
  | &emsp;&emsp;skuCode                    | String          | 产品编码           |
  | &emsp;&emsp;snCode                     | String          | sn             |
  | &emsp;&emsp;status                     | Integer         | 维修结果: 3良品，4不良品 |
  | &emsp;&emsp;totalAmount                | Decimal         | 总金额            |
  | &emsp;&emsp;payAmount                  | Decimal         | 实付金额           |
  | &emsp;&emsp;currency                   | String          | 币种             |
  | &emsp;&emsp;maintenanceDetails         | Array\[Object\] | 维修详情列表         |
  | &emsp;&emsp;&emsp;&emsp;description    | String          | 维修详情描述         |
  | &emsp;&emsp;&emsp;&emsp;attachmentList | Array           | 附件列表           |
  | &emsp;&emsp;partDetails                | Array\[Object\] | 维修消耗物料详情列表     |
  | &emsp;&emsp;&emsp;&emsp;type           | Integer         | 操作类型：1维修 2替换   |
  | &emsp;&emsp;&emsp;&emsp;totalPrice     | String          | 总价             |
  | &emsp;&emsp;&emsp;&emsp;num            | String          | 数量             |
  | &emsp;&emsp;&emsp;&emsp;skuCode        | String          | 物料编码           |
  | &emsp;&emsp;&emsp;&emsp;description    | String          | 故障描述           |
  | &emsp;&emsp;&emsp;&emsp;newSn          | String          | 新部件的SN         |
  | &emsp;&emsp;&emsp;&emsp;oldSn          | String          | 旧部件的SN         |


- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": [
      {
        "skuCode": "RP_S50",
        "snCode": "565656",
        "status": 3,
        "totalAmount": 4.3,
        "payAmount": 4.3,
        "currency": "USD",
        "maintenanceDetails": [
          {
            "description": "待维修完成50%",
            "attachmentList": [
              "https://dev.besender.com/files/20210415/1618468065XdXvliSgP9.png",
              "https://dev.besender.com/files/20210415/1618468069bUh4vzqlNu.png"
            ]
          },
          {
            "description": "维修完成100%，已经修好，可以寄回给消费者。",
            "attachmentList": []
          }
        ],
        "partDetails": [
          {
            "type": 2,
            "totalPrice": 2,
            "num": 1,
            "skuCode": "MR_8.02.0054",
            "description": "更换滚刷1个",
            "newSn": "",
            "oldSn": ""
          },
          {
            "type": 2,
            "totalPrice": 2.3,
            "num": 1,
            "skuCode": "MR_9.01.0093",
            "description": "更换电池1个",
            "newSn": "112",
            "oldSn": "332"
          }
        ]
      }
    ]
  }
  ```
