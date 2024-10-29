## 新增售后服务订单（支持批量服务）

### 功能介绍

> 一、使用BSD回邮单  
> 处理流程：  
> 1、验证用户输入的地址信息是否正确  
> 2、创建回邮label  
> 3、返回创建成功的信息
> 
> 二、不用BSD回邮单  
> 当使用自己的物流寄回BSD服务中心时，需要填写寄回的物流单号。
>
> 三、支持创建"保外"`维修`和`发配件`服务类型的订单，  
> 创建`发配件`服务类型的订单时，需要传递具体的`出库物品信息`。

### URI

> POST /open/api/v1/add_multi_back_order

### 请求消息

- 请求参数

  | 参数                      | 是否必填  | 参数类型 | 描述                                                                                       |
  |---------------------| ---------------------|------------------------------------------------------------------------------------------|---|
  | warehouse_id            | true  | Integer | 服务中心ID（需向BSD管理员要）                                                                        |
  | other_order_no          | false | String | 第三方平台售后订单号                                                                               |
  | old_sn                  | false | String | 产品SN号码                                                                                   |
  | express_no              | false | String | 物流单号，如果填写，则表示用自己的物流服务                                                                    |
  | name                    | true  | String | 用户名称                                                                                     |
  | phone                   | true  | String | 联系电话                                                                                     |
  | email                   | true  | String | 邮箱地址                                                                                     |
  | zip_code                | true  | String | 邮编                                                                                       |
  | country_code            | true  | String | 国家代码，例如：US                                                                               |
  | state_code              | true  | String | 州/省代码                                                                                    |
  | city                    | true  | String | 城市                                                                                       |
  | address_line1           | true  | String | 地址的第一行，最大字符数不超过35，一般填写"街道地址"                                                             |
  | address_line2           | false | String | 地址的第二行，一般填写"门牌号"                                                                         |
  | user_note               | true  | String | 备注                                                                                       |
  | after_sale_type         | true  | Integer | 售后类型：2维修，6退件，12换货，14发配件                                                                  |
  | service_type            | false | Integer | 服务类型：1保内（默认值），2保外                                                                        |
  | upload_images           | false | Array | 附件url地址列表，可以是消费者上报订单时上传的附件，方便工程师收到实物后进行对比排查产品故障                                          |
  | out_info                | false  | Array[Object] | 出库物品信息（当 ***售后类型*** 选择`14发配件`时，该字段信息必填）                                                  |
  | &emsp;&emsp;sku         | true  | String | 物料SKU(仅支持发物料)                                                                            |
  | &emsp;&emsp;sku_type | false | Integer | 类型，如果不带BSD的sku前缀时，需要填写该字段：1全新机 2翻新机 6物料                                                  |
  | &emsp;&emsp;num | true | Integer | 发出数量                                                                                     |
  | carrier_code            | false | String | 物流选择：货运商，如果使用BSD平台的物流服务，该字段必填，目前美国已签约的货运商包括`fedex`/`usps`/`ups`                          |
  | service_code            | false | String | 物流选择：货运服务，如果使用BSD平台的物流服务，该字段必填，详细信息参考[ServiceCode](../README.md#物流方及服务种类信息(ServiceCode)) |
  | buy_way                 | false | String | 购买途径                                                                                     |
  | buy_no                  | false | String | 购买订单号                                                                                    |
  | buy_time                | false | String | 购买日期                                                                                     |
  | safe_time               | false | String | 保修日期                                                                                     |
  | info                    | true  | Array[Object] | 入库产品信息                                                                                   |
  | &emsp;&emsp;sku         | true  | String | 产品SKU，[SKU前缀介绍](../README.md#SKU前缀介绍)                                                    |
  | &emsp;&emsp;num         | true  | Integer | 产品数量                                                                                     |
  | &emsp;&emsp;box_num     | false | Integer | 包装箱号                                                                                     |
  | &emsp;&emsp;old_sn_list | false | Array | 产品SN号码列表                                                                                 |

- 请求示例
  ```json
  {
    "warehouse_id": 6,
    "other_order_no": "XXX-XXX001",
    "old_sn": "OLD_SN",
    "express_no": "",
    "name": "test",
    "phone": "1-332-8774555",
    "email": "test@gmail.com",
    "zip_code": "94117",
    "country_code": "US",
    "state_code": "CA",
    "city": "San Francisco",
    "address_line1": "215 Clayton St",
    "address_line2": "",
    "user_note": "测试订单",
    "after_sale_type": 2,
    "service_type": 1,
    "upload_images": ["https://fixcdn.besender.com/129321.png", "https://fixcdn.besender.com/329321.png"],
    "out_info": [
        {
            "sku": "BC-JG-R00001",
            "num": 1
        },
        {
            "sku": "BC-JG-R00002",
            "num": 1
        }
    ],  
    "carrier_code": "fedex",
    "service_code": "fedex_ground",
    "buy_way": "amazon",
    "buy_no": "",
    "buy_time": "",
    "safe_time": "",
    "info": [
        {
            "box_num":2,
            "sku": "S50",
            "num": 2,
            "old_sn_list": ["1243432", "32482048"]
        },
        {
            "box_num":12,
            "sku": "BC-JG-R00001",
            "num": 2,
            "old_sn_list": ["1243432", "dsfa3332"]
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
          "order_no": "BSRxxxx-xxxx"
      }
  }
  ```
