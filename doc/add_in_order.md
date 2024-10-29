## 新增头程或转运入库服务订单

### 功能介绍

> 该接口的功能是客户准备把货物发到BSD仓库前，可以通过该接口创建一条入库服务订单，方便BSD仓库管理员收到货物时根据入库单来清点。  
> 该接口主要用在客户批量发新机或维修物料到BSD仓库，一般用在头程发运或从其他仓库调拨移库到BSD仓库。

### URI

> POST /open/api/v1/add_in_order

### 请求消息

- 请求参数

| 参数 | 是否必填 | 参数类型 | 描述 |
|---|---|---|---|
| other_order_no | false | String | 第三方平台订单号 |
| warehouse_id | true | Integer | 服务中心ID（需向BSD管理员要） |
| arrival_type | true | Integer | 送达方式ID，以最终打包好装运的方式为准，[参考送达方式介绍](#送达方式介绍) |
| inbound_pallet | false | Integer | 入库栈板总数量，当选择非`箱`的送到方式时，需要填写栈板总数量 |
| carrier | false | Integer | 运输方式，1海运 2空运 3快递 4陆运 5铁运 6自提 7清关 |
| express_no | false | String | 物流单号,如果有多个请用英文逗号将物流单号分割开 |
| expect_in_time | false | String | 预计到达时间，例如：2021-11-01 |
| user_note | false | String | 用户备注 |
| name | false | String | 发件人名称 |
| phone | false | String | 发件人联系电话 |
| email | false | String | 发件人邮箱地址 |
| zipcode | false | String | 发件人邮编 |
| country_code | false | String | 发件人所在国家代码，例如：CN |
| state_code | false | String | 发件人所在州/省代码 |
| city | false | String | 发件人所在城市 |
| address | false | String | 发件人详细地址 |
| attachments | false | Array[Object] | 入库附件列表 |
| &emsp;&emsp;file_name | false | String | 附件名称 |
| &emsp;&emsp;file_url | false | String | 附件url地址 |
| service_list | false | Array[Object] | 选择的增值服务 |
| &emsp;&emsp;service_id | false | Integer | 服务项ID |
| packages | true | Array[Object] | 入库物品信息，以**`箱`**为维度进行填写 |
| &emsp;&emsp;quantity | true | Integer | 箱子数量 |
| &emsp;&emsp;remark | false | String | 备注信息 |
| &emsp;&emsp;long | true | Float | 单个箱子的长度 |
| &emsp;&emsp;width | true | Float | 单个箱子的宽度 |
| &emsp;&emsp;height | true | Float | 单个箱子的高度 |
| &emsp;&emsp;distance_unit | true | String | 尺寸单位：厘米(cm)、英寸(in) |
| &emsp;&emsp;weight | true | Float | 单个箱子打包好产品后的重量 |
| &emsp;&emsp;mass_unit | true | String | 重量单位：kg、lb |
| &emsp;&emsp;items | true | Array[Object] | 箱子内所装的产品详情（同一个箱子内可以存在多种产品） |
| &emsp;&emsp;&emsp;&emsp;sku | true | String | 产品SKU |
| &emsp;&emsp;&emsp;&emsp;sku_type | true | Integer | 产品类型（1全新机 2待翻新机 6物料）|
| &emsp;&emsp;&emsp;&emsp;quantity_per_box | true | Integer | 每个箱子装入该产品的数量 |

- 请求示例场景1：
  > 空运10箱物料，每箱装100个物料SKU1，200个物料SKU2。
  ```json
  {
      "other_order_no": "",
      "warehouse_id": 1,
      "arrival_type": 1,
      "inbound_pallet": 0,
      "carrier": 2,
      "express_no": "231625123",
      "expect_in_time": "2021-11-08",
      "user_note": "notes 123456",
      "name": "Jony",
      "phone": "13387723642",
      "email": "test@gmail.com",
      "zipcode": "94117",
      "country_code": "CN",
      "state_code": "",
      "city": "ShenZhen",
      "address": "address 91828",
      "packages": [
          {
              "quantity": 10,
              "remark": "",
              "long": 230,
              "width": 230,
              "height": 200,
              "distance_unit": "in",
              "weight": 300,
              "mass_unit": "lb",
              "items": [
                  {
                      "sku": "SKU1",
                      "sku_type": 6,
                      "quantity_per_box": 100
                  },
                  {
                      "sku": "SKU2",
                      "sku_type": 6,
                      "quantity_per_box": 200
                  }
              ]
          }
      ]
  }
  ```

- 请求示例场景2：

> 每箱装10个SKU1，20个SKU2，这样的箱子共10箱；  
每箱装100个SKU3，这样的箱子共25箱；  
最后打包成了5个`托盘(栈板)`发出。

  ```json
  {
  "other_order_no": "",
  "warehouse_id": 1,
  "arrival_type": 2,
  "inbound_pallet": 5,
  "carrier": 1,
  "express_no": "3245812,231625123",
  "expect_in_time": "2021-11-08",
  "user_note": "notes 123456",
  "name": "Jony",
  "phone": "13387723642",
  "email": "test@gmail.com",
  "zipcode": "94117",
  "country_code": "CN",
  "state_code": "",
  "city": "ShenZhen",
  "address": "address 91828",
  "packages": [
    {
      "quantity": 10,
      "remark": "贵重物品",
      "long": 230,
      "width": 230,
      "height": 200,
      "distance_unit": "in",
      "weight": 300,
      "mass_unit": "lb",
      "items": [
        {
          "sku": "SKU1",
          "sku_type": 1,
          "quantity_per_box": 10
        },
        {
          "sku": "SKU2",
          "sku_type": 6,
          "quantity_per_box": 20
        }
      ]
    },
    {
      "quantity": 25,
      "remark": "贵重物品",
      "long": 230,
      "width": 230,
      "height": 200,
      "distance_unit": "in",
      "weight": 350,
      "mass_unit": "lb",
      "items": [
        {
          "sku": "SKU3",
          "sku_type": 1,
          "quantity_per_box": 100
        }
      ]
    }
  ]
}
  ```

- 请求示例场景3：
  > 每箱装10个新机SKU1，20个物料SKU2，这样的箱子共100箱；  
  > 每箱装100个待翻新机SKU3，这样的箱子共350箱；  
  > 最后打包成了50个`托盘(栈板)`通过`40尺货柜`发出。
  ```json
  {
      "other_order_no": "",
      "warehouse_id": 1,
      "arrival_type": 4,
      "inbound_pallet": 50,
      "carrier": 4,
      "express_no": "231625123",
      "expect_in_time": "2021-11-08",
      "user_note": "notes 123456",
      "name": "Jony",
      "phone": "13387723642",
      "email": "test@gmail.com",
      "zipcode": "94117",
      "country_code": "US",
      "state_code": "CA",
      "city": "",
      "address": "address 91828",
      "packages": [
          {
              "quantity": 100,
              "remark": "贵重物品",
              "long": 230,
              "width": 230,
              "height": 200,
              "distance_unit": "in",
              "weight": 300,
              "mass_unit": "lb",
              "items": [
                  {
                      "sku": "SKU1",
                      "sku_type": 1,
                      "quantity_per_box": 10
                  },
                  {
                      "sku": "SKU2",
                      "sku_type": 6,
                      "quantity_per_box": 20
                  }
              ]
          },
          {
              "quantity": 350,
              "remark": "贵重物品",
              "long": 230,
              "width": 230,
              "height": 200,
              "distance_unit": "in",
              "weight": 350,
              "mass_unit": "lb",
              "items": [
                  {
                      "sku": "SKU3",
                      "sku_type": 2,
                      "quantity_per_box": 100
                  }
              ]
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
| &emsp;&emsp;order_no | String | 入库订单号 |

- 响应示例
  ```json
  {
      "code": 200,
      "data": {
          "order_no": "1026-IB21102921"
      }
  }
  ```

### 获取箱唛标

#### URI

> GET /open/api/v1/download_box_label?order_no=1026-IB21102921

- 请求参数
  > order_no: 订单号，创建订单时返回的数据，如上

### 送达方式介绍

| ID | 送达方式 | 简介 |
|---|---|---|
| 1 | 箱 | - |
| 2 | 托盘(栈板) | - |
| 3 | 20 FT Container(20尺货柜) | 内容积为5.89x2.35x2.38米，配货毛重一般为18吨，体积为28立方米 |
| 4 | 40 FT Container(40尺货柜) | 内容积为12.1x2.34x2.38米，配货毛重一般为22吨，体积为57立方米 |
| 5 | 40 FT HC Container(40尺高柜) | 内容积为12.1x2.34x2.69米配货毛重一般为26吨，体积为67立方米 |
| 6 | 45 FT Container(45尺货柜) | 内容积为13.58x2.34x2.69米，配货毛重一般为29吨，体积为83立方米 |
