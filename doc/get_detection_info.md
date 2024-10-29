## 获取检测结果信息

### 功能介绍

> 该接口主要功能是需要检测的订单对应的检测结果信息，方便用户依照检测信息进行下一步操作。

### URI

> GET /open/api/v1/get_detection_info

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
  | data | Object | 返回数据 |
  | &emsp;&emsp;detectionList | Array\[Object\] | 检测信息列表 |
  | &emsp;&emsp;&emsp;&emsp;skuCode | String | 产品编码 |
  | &emsp;&emsp;&emsp;&emsp;snCode | String | sn |
  | &emsp;&emsp;&emsp;&emsp;status | Integer | 检测结果: 1可维修，2不可维修 |
  | &emsp;&emsp;&emsp;&emsp;details | Array\[Object\] | 检测详情列表 |
  | &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;description | String | 检测详情描述 |
  | &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;attachmentList | Array | 附件列表 |
  | &emsp;&emsp;itemList | Array\[Object\] | 返厂物品信息列表 |
  | &emsp;&emsp;&emsp;&emsp;name | String | 产品名称 |
  | &emsp;&emsp;&emsp;&emsp;skuCode | String | 产品编码 |
  | &emsp;&emsp;&emsp;&emsp;snCode | Array | sn |
  | &emsp;&emsp;&emsp;&emsp;num | String | 数量 |



- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": {
      "detectionList": [
        {
          "skuCode": "RP_S50",
          "snCode": "3333333",
          "status": 3,
          "details": [
            {
              "description": "待检测",
              "attachmentList": [
                "http://dev.besender.com/files/20210415/1618451251VgyZ60789A.png"
              ]
            },
            {
              "description": "检测完成50%",
              "attachmentList": [
                "http://dev.besender.com/files/20210415/1618451454rfebGu2CQm.png"
              ]
            },
            {
              "description": "检测全部完成！",
              "attachmentList": [
                "http://dev.besender.com/files/20210415/16184519945NbpISz20d.png",
                "http://dev.besender.com/files/20210415/1618451997u2txtOF6Sn.png"
              ]
            }
          ]
        }
      ],
      "itemList": [
        {
          "name": "S50维修机",
          "skuCode": "RP_S50",
          "snCode": ["3333333"],
          "num": 1
        }
      ]
    }
  }
  ```
