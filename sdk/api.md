# HTTP API接入文档

## 接入域名

http://httpdns.ucloud.cn

## API 文档

### 查询 HTTPDNS 服务地址

GET /{auth_id}/service

请求参数

| 名称          | 位置   | 类型    | 必填 | 描述                                                         |
| :------------ | ------ | ------- | ---- | ------------------------------------------------------------ |
| auth_id       | Path   | String  | 是   | 鉴权 ID。                                                    |
| Authorization | Header | String  | 是   | 签名字符串为所有 url 参数按照参数命字典序列排序，例如 b=b1&c=c1&a=a1 的签名字符串为 a1-b1-c1-\<AuthSecret\>，然后计算出md5值，并转成全小写，其中 \<AuthSecret\> 用实际的鉴权 Secret 替代。 |
| timestamp     | Query  | Integer | 是   | 秒级时间戳，过期时间为1分钟。                                |
| ip            | Query  | String  | 否   | 客户端 IP，用于就近接入。                                    |
| app_id        | Query  | String  | 否   | APP ID，对于iOS应用为 Bundle ID，对于 Android 应用为 Package Name，当使用的鉴权 ID 属于控制台上创建的应用时，该参数必填。 |

响应参数

| HTTP 状态码 | 描述     | 示例                                                         |
| ----------- | -------- | ------------------------------------------------------------ |
| 200         | 查询成功 | {<br/>  "auth_id": "abc-xxx",<br/>  "client_ip": "100.11.11.11",<br/>  "best_service_node": "http://100.10.10.10",<br/>  "service_node_list": [<br/>    "http://100.10.10.10"<br/>  ]<br/>} |
| 401         | 认证失败 | {<br/>  "status": 401,<br/>  "code": "UNAUTHORIZED",<br/>  "message": "request is unauthorized"<br/>} |

### 进行 HTTPDNS 解析

GET /{auth_id}/resolve

请求参数

| 名称          | 位置   | 类型    | 必填 | 描述                                                         |
| :------------ | ------ | ------- | ---- | ------------------------------------------------------------ |
| auth_id       | Path   | String  | 是   | 鉴权 ID。                                                    |
| Authorization | Header | String  | 是   | 签名字符串为所有 url 参数按照参数命字典序列排序，例如 b=b1&c=c1&a=a1 的签名字符串为 a1-b1-c1-\<AuthSecret\>，然后计算出md5值，并转成全小写，其中 \<AuthSecret\> 用实际的鉴权 Secret 替代。 |
| timestamp     | Query  | Integer | 是   | 秒级时间戳，过期时间为1分钟。                                |
| host          | Query  | String  | 是   | 需要解析的域名                                               |
| app_id        | Query  | String  | 否   | APP ID，对于iOS应用为 Bundle ID，对于 Android 应用为 Package Name，当使用的鉴权 ID 属于控制台上创建的应用时，该参数必填。 |

响应参数

| HTTP 状态码 | 描述                                                         | 示例                                                         |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 200         | 查询成功，响应中的 ip_list 表示解析处的 IP 列表，ttl 表示解析结果的 | {<br/>  "host": "api.ucloud.cn",<br/>  "client_ip": "100.11.11.11",<br/>  "ip_list": [<br/>    "100.100.10.10"<br/>  ],<br/>  "ttl": 600<br/>} |
| 401         | 认证失败，message 提示 request is unauthorized               | {<br/>  "status": 401,<br/>  "code": "UNAUTHORIZED",<br/>  "message": "request is unauthorized"<br/>} |
| 403         | 域名无权限解析，没有添加到系统中，message 提示 host resolving is forbidden | {<br/>  "status": 403,<br/>  "code": "HOST_FORBIDDEN",<br/>  "message": "host resolving is forbidden"<br/>} |
| 404         | 解析解析失败，DNS 记录不存在，message 提示 record cannot be found | {<br/>  "status": 404,<br/>  "code": "FAIL_TO_RESOLVE",<br/>  "message": "record cannot be found"<br/>} |
| 404         | 解析解析失败，无法解析域名（外网DNS异常），message 提示 fail to resolve the host | {<br/>  "status": 404,<br/>  "code": "FAIL_TO_RESOLVE",<br/>  "message": "fail to resolve the host"<br/>} |

