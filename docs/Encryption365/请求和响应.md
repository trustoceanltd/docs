在开始和API进行交互之前，请先阅读此页面的请求说明。以便于API服务器可以正确理解您的参数和行为。
### 请求方法
所有的接口均采用 HTTP POST 方法访问
### 参数格式
将所有的请求参数构建为JSON对象，POST 到对应的API接口即可。下面是一个设备注册请求的Body参数举例：
```json
{
    "password":"your-password",
    "username":"account@exmaple.com",
    "servername": "TestDocAPI"
}
```
### 响应格式
请求发送成功时，HTTP CODE 始终为 200 。且所有请求的响应都以JSON格式进行返回。下面是一个设备注册请求的响应举例 Response Body：
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