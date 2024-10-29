## 获取产品SKU列表
暂不开放

### 功能介绍

> 该接口功能是获取客户下所有的产品SKU列表。

### URI

> GET /open/api/v1/list_product_sku

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
      |---|---|---|---|
  | status | false | Integer | 产品SKU状态：1可用 2草稿 3审核中 4审核不通过，不填表示获取所有SKU信息 |

- 请求示例
  ```json
  {
    "status": 1
  }

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
        |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Array\[Object\] | 响应详细数据 |
  | &emsp;&emsp;status | Integer | 1可用 2草稿 3审核中 4审核不通过 |
  | &emsp;&emsp;type | Integer | 1全新 2翻新 3质检 4报废 5退件 6物料 7维修 |
  | &emsp;&emsp;sku | String | 产品SKU |
  | &emsp;&emsp;sku_name | String | 产品SKU名称 |
  | &emsp;&emsp;model | String | 型号 |

- 响应示例
  ```json
  {
      "code": 200,
      "message": "",
      "data": [
        {
          "status": 1,
          "type": 6,
          "sku": "MR_B61-9801",
          "sku_name": "电池",
          "model": "A10"
        },
        {
          "status": 1,
          "type": 6,
          "sku": "MR_B61-9801",
          "sku_name": "电池",
          "model": "A10"
        },
        {
          "status": 1,
          "type": 6,
          "sku": "MR_B61-9801",
          "sku_name": "电池",
          "model": "A10"
        }
      ]
  }
  ```
