## 获取产品的故障现象标签

### 功能介绍

> 该接口主要功能是获取产品的故障现象标签列表。

### URI

> GET /open/api/v1/get_product_fault

### 请求消息

- 请求参数

| 参数  | 是否必填  | 参数类型   | 描述       |
|-----|-------|--------|----------|
| sku | true  | String | 产品的SKU编码 |

- 请求示例
  ```json
  {
    "sku": "CP-SH-R00001-00-00"
  }
  ```

### 响应消息

- 响应参数

| 参数                  | 参数类型            | 描述      |
|---------------------|-----------------|---------|
| code                | Integer         | 响应结果    |
| message             | String          | 响应信息    |
| data                | Array\[Object\] | 返回数据    |
| &emsp;&emsp;en_name | String          | 现象标签英文名 |
| &emsp;&emsp;cn_name | String          | 现象标签中文名 |

- 响应示例
  ```json
  {
    "code": 200,
    "message": "Success",
    "data": [
        {
            "en_name": "Run just seconds",
            "cn_name": "运行几秒钟"
        },
        {
            "en_name": "Boot edge brush self-opening",
            "cn_name": "开机边刷自启"
        },
        {
            "en_name": "Error code：40",
            "cn_name": "错误代码：40"
        },
        {
            "en_name": "Error code：42",
            "cn_name": "错误代码：42"
        }
    ]
  }
  ```
