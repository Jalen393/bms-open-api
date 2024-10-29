## 获取产品库存信息

### 功能介绍

> 该接口功能是获取客户下所有的产品在BSD每个服务中心的库存信息列表。

### URI

> GET /open/api/v1/list_stock

### 请求消息

- 请求参数

| 参数       | 是否必填  | 参数类型    | 描述                |
|----------|-------|---------|-------------------|
| sku_list | false | String  | 获取指定sku的库存信息，逗号分隔 |
| page     | false | Integer | 当前页，默认第一页         |
| limit    | false | Integer | 每页返回的数据记录数，默认为10条 |

- 请求示例
  ```json
  {
    "sku_list": "NEW_SKU1,NEW_SKU2"
    "page": 1,
    "limit": 3
  }

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Array\[Object\] | 响应详细数据 |
  | &emsp;&emsp;sku | String | 产品SKU |
  | &emsp;&emsp;sku_type | String | 产品类型：1全新，2翻新，4待报废，5退件 |
  | &emsp;&emsp;name | String | 产品名称 |
  | &emsp;&emsp;model | String | 产品型号 |
  | &emsp;&emsp;warehouse_id | Integer | 服务中心ID |
  | &emsp;&emsp;warehouse_name | String | 服务中心名称 |
  | &emsp;&emsp;warn_num | Integer | 预警库存 |
  | &emsp;&emsp;num | Integer | 当前总库存 |
  | &emsp;&emsp;can_use_num | Integer | 可发货数量 |
  | &emsp;&emsp;ing_num | Integer | 待处理数量 |
  | &emsp;&emsp;total_in_num | Integer | 历史总入库数量 |
  | &emsp;&emsp;total_out_num | Integer | 历史总出库数量 |
  | meta | Object | 分页相关元数据 |
  | &emsp;&emsp;current_page | Integer | 当前页码 |
  | &emsp;&emsp;last_page | Integer | 最后一页页码 |
  | &emsp;&emsp;per_page | Integer | 每页返回的记录数 |
  | &emsp;&emsp;total | Integer | 查询结果总记录数 |


- 响应示例
  ```json
  {
      "code": 200,
      "message": "Success",
      "data": [
          {
            "sku": "S60",
            "sku_type": 1,
            "name": "S60全新机",
            "model": "XXXX-S60",
            "warehouse_id": 1,
            "warehouse_name": "USCA001",
            "warn_num": 10,
            "num": 30,
            "can_use_num": 30,
            "ing_num": 0,
            "total_in_num": 30,
            "total_out_num": 0
        },
        {
            "sku": "S60",
            "sku_type": 5,
            "name": "S60翻新机",
            "model": "XXXX-S60",
            "warehouse_id": 1,
            "warehouse_name": "USCA001",
            "warn_num": 0,
            "num": 30,
            "can_use_num": 30,
            "ing_num": 0,
            "total_in_num": 30,
            "total_out_num": 0
        },
        {
            "sku": "BC-JG-R001",
            "sku_type": 5,
            "name": "机器人",
            "model": "BC-JG-R001",
            "warehouse_id": 1,
            "warehouse_name": "USCA001",
            "warn_num": 1,
            "num": 12,
            "can_use_num": 8,
            "ing_num": 4,
            "total_in_num": 12,
            "total_out_num": 0
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
