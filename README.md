# 开放接口文档

## 介绍

彼森德平台开放接口，供第三方平台以编程的方式对接BSD平台获取相应的数据。

## 接口返回code说明

200表示成功，其他都表示失败，message会给出对应的错误信息。

### 常见错误

| code | message                                           | desc                                                             |
|------|---------------------------------------------------|------------------------------------------------------------------|
| 400  | Validation error.                                 | 请求参数验证不通过，具体错误信息放在data字段中，[格式参考](./README.md#参数验证不通过对应的详细错误信息格式) |
| 410  | after_sale_type in ** order can only be ** or **  | 售后服务类型跟sku类型不匹配                                                  |
| 411  | StateCode error ! Do you want to enter CA?        | 用户地址校验不通过（错误信息不固定）                                               |
| 412  | Please configure currency code first              | BSD管理员还没有设置结算的货币代码                                               |
| 413  | Your USD balance is insufficient, please recharge | 支付币种余额不足                                                         |
| 414  | ****                                              | 创建回邮单失败                                                          |
| 415  | The out order already exists                      | 出库单已经存在不能重复创建                                                    |
| 416  | sku(***) out of stock                             | 库存不足                                                             |
| 417  | order no not found!                               | 订单号不存在                                                           |
| 418  | ** does not exist!                                | sku不存在                                                           |
| 500  | ****                                              | 其他错误                                                             |

#### 参数验证不通过对应的详细错误信息格式

```json
{
  "code": 400,
  "message": "Validation error.",
  "data": {
    "address_line2": [
      "The address line2 may not be greater than 35 characters."
    ],
    "user_note": [
      "The user note field is required."
    ],
    "buy_time": [
      "The buy time is not a valid date."
    ],
    "safe_time": [
      "The safe time is not a valid date."
    ]
  }
}
```

## 接口认证

接口认证采用**OAuth 2.0授权机制**下的Client模式（Client Credentials），具体参考[详细文档](./doc/auth_method.md)

## 对外开放的接口列表

[//]: # (- [新增售后服务订单&#40;单件服务&#41;]&#40;./doc/add_back_order.md&#41;)
- [新增售后服务订单(支持批量服务)](./doc/add_multi_back_order.md)
- [新增出库服务订单](./doc/add_out_order.md)
- [用户地址信息校验](./doc/check_back_address.md)
- [物流轨迹信息查询](./doc/get_logistics_status_2.md)
- [获取产品库存信息列表](./doc/list_stock.md)
- [**换货**和**维修**确认接口](./doc/update_order_status.md)
- [检测结果信息查询](./doc/get_detection_info.md)
- [维修结果信息查询](./doc/get_maintenance_info.md)
- [获取维修订单的全部信息](./doc/get_repair_order_info.md)
- [获取产品的故障现象标签](./doc/get_sku_fault_label.md)
- [仓管入库验收信息查询](./doc/get_in_warehouse_info.md)
- [出库信息查询](./doc/get_out_warehouse_info.md)
- [取消售后服务订单](./doc/cancel_back_order.md)
- [获取售后单创建结果状态](./doc/get_order_status.md)
- [获取订单详细进度信息](./doc/get_progress_details.md)
- [更新退货订单的退款金额](./doc/update_order_refund.md)
- [新增头程或转运入库服务订单](./doc/add_in_order.md)
- [获取头程或转运入库详情](./doc/get_inbound_info.md)
- [新增产品](doc/add_product.md)

### 售后数据报告接口 v1.0

- [获取指定时间段内维修订单结果及物料消耗详情](./doc/get_repair_order_details.md)
- [获取指定时间段内翻新订单结果及物料消耗详情](./doc/get_retread_order_details.md)

### 售后数据报告接口 v2.0

- [获取指定时间段内售后订单列表](./doc/get_after_sales_order_list.md)
- [获取售后订单详情](./doc/get_after_sales_order_detail.md)

## 对外同步的信息列表

- 寄回的物品信息同步
- 寄出的物品信息同步
- 返厂信息和**换货**/**维修**订单检测结果信息同步
- 维修结果信息同步
- 出入库物流信息同步
- 成功取消回邮单信息同步

**[查看具体推送的数据结构](./doc/push_info.md)**

## SKU前缀介绍
> SKU前缀如果不填，系统会自动根据售后类型推算。

| ID | Prefix | Service Name |
|---|---|---|
| 1 | NEW_ | 全新产品 |
| 2 | RV_ | 批量处理 |
| 3 | QT_ | 质检 |
| 4 | SR_ | 报废 |
| 5 | RT_ | 退件 |
| 6 | MR_ | 物料 |
| 7 | RP_ | 维修 |
| 8 | CHA_ | 换货 |

## 物流方及服务种类信息(ServiceCode)

### FedEx

| Code | Service Name |
|---|---|
| fedex_home_delivery | FedEx Home Delivery® |
| fedex_priority_overnight | FedEx Priority Overnight® |
| fedex_standard_overnight | FedEx Standard Overnight® |
| fedex_2_day_am | FedEx 2Day® A.M. |
| fedex_2_day | FedEx 2Day® |
| fedex_express_saver | FedEx Express Saver® |
| fedex_ground | FedEx Ground® |
| fedex_smart_post | FedEx SmartPost(only support single parcel) |

### UPS

| Code | Service Name            |
|---|-------------------------|
| ups_next_day_air_early_am | UPS Next Day Air® Early |
| ups_next_day_air | UPS Next Day Air®       |
| ups_next_day_air_saver | UPS Next Day Air Saver® |
| ups_second_day_air_am | UPS 2nd Day Air AM®     |
| ups_second_day_air | UPS 2nd Day Air®        |
| ups_3_day_select | UPS 3 Day Select®       |
| ups_ground | UPS® Ground（不支持加拿大地区）   |
| ups_standard | UPS® Standard（只支持加拿大地区） |

### USPS

| Code | Service Name |
|---|---|
| usps_first | USPS First Class Mail |
| usps_priority | USPS Priority Mail |
| usps_priority_express | USPS Priority Mail Express |

### SAGAWA（日本地区）

| Code           | Service Name |
|----------------|---|
| express | SAGAWA EXPRESS |

### HANJIN（韩国地区）

| Code           | Service Name |
|----------------|---|
| express | HANJIN EXPRESS |

### GLS（德国地区）

| Code           | Service Name    |
|----------------|-----------------|
| PARCEL | Business Parcel |

### DHL（德国地区）

| Code           | Service Name    |
|----------------|-----------------|
| dhl_parcel | DHL Parcel |
