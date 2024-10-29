## 对外同步信息的数据格式

### 成功取消回邮单信息同步

```json
{
  "assCode": "xxxxx",
  "thirdAssCode": "39fbe70d-78c6-4922-3e46-3688326bcd19"
}
```

### 寄出的物品信息同步

```json
{
  "assCode": "xxxxx",
  "thirdAssCode": "39fbe70d-78c6-4922-3e46-3688326bcd19",
  "note": "<p>ok<img src=\"http:\/\/dev.besender.com\/images\/20210426\/1619421867ldlzDu2YMF.png\"><\/p>",
  "itemList": [
    {
      "name": "S50维修机",
      "skuCode": "RP_S50",
      "snCode": [],
      "num": 1
    }
  ]
}
```

### 仓管入库验收信息同步
```json
{
  "assCode": "xxxxx",
  "thirdAssCode": "39fc1fdc-5520-413c-49c1-7a7fe071534f",
  "note": "<p>ok<img src=\"http:\/\/dev.besender.com\/images\/20210426\/1619421867ldlzDu2YMF.png\"><\/p>",
  "attachmentList": [
    "http://dev.besender.com/files/20210415/1618466339AI9iXmvFXQ.png"
  ],
  "itemList": [
    {
      "name": "TEAT0.0.1",
      "skuCode": "RT_TEAT0.0.1",
      "snCode": [],
      "num": 1
    }
  ]
}
```

### 返厂信息和**换货**/**维修**订单检测结果信息同步

```json
{
  "assCode": "xxxxx",
  "thirdAssCode": "39fbe77f-c0ff-5114-ce1c-ec4dfdd567ff",
  "detectionList": [
    {
      "skuCode": "RP_S50",
      "snCode": "565656",
      "status": 1,
      "details": [
        {
          "description": "待检测！",
          "attachmentList": [
            "http://dev.besender.com/files/20210415/1618466339AI9iXmvFXQ.png"
          ]
        },
        {
          "description": "检测完成60%",
          "attachmentList": [
            "http://dev.besender.com/files/20210415/1618466385nY1Vde509B.png"
          ]
        },
        {
          "description": "检测全部完成，检测结果为可以维修好。",
          "attachmentList": [
            "http://dev.besender.com/files/20210415/1618466423fmeX8Plc36.png",
            "http://dev.besender.com/files/20210415/1618466427XU0xsFekCB.png",
            "http://dev.besender.com/files/20210415/1618466430yevNOPVguC.png"
          ]
        }
      ]
    }
  ],
  "itemList": [
    {
      "name": "S50维修机",
      "skuCode": "RP_S50",
      "snCode": ["565656"],
      "num": 1
    }
  ]
}
```

### 维修结果信息同步

```json
{
  "assCode": "xxxxx",
  "thirdAssCode": "39fbe77f-c0ff-5114-ce1c-ec4dfdd567ff",
  "maintenanceList": [
    {
      "skuCode": "RP_S50",
      "snCode": "565656",
      "status": 3,
      "totalAmount": 4.3,
      "payAmount": 4.3,
      "currency": "USD",
      "maintenanceDetails": [
        {
          "description": "待维修完成50%",
          "attachmentList": [
            "http://dev.besender.com/files/20210415/1618468065XdXvliSgP9.png",
            "http://dev.besender.com/files/20210415/1618468069bUh4vzqlNu.png"
          ]
        },
        {
          "description": "维修完成100%，已经修好，可以寄回给消费者。",
          "attachmentList": [
          ]
        }
      ],
      "partDetails": [
        {
          "type": 2,
          "totalPrice": 2,
          "num": 1,
          "skuCode": "MR_8.02.0054",
          "description": "更换滚刷1个"
        },
        {
          "type": 2,
          "totalPrice": 2.3,
          "num": 1,
          "skuCode": "MR_9.01.0093",
          "description": "更换电池1个"
        }
      ]
    }
  ]
}
```

### 出入库物流信息同步

```json
{
  "assCode": "xxxxx",
  "thirdAssCode": "39fbe77f-c0ff-5114-ce1c-ec4dfdd567ff",
  "type": 1,
  "expressNo": "1Z7V1Y240397237662",
  "expressStatus": 5,
  "trackingUrl": "http://wwwapps.ups.com/WebTracking/track?HTMLVersion=5.0&loc=en_US&Requester=UPSHome&WBPM_lid=homepage%2Fct1.html_pnl_trk&track.x=Track&trackNums=1Z7V1Y240397237662",
  "labelUrl": "https://ezeeship.com/api/ezeeship/label/printLabel?objectId=fbeee0459d9b11eb80168105b4838b56",
  "carrierCode": "ups",
  "serviceCode": "ups_ground",
  "logisticsDetailList": [
    {
      "status": "DELIVERED",
      "statusDetails": "Delivered",
      "country": "US",
      "state": "CA",
      "city": "Montclair",
      "statusTime": "2021-04-13 21:35:28"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "On FedEx vehicle for delivery",
      "country": "US",
      "state": "CA",
      "city": "CITY OF INDUSTRY",
      "statusTime": "2021-04-13 11:31:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "Arrived at FedEx location",
      "country": "US",
      "state": "CA",
      "city": "CITY OF INDUSTRY",
      "statusTime": "2021-04-13 11:28:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "At local FedEx facility",
      "country": "US",
      "state": "CA",
      "city": "CITY OF INDUSTRY",
      "statusTime": "2021-04-13 11:26:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "In transit",
      "country": "US",
      "state": "CA",
      "city": "WALNUT",
      "statusTime": "2021-04-13 10:44:59"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "In transit",
      "country": "US",
      "state": "CA",
      "city": "WALNUT",
      "statusTime": "2021-04-12 19:30:33"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "Departed FedEx location",
      "country": "US",
      "state": "CA",
      "city": "BLOOMINGTON",
      "statusTime": "2021-04-12 05:11:33"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "Arrived at FedEx location",
      "country": "US",
      "state": "CA",
      "city": "BLOOMINGTON",
      "statusTime": "2021-04-11 20:40:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "In transit",
      "country": "US",
      "state": "AZ",
      "city": "WILLCOX",
      "statusTime": "2021-04-11 08:54:03"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "In transit",
      "country": "US",
      "state": "TX",
      "city": "SWEETWATER",
      "statusTime": "2021-04-10 20:47:51"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "Left FedEx origin facility",
      "country": "US",
      "state": "AR",
      "city": "MABELVALE",
      "statusTime": "2021-04-10 08:38:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "Arrived at FedEx location",
      "country": "US",
      "state": "AR",
      "city": "MABELVALE",
      "statusTime": "2021-04-10 01:18:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "In FedEx possession",
      "country": "US",
      "state": "AR",
      "city": "LITTLE ROCK",
      "statusTime": "2021-04-09 20:41:00"
    },
    {
      "status": "TRANSIT",
      "statusDetails": "Picked up",
      "country": "US",
      "state": "AR",
      "city": "MABELVALE",
      "statusTime": "2021-04-09 00:00:00"
    },
    {
      "status": "UNKNOWN",
      "statusDetails": "Shipment information sent to FedEx",
      "country": "US",
      "statusTime": "2021-04-07 06:15:00"
    }
  ]
}
```
