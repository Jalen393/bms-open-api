## 获取维修结果信息

### 功能介绍

> 该接口主要功能是查询订单的维修信息。

### URI

> GET /open/api/v1/get_repair_order_info

### 请求消息

- 请求参数

| 参数             | 是否必填  | 参数类型   | 描述         |
|----------------|-------|--------|------------|
| order_no       | true  | String | 订单号        |
| other_order_no | false | String | 第三方平台售后订单号 |

- 请求示例
  ```json
  {
    "order_no": "BSR23xxxx",
    "other_order_no": "xxxx"
  }
  ```

### 响应消息

- 响应参数

| 参数                                      | 参数类型            | 描述                                                                                                                    |
|-----------------------------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------|
  | code                                    | Integer         | 响应结果                                                                                                                  |
  | message                                 | String          | 响应信息                                                                                                                  |
  | data                                    | Array\[Object\] | 返回数据                                                                                                                  |
  | &emsp;&emsp;skuCode                     | String          | 产品编码                                                                                                                  |
  | &emsp;&emsp;snCode                      | String          | 实物SN                                                                                                                  |
  | &emsp;&emsp;status                      | Integer         | 订单状态: 1待审核、2客户驳回、3待支付、4已取消、5草稿、6创建失败、7在途、8仓管驳回、9已入库、10开始维修、11完成维修、12待报废、13已报废、14待发货、15运单创建失败、16待拣货、17拣货中、18拣货失败、19已发货 |
  | &emsp;&emsp;orderNo                     | String          | BSD售后ID                                                                                                               |
  | &emsp;&emsp;otherOrderNo                | String          | 云鲸售后ID                                                                                                                |
  | &emsp;&emsp;afterSaleType               | Integer         | 售后类型: 0其他, 1故障检测，2维修，3质检，4质检转翻新，5翻新，6退件转翻新，8全新, 9退件认领, 11报废, 12换货 13退物料 14发配件                                         |
  | &emsp;&emsp;createdAt                   | String          | 建单时间                                                                                                                  |
  | &emsp;&emsp;inboundAt                   | String          | 入厂时间                                                                                                                  |
  | &emsp;&emsp;deliveredAt                 | String          | 物流抵达时间                                                                                                                |
  | &emsp;&emsp;startAt                     | String          | 维修开始时间                                                                                                                |
  | &emsp;&emsp;endAt                       | String          | 维修结束时间                                                                                                                |
  | &emsp;&emsp;outboundAt                  | String          | 出厂时间                                                                                                                  |
  | &emsp;&emsp;outboundExpressNo           | String          | 出库物流单号                                                                                                                |
  | &emsp;&emsp;engineerName                | String          | 维修人                                                                                                                   |
  | &emsp;&emsp;note                        | String          | 备注                                                                                                                    |
  | &emsp;&emsp;attachmentList              | Array           | 部件图片                                                                                                                  |
  | &emsp;&emsp;faultLabelList              | Array\[Object\] | 复现现象标签详情列表                                                                                                            |
  | &emsp;&emsp;&emsp;&emsp;cnName          | String          | 故障名称中文                                                                                                                |
  | &emsp;&emsp;&emsp;&emsp;enName          | String          | 故障名称英文                                                                                                                |
  | &emsp;&emsp;repairMethodList            | Array\[Object\] | 故障标签列表                                                                                                                |
  | &emsp;&emsp;&emsp;&emsp;cnName          | String          | 维修方法中文                                                                                                                |
  | &emsp;&emsp;&emsp;&emsp;enName          | String          | 维修方法英文                                                                                                                |
  | &emsp;&emsp;partDetails                 | Array\[Object\] | 维修消耗物料详情列表                                                                                                            |
  | &emsp;&emsp;&emsp;&emsp;repairType      | Integer         | 维修类型:1维修 2替换 3补充 4消耗                                                                                                  |
  | &emsp;&emsp;&emsp;&emsp;partCode        | String          | 物料料号                                                                                                                  |
  | &emsp;&emsp;&emsp;&emsp;useType         | Integer         | 使用属性 1客户,2消费者                                                                                                         |
  | &emsp;&emsp;&emsp;&emsp;num             | Integer         | 使用数量                                                                                                                  |
  | &emsp;&emsp;&emsp;&emsp;newSn           | Array           | 部件新SN                                                                                                                 |
  | &emsp;&emsp;&emsp;&emsp;oldSn           | Array           | 部件旧SN                                                                                                                 |
  | &emsp;&emsp;serviceCosts                | Decimal         | 劳务费                                                                                                                   |
  | &emsp;&emsp;estInboundShippingCosts     | Decimal         | 预估寄回运费                                                                                                                |
  | &emsp;&emsp;estOutboundShippingCosts    | Decimal         | 预估寄出运费                                                                                                                |
  | &emsp;&emsp;actualInboundShippingCosts  | Decimal         | 实际寄回运费                                                                                                                |
  | &emsp;&emsp;actualOutboundShippingCosts | Decimal         | 实际寄出运费                                                                                                                |
  | &emsp;&emsp;repairNum                   | String          | 维修次数                                                                                                                  |
  | &emsp;&emsp;repairLevel                 | String          | 维修等级                                                                                                                  |
  | &emsp;&emsp;pending_reason              | Integer         | 维修中断原因：1-缺少物料，2-保外待用户支付，3-无法维修待确认，4-维修暂停，5-其他                                                                         |
  | &emsp;&emsp;interruptSku                | String          | 中断SKU                                                                                                                 |
  | &emsp;&emsp;interruptRemark             | String          | 中断备注                                                                                                                  |

- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": [
      {
        "skuCode": "RP_S50",
        "snCode": "565656",
        "status": 3,
        "orderNo": "BSR23xxxx",
        "otherOrderNo": "xxxx",
        "afterSaleType": 2,
        "createdAt": "2023-10-07 13:41:50",
        "inboundAt": "2023-10-07 13:41:50",
        "deliveredAt": "2023-10-07 13:41:50",
        "startAt": "2023-10-07 13:41:50",
        "endAt": "2023-10-07 13:41:50",
        "outboundAt": "2023-10-07 13:41:50",
        "outboundExpressNo": "123456xxxxxx",
        "pending_reason": 1,
        "engineerName": "工程师-刘",
        "note": "维修描述1 | 维修描述2",
        "interruptSku": "B0002_1,B0003",
        "interruptRemark": "中断备注",
        "attachmentList": [
          "https://dev.besender.com/files/20210415/1618468065XdXvliSgP9.png",
          "https://dev.besender.com/files/20210415/1618468069bUh4vzqlNu.png"
        ],
        "repairNum": 0,
        "repairLevel": "L1",
        "faultLabelList": [
          {
            "cnName": "雅迪电动车故障",
            "enName": "yadea_breakdown"
          }
        ],
        "repairMethodList": [
          {
            "cnName": "云鲸-API-维修方法-001",
            "enName": "narwal-API- Maintenance Method -001"
          }
        ],
        "partDetails": [
          {
            "repairType": 2,
            "useType": 2,
            "partCode": "MR_yadea_mirror",
            "num": 1,
            "newSn": [
                "3488787"
             ],
            "oldSn": [
                "43548487"
            ]
          }
        ],
        "serviceCosts": 16.00000,
        "estInboundShippingCosts": 17.00000,
        "estOutboundShippingCosts": 18.00000,
        "actualInboundShippingCosts": 19.00000,
        "actualOutboundShippingCosts": 20.00000
      }
    ]
  }
  ```
