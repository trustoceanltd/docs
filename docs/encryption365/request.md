此章节主要介绍 Encryption365 API 接口的交互规范。

### 请求方法
所有的接口都必须采用 HTTP POST 方法进行访问。

### 参数格式
请将所有的请求参数构建为JSON对象进行传递。下面是一个设备注册请求的举例 Request Body：
```json
{
    "password":"your-password",
    "username":"account@exmaple.com",
    "servername": "TestDocAPI"
}
```

### HTTP CODE
无论执行成功或是失败，服务器都会返回 200 状态码。
```js
HTTP Status: 200
```
请记住，Encryption365 API 不会使用 HTTP 状态码来表示请求状态，倘若您接收到的响应状态码不是 200 ，
那么很有可能是您的网络连接出现了问题。

### 响应格式
所有接口响应数据都以 JSON 格式进行返回，下面是一个设备注册请求的响应举例 Response Body：
```json
{
    "result": "success",
    "client_id": "sd2dsss-e4e0-sdffs-2sd2-seceds",
    "access_token": "032b12f8abcba61c02e0b47bf",
    "ip_address": "118.190.214.146",
    "status": "active",
    "created_at": "2021-11-02 14:07:15"
}
```