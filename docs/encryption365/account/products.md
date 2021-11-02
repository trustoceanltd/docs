产品列表
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
