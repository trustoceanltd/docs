我们目前并未提供状态码标识错误信息，您可以使用响应体中的 `result` 字段来判断请求是否成功。
当 `result` 的值等于 `error` 时，服务器将同时返回一个额外的 `message`字段以详细说明错误原因。

### 响应结构
下面是一个登录错误的响应举例 Response Body：
```json
{
    "result": "error",
    "message": "账户或密码错误"
}
```