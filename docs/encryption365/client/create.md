设备账户用于认证和签发证书相关的操作的验证，我们推荐您为每个设备单独注册一个账户，这样您可以在不需要使用时，通过WEB控制台将对应的设备账户的Token吊销以停止继续访问证书签发服务。
### 注册新设备
#### 请求方法
```
POST https://encryption365.trustocean.com/client/create
```
#### 请求参数
|  参数名称   | 类型  | 必填 | 说明 |
|  ----  | ----  | ----  | ----  |
| username  | String | 是 | TRUSTOCEAN账户的邮箱地址 |
| password  | String | 是 | TRUSTOCEAN账户的登录密码 |
| servername | String | 是 | 服务器的主机名或设备名称，便于您自己区分 |

#### 响应结构
```json
{
    "result": "success",
    "client_id": "efcbbdff-e4e0-example-s5af-secured",
    "access_token": "032b12f8abcba61c02e0572f476b300",
    "ip_address": "118.190.214.146",
    "status": "active",
    "created_at": "2021-11-02 14:07:15"
}
```
请求Body中的 servername 参数，应该传入服务器的主机名、设备备注名、或其他您能够识别的名字。(PS: 没办法在上面输入解释)
您可能需要将注册获得的以下信息保存在数据库或配置文件中，作为将来调用其他API接口的认证参数：

- client_id
- access_token