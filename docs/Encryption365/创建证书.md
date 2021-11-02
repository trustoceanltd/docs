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