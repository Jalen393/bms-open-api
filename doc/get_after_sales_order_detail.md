## 获取指定时间段内维修订单结果及物料消耗详情

### 功能介绍

> 该接口主要功能是获取指定时间段内维修**完成**的订单结果及物料消耗详情。

### URI

> GET /open/api/v1/get_repair_order_details

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

| 参数                                    | 参数类型            | 描述               |
|---------------------------------------|-----------------|------------------|
| code                                  | Integer         | 响应结果             |
| message                               | String          | 响应信息             |
| data                                  | Array\[Object\] | 返回数据             |
| &emsp;&emsp;warehouse_name            | String          | 服务中心名称           |
| &emsp;&emsp;order_no                  | String          | 订单号              |
| &emsp;&emsp;sku                       | String          | 产品SKU            |
| &emsp;&emsp;sku_name                  | String          | 产品名称             |
| &emsp;&emsp;model                     | String          | 产品型号             |
| &emsp;&emsp;num                       | Integer         | 完成数量             |
| &emsp;&emsp;perfect_num               | Integer         | 良品数量             |
| &emsp;&emsp;un_perfect_num            | Integer         | 不良品数量            |
| &emsp;&emsp;end_time                  | String          | 完成时间             |
| &emsp;&emsp;created_at                | String          | 订单创建时间           |
| &emsp;&emsp;parts                     | Array\[Object\] | 物料消耗详情           |
| &emsp;&emsp;&emsp;&emsp;materiel_sku  | String          | 物料SKU            |
| &emsp;&emsp;&emsp;&emsp;materiel_name | String          | 物料名称             |
| &emsp;&emsp;&emsp;&emsp;quantity      | Integer         | 消耗数量             |
| &emsp;&emsp;&emsp;&emsp;type          | Integer         | 维修类型：1维修 2替换 3补充 |


- 响应示例
  ```json
  {
    "code": 200,
    "message": "Success",
    "data": [
        {
            "warehouse_name": "USCA001",
            "order_no": "1026-RP220112245",
            "sku": "RP_S50",
            "sku_name": "S50维修机",
            "model": "Roborock-S50",
            "num": 1,
            "end_time": "2022-01-12 18:15:23",
            "created_at": "2022-01-12 18:10:41",
            "perfect_num": 1,
            "un_perfect_num": 0,
            "parts": [
                {
                    "materiel_sku": "MR_8.02.0060",
                    "materiel_name": "扫地机器人主刷",
                    "quantity": 1,
                    "type": 2
                }
            ]
        },
        {
            "warehouse_name": "USCA001",
            "order_no": "1026-RP220112244",
            "sku": "RP_S50",
            "sku_name": "S50维修机",
            "model": "Roborock-S50",
            "num": 1,
            "end_time": "2022-01-12 17:25:12",
            "created_at": "2022-01-12 17:24:17",
            "perfect_num": 0,
            "un_perfect_num": 1,
            "parts": []
        }
    ]
  }
  ```
