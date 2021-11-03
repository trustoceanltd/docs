创建证书
使用此接口创建一个新的SSL证书订单，并根据响应中的域名验证信息完成域名验证后获得证书。
#### 请求方法
```
POST https://encryption365.trustocean.com/cert/create
```
#### 请求参数
|  参数名称   | 类型  | 必填 | 说明 |
|  ----  | ----  | ----  | ----  |
| client_id  | String | 是 | 从设备注册接口获取 |
| access_token  | String | 是 | 从设备注册接口获取 |
| pid  | Int | 是 | 从产品列表接口获取 |
| csr_code  | String | 是 | 使用您的编程语言内置的OpenSSL函数创建的证书申请信息(CSR)的PEM格式的代码内容 |
| domains  | String | 是 | 英文逗号(,)分隔开的域名\IP地址列表，如:a.com,www.a.com,my.a.com,45.90.90.90 |

#### 响应结构
```json

```