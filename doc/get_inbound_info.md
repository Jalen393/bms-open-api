## 获取头程或转运入库详情

### 功能介绍

> 该接口主要功能是查询头程或转运入库详情。

### URI

> GET /open/api/v1/get_inbound_info

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | order_no | true | String | 头程入库订单号 |

- 请求示例
  ```json
  {
    "order_no": "1026-IB21111888"
  }
  ```

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Object | 返回数据 |
  | &emsp;&emsp;total_boxes | Integer | 总箱数 |
  | &emsp;&emsp;done_boxes | Integer | 仓库已接收箱数 |
  | &emsp;&emsp;request_num | Integer | 产品申请入库总数量 |
  | &emsp;&emsp;confirm_num | Integer | 产品确认入库总数量 |
  | &emsp;&emsp;status | Integer | 订单状态：1草稿 2在途 3入库中 4已完成 5已取消 |
  | &emsp;&emsp;in_start_time | String | 入库开始时间 |
  | &emsp;&emsp;in_end_time | String | 入库结束时间 |
  | &emsp;&emsp;details | Array[Object] | 入库详细信息 |
  | &emsp;&emsp;&emsp;&emsp;sku | String | 产品sku |
  | &emsp;&emsp;&emsp;&emsp;request_num | Integer | 该产品申请入库总数量 |
  | &emsp;&emsp;&emsp;&emsp;confirm_num | Integer | 该产品确认入库总数量 |


- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": {
        "total_boxes": 15,
        "done_boxes": 15,
        "request_num": 1100,
        "confirm_num": 1100,
        "status": 4,
        "in_start_time": "2021-11-18 16:03:31",
        "in_end_time": "2021-11-18 16:04:17",
        "details": [
            {
                "sku": "NEW_CP-YJ-A00010-00-00",
                "request_num": 600,
                "confirm_num": 600
            },
            {
                "sku": "MR_9FWPA0312US",
                "request_num": 500,
                "confirm_num": 500
            }
        ]
    }
  }
  ```
