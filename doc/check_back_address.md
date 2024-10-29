## 验证邮寄地址

### 功能介绍
> 该接口主要功能是验证用户输入的邮寄地址是否正确，包括电话和邮箱，如果不正确，会给出相应的错误消息提示。
 
### URI
> POST /open/api/v1/check_back_address

### 请求消息
- 请求参数  
  
  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | name | true | String | 用户名 |
  | phone | true | String | 联系电话 |
  | email | true | String | 邮箱地址 |
  | zip_code | true | String | 邮编 |
  | country_code | true | String | 国家代码，例如：US |
  | state_code | true | String | 州/省代码 |
  | city | true | String | 城市 |
  | address_line1 | true | String | 地址的第一行，最大字符数不超过35，一般填写"街道地址" |
  | address_line2 | false | String | 地址的第二行，一般填写"门牌号"     |

- 请求示例
  ```json
  {
    "name": "test",
    "phone": "1-332-8774555",
    "email": "test@gmail.com",
    "country_code":"US",
    "state_code":"CA",
    "city":"San Francisco",
    "address_line1":"215 Clayton St",
    "zip_code":"94117"
  }
  ```

### 响应消息
- 响应参数
  
  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | Object | 校正后的地址信息 |
  | &emsp;&emsp;person_name | String | 用户名 |
  | &emsp;&emsp;phone | String | 联系电话 |
  | &emsp;&emsp;email | String | 邮箱地址 |
  | &emsp;&emsp;zip_code | String | 邮编 |
  | &emsp;&emsp;country_code | String | 国家代码，例如：US |
  | &emsp;&emsp;state_code | String | 州/省代码 |
  | &emsp;&emsp;city | String | 城市 |
  | &emsp;&emsp;address_line1 | String | 地址的第一行，最大字符数不超过35 |
  | &emsp;&emsp;address_line2 | String | 地址的第二行 |
  | &emsp;&emsp;isResidential | Bool | 该地址是否为居住地址 |
  | &emsp;&emsp;is_valid | Bool | 地址是否已验证 |
  
- 响应示例
  ```json
  {
      "code": 200,
      "message": "地址校验通过",
      "data": {
          "country_code": "US",
          "state_code": "CA",
          "city": "San Francisco",
          "person_name": "test",
          "phone": "1-332-8774555",
          "email": "test@gmail.com",
          "address_line1": "215 CLAYTON ST",
          "address_line2": null,
          "isResidential": true,
          "zip_code": "94117",
          "is_valid": true
      }
  }
  ```
