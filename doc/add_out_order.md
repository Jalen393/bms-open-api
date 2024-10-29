## 新增发货订单

### 功能介绍
> 该接口功能是创建一条新的出库订单，可以用来**只发配件**、**发新机**、或者**发翻新机**。  
> 处理流程：  
> 1、验证用户输入的地址信息是否正确  
> 2、创建出库出库订单  
> 3、返回创建成功的信息
 
### URI
> POST /open/api/v1/add_out_order

### 请求消息
- 请求参数  
  
  | 参数 | 是否必填 | 参数类型 | 描述                                              |
  |---|---|-------------------------------------------------|---|
  | warehouse_id | true | Integer | 服务中心ID（需向BSD管理员要）                               |
  | other_order_no | false | String | 第三方平台售后订单号                                      |
  | old_sn | false | String | 产品SN号码                                          |
  | name | true | String | 用户名称                                            |
  | phone | true | String | 联系电话                                            |
  | email | true | String | 邮箱地址                                            |
  | zip_code | true | String | 邮编                                              |
  | country_code | true | String | 国家代码，例如：US                                      |
  | state_code | true | String | 州/省代码，例如：CA                                     |
  | city | true | String | 城市                                              |
  | address_line1 | true | String | 地址的第一行，最大字符数不超过35，一般填写"街道地址"                               |
  | address_line2 | false | String | 地址的第二行，一般填写"门牌号"                                      |
  | out_note | false | String | 出库发货备注                                          |
  | buy_way | false | String | 购买途径                                            |
  | buy_no | false | String | 购买订单号                                           |
  | buy_time | false | String | 购买日期                                            |
  | safe_time | false | String | 保修日期                                            |
  | signature_service | false | Integer | 签名服务: 2-DIRECT, 3-ADULT                         |
  | insurance | false | Integer | 保险金额                                            |
  | info | true | Array[Object] | 出库物品信息                                          |
  | &emsp;&emsp;sku | true | String | 产品SKU，[SKU前缀介绍](../README.md#SKU前缀介绍)           |
  | &emsp;&emsp;sku_type | false | Integer | 产品类型，如果不带BSD的sku前缀时，需要填写该字段：1全新机 2翻新机 6物料 9翻新物料 |
  | &emsp;&emsp;sku_num | true | Integer | 发出数量                                            |

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
    "out_note": "测试出库订单",
    "signature_service": 0,
    "insurance": 0,
    "info": [
      {
        "sku": "MR_9.01.0075",
        "sku_num": 1
      },
      {
        "sku": "MR_9.01.0093",
        "sku_num": 2
      }
    ]
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
