## 新增售后服务订单（单件服务）

### 功能介绍

> 该接口功能是创建**退货**、**换货**、**维修**的售后服务订单。  
> 处理流程：  
> 1、验证用户输入的地址信息是否正确  
> 2、创建回邮label  
> 3、返回创建成功的信息

### URI

> POST /open/api/v1/add_back_order

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | warehouse_id | true | Integer | 服务中心ID（需向BSD管理员要） |
  | other_order_no | false | String | 第三方平台售后订单号 |
  | old_sn | false | String | 产品SN号码 |
  | name | true | String | 用户名称 |
  | phone | true | String | 联系电话 |
  | email | true | String | 邮箱地址 |
  | zip_code | true | String | 邮编 |
  | country_code | true | String | 国家代码，例如：US |
  | state_code | true | String | 州/省代码 |
  | city | true | String | 城市 |
  | address_line1 | true | String | 地址的第一行，最大字符数不超过35 |
  | address_line2 | false | String | 地址的第二行 |
  | user_note | true | String | 备注 |
  | after_sale_type | true | Integer | 售后类型：1故障检测，2维修，6退件，11报废，12换货 |
  | carrier_code | true | String | 物流选择：货运商，目前美国已签约的货运商包括`fedex`/`usps`/`ups` |
  | service_code | true | String | 物流选择：货运服务，详细信息参考[ServiceCode](../README.md#物流方及服务种类信息(ServiceCode)) |
  | sku | true | String | 产品SKU，[SKU前缀介绍](../README.md#SKU前缀介绍) |
  | buy_way | false | String | 购买途径 |
  | buy_no | false | String | 购买订单号 |
  | buy_time | false | String | 购买日期 |
  | safe_time | false | String | 保修日期 |

- 请求示例
  ```json
  {
    "warehouse_id": 6,
    "other_order_no": "XXX-XXX001",
    "old_sn": "xxx001xxx01",
    "name": "test",
    "phone": "1-332-8774555",
    "email": "test@gmail.com",
    "zip_code":"94117",
    "country_code":"US",
    "state_code":"CA",
    "city":"San Francisco",
    "address_line1":"215 Clayton St",
    "address_line2": "",
    "user_note": "测试订单",
    "after_sale_type": 2,
    "carrier_code": "fedex",
    "service_code": "fedex_standard_overnight",
    "sku": "RP_AA10EU128BL04",
    "buy_way": "amazon",
    "buy_no": "",
    "buy_time": "",
    "safe_time": ""
  }
  ```

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Object | 响应详细数据 |
  | &emsp;&emsp;order_no | String | 售后订单号 |

- 响应示例
  ```json
  {
      "code": 200,
      "message": "创建成功",
      "data": {
          "order_no": "39fbfce8-9a63-0941-eb13-xxxx"
      }
  }
  ```
