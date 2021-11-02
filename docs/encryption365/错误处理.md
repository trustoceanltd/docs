无论何时，只有HTTP请求成功时(Response HTTP Code=200)，才会收到响应，即便是错误响应。
### 响应结构
错误的请求，将会以JSON格式放在响应Body内，并且通过 message 字段详细解释。当遇到错误时，返回的响应体中 status 字段会标注。下面是一个错误响应的举例：
```json
{
    "result": "error",
    "message": "账户或密码错误"
}
```