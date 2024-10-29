## 获取订单详细进度信息

### 功能介绍

> 该接口主要功能是获取售后单每个节点的进度信息。

### URI

> GET /open/api/v1/get_progress_details

### 请求消息

- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | search | true | String | 查询参数，支持输入BSD平台订单号、第三方订单号、物流单号 |

- 请求示例
  ```json
  {
    "search": "1026-WH21032xxxx"
  }
  ```

### 响应消息

- 响应参数

  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Object | 返回数据 |
  | &emsp;order_no | String | BSD全局订单号 |
  | &emsp;warehouse_name | String | 服务中心名称 |
  | &emsp;country_code | String | 国家代码 |
  | &emsp;in_order_info | Object | 入库信息 |
  | &emsp;&emsp;status | Integer | 入库订单状态: 1在途 2已入库 3驳回 4已上架 5取消 |
  | &emsp;&emsp;order_no | String | 入库订单号 |
  | &emsp;&emsp;express_no | String | 入库物流单号 |
  | &emsp;&emsp;note | String | 入库操作备注（html格式） |
  | &emsp;&emsp;carrier_code | String | 物流服务商 |
  | &emsp;&emsp;service_code | String | 物流服务类型 |
  | &emsp;&emsp;tracking_url | String | 物流状态追踪链接 |
  | &emsp;&emsp;created_at | String | 创建时间 |
  | &emsp;&emsp;in_time | String | 入库时间 |
  | &emsp;after_sale_info | Array\[Object\] | 售后信息 |
  | &emsp;&emsp;status | Integer | 售后订单状态：1新订单 2进行中 3已完成 4已出库 5驳回 6异常 |
  | &emsp;&emsp;order_no | String | 售后订单号 |
  | &emsp;&emsp;type | Integer | 售后类型：1故障检测，2维修，3质检，4质检转翻新，5翻新，6退件转翻新，8全新, 9退件认领, 11报废, 12换货 |
  | &emsp;&emsp;result | Integer | 检测或维修结果：1可维修，2不可维修，3良品，4不良品 |
  | &emsp;&emsp;sale_log | Array\[Object\] | 售后检测或维修描述信息 |
  | &emsp;&emsp;&emsp;status | Integer | 售后进度状态：1新订单 2已分配 3进行中 4已完成 5已出库 6驳回 7待审核 8审核 |
  | &emsp;&emsp;&emsp;description | String | 售后进度描述 |
  | &emsp;&emsp;&emsp;attachment | Array | 附件信息 |
  | &emsp;&emsp;&emsp;created_at | String | 创建时间 |
  | &emsp;&emsp;sale_part | Array\[Object\] | 维修耗材信息 |
  | &emsp;&emsp;&emsp;cn_name | String | 中文名称 |
  | &emsp;&emsp;&emsp;en_name | String | 英文名称 |
  | &emsp;&emsp;&emsp;type | Integer | 操作类型：1维修 2替换 |
  | &emsp;&emsp;&emsp;num | Integer | 消耗数量 |
  | &emsp;&emsp;&emsp;error_desc | String | 故障描述 |
  | &emsp;out_order_info | Object | 出库信息 |
  | &emsp;&emsp;status | Integer | 出库订单状态: 1待发货 2已发货 3驳回 4取消 |
  | &emsp;&emsp;order_no | String | 出库订单号 |
  | &emsp;&emsp;express_no | String | 出库物流单号 |
  | &emsp;&emsp;note | String | 出库操作备注（html格式） |
  | &emsp;&emsp;carrier_code | String | 物流服务商 |
  | &emsp;&emsp;service_code | String | 物流服务类型 |
  | &emsp;&emsp;tracking_url | String | 物流状态追踪链接 |
  | &emsp;&emsp;created_at | String | 创建时间 |
  | &emsp;&emsp;out_time | String | 出库时间 |


- 响应示例
  ```json
  {
    "code": 200,
    "message": "success",
    "data": {
      "order_no": "39fcbb81-cfd1-77ce-d2de-7c405658f06b",
      "warehouse_name": "USCA001",
      "country_code": "US",
      "in_order_info": {
        "status": 2,
        "order_no": "1026-WH2105261356",
        "express_no": "1Z004A100394100936",
        "note": "<p>已入库，拍照如下：</p><p><img src=\"http://dev.besender.com/images/20210526/1622016349GPFu637dde.png\"></p>",
        "carrier_code": "ups",
        "service_code": "ups_ground",
        "tracking_url": "http://wwwapps.ups.com/WebTracking/track?HTMLVersion=5.0&loc=en_US&Requester=UPSHome&WBPM_lid=homepage%2Fct1.html_pnl_trk&track.x=Track&trackNums=1Z004A100394100936",
        "created_at": "2021-05-26 15:40:16",
        "in_time": "2021-05-26 16:05:56"
      },
      "after_sale_info": [
        {
          "status": 4,
          "order_no": "1026-RPQ2105261223",
          "type": 1,
          "result": 1,
          "sale_log": [
            {
              "status": 1,
              "description": "phone not start!",
              "attachment": [],
              "created_at": "2021-05-26 16:05:57"
            },
            {
              "status": 2,
              "description": null,
              "attachment": [],
              "created_at": "2021-05-26 16:06:09"
            },
            {
              "status": 3,
              "description": "开始检测",
              "attachment": [
                "http://dev.besender.com/files/20210526/1622016497CSKdYNOAmX.png"
              ],
              "created_at": "2021-05-26 16:08:18"
            },
            {
              "status": 3,
              "description": "检测完成100%",
              "attachment": [
                "http://dev.besender.com/files/20210526/1622016579sShrVhGjMQ.png",
                "http://dev.besender.com/files/20210526/162201661039mbpAqB5G.png"
              ],
              "created_at": "2021-05-26 16:09:41"
            },
            {
              "status": 4,
              "description": null,
              "attachment": [],
              "created_at": "2021-05-26 16:10:12"
            },
            {
              "status": 5,
              "description": null,
              "attachment": [],
              "created_at": "2021-05-26 16:19:48"
            }
          ],
          "sale_part": []
        },
        {
          "status": 4,
          "order_no": "1026-RP2105261224",
          "type": 2,
          "result": 3,
          "sale_log": [
            {
              "status": 1,
              "description": "phone not start!",
              "attachment": [],
              "created_at": "2021-05-26 16:10:47"
            },
            {
              "status": 2,
              "description": null,
              "attachment": [],
              "created_at": "2021-05-26 16:10:47"
            },
            {
              "status": 3,
              "description": "维修完成，已经修好！",
              "attachment": [
                "http://dev.besender.com/files/20210526/162201661039mbpAqB5G.png"
              ],
              "created_at": "2021-05-26 16:14:21"
            },
            {
              "status": 4,
              "description": null,
              "attachment": [],
              "created_at": "2021-05-26 16:16:27"
            },
            {
              "status": 5,
              "description": null,
              "attachment": [],
              "created_at": "2021-05-26 16:19:48"
            }
          ],
          "sale_part": [
            {
              "cn_name": "部位A",
              "en_name": "pA",
              "type": 2,
              "num": 2,
              "error_desc": "replace"
            }
          ]
        }
      ],
      "out_order_info": {
        "status": 2,
        "order_no": "1026-OUT210526534",
        "express_no": "794635312749",
        "note": "<p>已发出货物</p><p><img src=\"http://dev.besender.com/images/20210526/1622017177sXIO4gGgOf.png\"></p>",
        "carrier_code": "fedex",
        "service_code": "fedex_priority_overnight",
        "tracking_url": "https://www.fedex.com/apps/fedextrack/?action=track&cntry_code=us&trackingnumber=794635312749",
        "created_at": "2021-05-26 16:19:48",
        "out_time": "2021-05-26 16:19:48"
      }
    }
  }
  ```
