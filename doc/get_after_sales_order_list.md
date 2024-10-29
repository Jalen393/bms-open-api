## 获取指定时间段内售后订单列表

### 功能介绍

> 该接口主要功能是获取指定时间段内所有的售后订单列表，  
> 售后订单类型包括：维修、退货、换货、发配件、DOA。

### URI

> GET /open/api/v2/get_after_sales_order_list

### 请求消息

- 请求参数

| 参数    | 是否必填  | 参数类型    | 描述                          |
|-------|-------|---------|-----------------------------|
| start | false | String  | 起始时间，例如：2022-01-01 00:00:00 |
| end   | false | String  | 结束时间，例如：2022-01-31 23:59:59 |
| page  | false | Integer | 当前页，默认第一页                   |
| limit | false | Integer | 每页返回的数据记录数，默认为10条，最大值：100   |

- 请求示例
  ```json
  {
    "start": "2022-01-01 00:00:00",
    "end": "2022-01-31 23:59:59"
  }
  ```

### 响应消息

- 响应参数

| 参数                                    | 参数类型            | 描述                                               |
|---------------------------------------|-----------------|--------------------------------------------------|
| code                                  | Integer         | 响应结果                                             |
| message                               | String          | 响应信息                                             |
| data                                  | Array\[Object\] | 返回数据                                             |
| &emsp;&emsp;order_no                  | String          | 全局订单号                                            |
| &emsp;&emsp;warehouse_id              | Integer         | 服务中心ID                                           |
| &emsp;&emsp;warehouse_name            | String          | 服务中心名称                                           |
| &emsp;&emsp;order_type                | Integer         | 订单类型: 1自助报修，2客服报修                                |
| &emsp;&emsp;order_status              | Integer         | 订单状态：[如下表](./get_after_sales_order_list.md#订单状态) |
| &emsp;&emsp;order                     | String          | 产品SKU                                            |
| &emsp;&emsp;sku_name                  | String          | 产品名称                                             |
| &emsp;&emsp;model                     | String          | 产品型号                                             |
| &emsp;&emsp;perfect_num               | Integer         | 良品数量                                             |
| &emsp;&emsp;un_perfect_num            | Integer         | 不良品数量                                            |
| &emsp;&emsp;end_time                  | String          | 完成时间                                             |
| &emsp;&emsp;created_at                | String          | 订单创建时间                                           |
| &emsp;&emsp;parts                     | Array\[Object\] | 物料消耗详情                                           |
| &emsp;&emsp;&emsp;&emsp;materiel_sku  | String          | 物料SKU                                            |
| &emsp;&emsp;&emsp;&emsp;materiel_name | String          | 物料名称                                             |
| &emsp;&emsp;&emsp;&emsp;quantity      | Integer         | 消耗数量                                             |
| &emsp;&emsp;&emsp;&emsp;type          | Integer         | 维修类型：1维修 2替换 3补充                                 |
| meta                                  | Object          | 分页相关元数据                                          |
| &emsp;&emsp;current_page              | Integer         | 当前页码                                             |
| &emsp;&emsp;last_page                 | Integer         | 最后一页页码                                           |
| &emsp;&emsp;per_page                  | Integer         | 每页返回的记录数                                         |
| &emsp;&emsp;total                     | Integer         | 查询结果总记录数                                         |

- 响应示例
  ```json
  {
    "code": 200,
    "message": "Success",
    "data": [
        {
            "warehouse_name": "USCA001",
            "order_no": "BS230622-0001",
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
    ],
    "meta": {
        "current_page": 1,
        "last_page": 75,
        "per_page": 3,
        "total": 225
    }
  }
  ```

### 订单状态

| 数值  | 描述       |
|-----|----------|
| 1   | 待审核      |
| 2   | 客户驳回     |
| 3   | 待支付      |
| 4   | 已取消      |
| 5   | 草稿       |
| 6   | 回邮单创建失败  |
| 7   | 在途       |
| 8   | 仓管驳回     |
| 9   | 已入库      |
| 10  | 开始维修     |
| 11  | 完成维修     |
| 12  | 待报废      |
| 13  | 已报废      |
| 14  | 待发货      |
| 15  | 出库运单创建失败 |
| 16  | 待拣货      |
| 19  | 已发货      |

