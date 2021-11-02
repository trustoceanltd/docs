Encryption365 SSL 旨在为您提供完全可控、自定义流程的 SSL 证书签发服务，这项服务完全免费，
并在社区中广受好评。ENC365可帮助您和您的业务实现自动化SSL申请、部署、吊销，并且提供FlextSSL产品，
在同一本证书内增加保护域名、公网IP地址、通配符域名。API接口非常简单，仅需很少的编程即可完成自定义的证书逻辑对接。
您还可以借助这项API能力，将她集成到您的Nginx-Lua环境、Linux环境、Windows环境、主机面板、Varnish环境，
或者利用GoLang开发易用的命令行工具以供社区其他人使用。同时，ENC365还具有下面这些优点：


- 支持 RSA 2048 - 4096 位加密算法
- 支持流行且高性能的 ECC 加密算法
- 在移动端和PC端设备中友好信任
- 支持预先完成域名验证
- 多因素域名验证算法公开
- 仅仅几分钟即可颁发新的证书
- 更重要的是其他社区朋友(您)做出的脚本、插件、工具、WEB界面


## 项目推荐
这是社区目前已实现的客户端、工具，您也可以向我们提交您的实现:
- [Encryption365 SSL 宝塔插件](https://github.com/trustoceanltd/Encryption365_Baota)

基于宝塔面板实现的ENC365客户端，提供证书申请、注册、管理、自动续期。

## 1.请求和响应
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
## 2.错误响应
无论何时，只有HTTP请求成功时(Response HTTP Code=200)，才会收到响应，即便是错误响应。
### 响应结构
错误的请求，将会以JSON格式放在响应Body内，并且通过 message 字段详细解释。当遇到错误时，返回的响应体中 status 字段会标注。下面是一个错误响应的举例：
```json
{
    "result": "error",
    "message": "账户或密码错误"
}
```
## 3.设备账户
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
## 4.认证请求
接下来的所有API访问都需要您提供认证信息， `client_id` 和 `access_token` 。这两个信息都是您通过 设备账户 一节中的说明完成注册并获得的。
这两个认证参数需要作为请求参数，一同放置在请求体的JSON结构中，进行认证。
老话重说，为了便于多设备管理，比如：您有很多台服务器都需要部署ENC365证书服务。我们还是建议您分别为不同的服务器注册不同的账户，
以获得不同`access_token`，这样，您可以在将来通过TRUSTOCEAN的控制台吊销或管理不同设备的访问权限。
## 5.产品列表
此接口帮助你查询目前可订购的ENC365产品，并获得对应下单的产品PID和付费证书的定价。
#### 请求方法
```
POST https://encryption365.trustocean.com/account/products
```
#### 请求参数
|  参数名称   | 类型  | 必填 | 说明 |
|  ----  | ----  | ----  | ----  |
| client_id  | String | 是 | 从设备注册接口获取 |
| access_token  | String | 是 | 从设备注册接口获取 |

#### 响应结构
```json
{
  "result": "success",
  "products": {
    "100": {
      "title": "免费版 SSL 证书",
      "useage": "试用",
      "class": "DV",
      "term": "90天",
      "brand": "环智中诚",
      "logo": "/encryption365/static/img/logo-encryption365.svg",
      "support": false,
      "isFree": true,
      "level": "dv",
      "businessDefault": false,
      "default": true,
      "promote": false,
      "promoText": "促销",
      "recommended": false,
      "period": "quarterly",
      "periodText": "季度",
      "price": {
        "fqdn": 0,
        "wildcard": 0
      },
      "normal_price": {
        "fqdn": 0,
        "wildcard": 0
      }
    },
    "108": {
      "title": "正式版 SSL 证书",
      "useage": "个人/企业",
      "class": "DV",
      "term": "1年",
      "brand": "环智中诚",
      "logo": "/encryption365/static/img/logo-encryption365.svg",
      "support": true,
      "isFree": false,
      "level": "dv",
      "businessDefault": true,
      "default": false,
      "promote": true,
      "promoText": "超实惠",
      "recommended": true,
      "period": "annually",
      "periodText": "年",
      "price": {
        "fqdn": 256,
        "wildcard": 750
      },
      "normal_price": {
        "fqdn": 529,
        "wildcard": 1668
      }
    }
  }
}
```
注意：

1. 接口响应中的 `products` 对象的键将作为后续创建证书接口中的`pid`。比如这里的 `100`和`108`代表两款产品的
`pid`。
2. 根据账户策略的不同，不同账户调用此接口查询到的产品不完全一致。

## 6.创建证书
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
{
    "result": "success",
    "cert_status": "enroll_caprocessing",
    "dcv_info": { 
        "api.trustocean.com": {
            "domain": "api.trustocean.com",
            "emails": [
                "admin@trustocean.com",
                "administrator@trustocean.com",
                "hostmaster@trustocean.com",
                "postmaster@trustocean.com",
                "webmaster@trustocean.com",
                "admin@api.trustocean.com",
                "administrator@api.trustocean.com",
                "hostmaster@api.trustocean.com",
                "postmaster@api.trustocean.com",
                "webmaster@api.trustocean.com"
            ],
            "method": "http",
            "status": "needverification",
            "domainmd5hash": "3e9a833f8eaf35c3f4831263f2fcdf83",
            "isip": false,
            "subdomain": "api",
            "topdomain": "trustocean.com",
            "dns_host": "_b8ee25a34bc5cd1f4d5dc8c20fd4eeb2.api",
            "dns_type": "CNAME",
            "dns_value": "fdadae5fbe8fce33026ffa3de7d27f54.6edc2686259e2ed1d64053aaef156d18.cab202166585.comodoca.com",
            "http_verifylink": "http://api.trustocean.com/.well-known/pki-validation/B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "http_filename": "B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "http_filecontent": "fdadae5fbe8fce33026ffa3de7d27f546edc2686259e2ed1d64053aaef156d18\r\ncomodoca.com\r\ncab202166585",
            "https_verifylink": "https://api.trustocean.com/.well-known/pki-validation/B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "https_filename": "B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "https_filecontent": "fdadae5fbe8fce33026ffa3de7d27f546edc2686259e2ed1d64053aaef156d18\r\ncomodoca.com\r\ncab202166585",
            "email": null
        },
        "trustocean.com": {
            "domain": "trustocean.com",
            "emails": [
                "admin@trustocean.com",
                "administrator@trustocean.com",
                "hostmaster@trustocean.com",
                "postmaster@trustocean.com",
                "webmaster@trustocean.com"
            ],
            "method": "http",
            "status": "needverification",
            "domainmd5hash": "f7781fc6f4b6a396532df4e70aee94e7",
            "isip": false,
            "subdomain": null,
            "topdomain": "trustocean.com",
            "dns_host": "_b8ee25a34bc5cd1f4d5dc8c20fd4eeb2",
            "dns_type": "CNAME",
            "dns_value": "fdadae5fbe8fce33026ffa3de7d27f54.6edc2686259e2ed1d64053aaef156d18.cab202166585.comodoca.com",
            "http_verifylink": "http://trustocean.com/.well-known/pki-validation/B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "http_filename": "B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "http_filecontent": "fdadae5fbe8fce33026ffa3de7d27f546edc2686259e2ed1d64053aaef156d18\r\ncomodoca.com\r\ncab202166585",
            "https_verifylink": "https://trustocean.com/.well-known/pki-validation/B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "https_filename": "B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "https_filecontent": "fdadae5fbe8fce33026ffa3de7d27f546edc2686259e2ed1d64053aaef156d18\r\ncomodoca.com\r\ncab202166585",
            "email": null
        },
        "www.trustocean.com": {
            "domain": "www.trustocean.com",
            "emails": [
                "admin@trustocean.com",
                "administrator@trustocean.com",
                "hostmaster@trustocean.com",
                "postmaster@trustocean.com",
                "webmaster@trustocean.com",
                "admin@www.trustocean.com",
                "administrator@www.trustocean.com",
                "hostmaster@www.trustocean.com",
                "postmaster@www.trustocean.com",
                "webmaster@www.trustocean.com"
            ],
            "method": "http",
            "status": "needverification",
            "domainmd5hash": "b0b56a47b41e0a107f803da38bb017b4",
            "isip": false,
            "subdomain": "www",
            "topdomain": "trustocean.com",
            "dns_host": "_b8ee25a34bc5cd1f4d5dc8c20fd4eeb2.www",
            "dns_type": "CNAME",
            "dns_value": "fdadae5fbe8fce33026ffa3de7d27f54.6edc2686259e2ed1d64053aaef156d18.cab202166585.comodoca.com",
            "http_verifylink": "http://www.trustocean.com/.well-known/pki-validation/B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "http_filename": "B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "http_filecontent": "fdadae5fbe8fce33026ffa3de7d27f546edc2686259e2ed1d64053aaef156d18\r\ncomodoca.com\r\ncab202166585",
            "https_verifylink": "https://www.trustocean.com/.well-known/pki-validation/B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "https_filename": "B8EE25A34BC5CD1F4D5DC8C20FD4EEB2.txt",
            "https_filecontent": "fdadae5fbe8fce33026ffa3de7d27f546edc2686259e2ed1d64053aaef156d18\r\ncomodoca.com\r\ncab202166585",
            "email": null
        }
    },
    "unique_id": "cab202166585",
    "created_at": "2021-11-02 16:25:09",
    "trustocean_id": 52295091,
    "csr_code": "-----BEGIN CERTIFICATE REQUEST-----\r\nMIICwjCCAaoCAQAwfTELMAkGA1UEBhMCQ04xDzANBgNVBAcMBuilv+WuiTEbMBkG\r\nA1UECgwSVFJVU1RPQ0VBTiBMSU1JVEVEMRIwEAYDVQQLDAlJVCDpg6jpl6gxFzAV\r\nBgNVBAMMDnRydXN0b2NlYW4uY29tMRMwEQYDVQQIDApTb21lLVN0YXRlMIIBIjAN\r\nBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArlFy7JzEQfmv9wC4wUtuibLR0mLh\r\nGnm7PJGCgNRGmNs37ZG8CIf8zGnds6aVeUN1S4Loo2YdWrzUhRlKMd0k3B9fxIaE\r\nsVgOtIEEVuwOTviVNLzjf1cf9VvvzflW5TFpBirwgZn+cKhVhgSNTfxIbgpDvyx6\r\ngCVtnswJjX7LGUfX8E+vzzJVePYhUI1UtOQDqLt5lCq2cqNmoTHX009ZtmyjzlZz\r\nDrIFGhxiIFakbl5r6ZVbzVE9PGjbvnKGp32L0JncmIKnE8knh06Dp3/rVncAfs2y\r\n9ZEAC0IqXw3uUh5OqKlhIa6BNdFYYDoqTXZpYtZoI6uMlUuoUFYsJQo4gQIDAQAB\r\noAAwDQYJKoZIhvcNAQELBQADggEBAFOhJkd569YZdxfr3B7OiiIbZ/U1k8mzwwuG\r\nW/wSzfPGaab3LlZJD8+TSrIHrtPIFDuqUUK90v5fMAtkkfixCM2w5tJxq6nsKeE6\r\nMS2bmouCJFVSGxZ2dFYK22D66D03DZ5siq4gtNgQnuVaoGUgzak96yQPIvl1DD1n\r\nXhQq0SSF9qiq0+uBNT5G7PNdLWz80Q68kl0r9dApOMfhn3yZte+0O38orhpoPLJ2\r\nPGJvlt4vwkjwTVFIFa5LwdNS2riVP6147ilbpi/HZLtmJIsebGLjeGc7y/S9BCN2\r\nrTrDU2K0rmLgNmglJRh9SHDPmvYtcarVizfHTJAIzMF5W77//Q4=\r\n-----END CERTIFICATE REQUEST-----",
    "contact_email": "enc365@qiaokr.com",
    "domains": [
        "www.trustocean.com",
        "trustocean.com",
        "api.trustocean.com"
    ],
    "total_fees": 0
}
```