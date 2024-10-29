### 接口认证方式
> OAuth 2.0授权机制下的Client模式（Client Credentials）

### 简介
> 通过调用该接口获取代表用户身份的access token，为接下来的业务api请求提供身份认证信息，
> access token会过期，默认设置为24小时，过期后需要重新获取有效的access token。

### URI
> POST /open/api/v1/access_token

### 请求消息
- 请求参数

  | 参数 | 是否必填 | 参数类型 | 描述 |
  |---|---|---|---|
  | client_id | true | String | Besender平台申请的客户端ID |
  | client_secret | true | String | Besender平台申请的客户端秘钥 |

- 请求示例
  ```json
  {
    "client_id": 19,
    "client_secret": "cAREfCzucJ8hXXXXXXXXXXXX"
  }
  ```


### 响应消息
- 响应参数

  | 参数 | 参数类型 | 描述 |
  |---|---|---|
  | code | Integer | 响应结果 |
  | message | String | 响应信息 |
  | data | String | 响应详细数据 |
  | &emsp;&emsp;token | Object | token信息 |
  | &emsp;&emsp;&emsp;&emsp;token_type | String | token类型 |
  | &emsp;&emsp;&emsp;&emsp;expires_in | Integer | 有效期，单位：秒 |
  | &emsp;&emsp;&emsp;&emsp;access_token | String | access token信息 |
  | &emsp;&emsp;userInfo | Object | 用户基本信息 |

- 响应示例
  ```json
  {
    "code": 200,
    "data": {
        "token": {
            "token_type": "Bearer",
            "expires_in": 86400,
            "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUXXXXxxxkMWNhOThiMTQyZjE3YjYzYmRjMmZjM2VjNjAxNGQ0ZjQ5OTdjNmNmYTk1NzNmODFlNDMyOTFjMmVjOTliOGY5ZWY1OTMyODYyNmEyIn0.eyJhdWQiOiIxMiIsImp0aSI6IjM2YmJkMWNhOThiMTQyZjE3YjYzYmRjMmZjM2VjNjAxNGQ0ZjQ5OTdjNmNmYTk1NzNmODFlNDMyOTFjMmVjOTliOGY5ZWY1OTMyODYyNmEyIiwiaWF0IjoxNjE3Nzg5MTI2LCJuYmYiOjE2MTc3ODkxMjYsImV4cCI6MTYxNzg3NTUyNiwic3ViIjoiMiIsInNjb3BlcyI6W119.O9SYayuLuldZcpPW4pf73gkOEGgER_g966incDG2mt9lJk_kFRjHYIFXFjKEHpH-LFOyvLVymadM-7DNkQQzBR3c0tiCEXfNhsh-YiaQjSiFlYZ_Ze9RS152R4F5aBqQaJ8ajKITDcjp9OolvzLxhTC1G8rIYfQ6WzWY0vRvDy6gR7sGUzByTOV_12LkDB6V1eDZ3ottOpMc-LDz3y9lkGLK6yDSdRXS-kZCePCcKUSfljxNDde0qOPyEEFcGJx6ezYTnb11Mf12f6k8VcOCJ627lrC4cU9uCRX4H_hvBSKl_Lq_nGeEQgsnQ0CEVEb4mIYNxyiytRGExdxIPvKr8HirGrtTAh20mnpoNyeajHpJT15zcxc-MLZ_FfrceFt84Y4yyTstmVmb4DQooXuwO9vj0neWCksk0wkNlsTqmCgpwV30Z4fhGHnLCZRAm-3-Sn3gUvL3OeaIS-vi9VAEb-wDAWY1L5EzI3K4DqMAVRJsiWKacFsWLDCauy0Z_oxMo-Oz_uu1Fz313Scx_cehvKV19xMJDmv6YFrE3CokwTOTnpO6Iu89tqBihbfoha16gWzdpRrLrfy9A8mKF2-77U8c6E_s1qC_yk0Qp68cvP30-wfUYlBgwrfBJrQqtgn2QeXxktBrOifpHa-B2R3QP47I0RyA8ebtg0wHUMY7wHA"
        },
        "userInfo": {
            "id": 2,
            "account": "test007",
            "score": "461.74970"
        }
    }
  }
  ```


### API调用示例(CURL)
```bash
curl -H "Authorization: Bearer ACCESS_TOKEN" 'http://host.com/api/demo' -H "Content-Type:application/json" -X POST --data '{"code": "test", "name": "测试"}'
```
