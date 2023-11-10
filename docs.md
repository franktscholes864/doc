
## 1. 提交号码

URL: `/index.php/api/sms/addphone`  

类型： `POST`   
`Content-Type: application/json`  

| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| enc | string | 是 | 加密内容 |
### ①示例POST加密前多个参数内容
```json
{"phone":["22890909925","22890909926","22890909927"]}
```
### ①示例POST加密前单个参数内容
```json
{"phone":["22890909925"]}
```
### ②加密方式

密钥：`b9ec58e8dbd83f1fac9739fe60930009`
iv：`ad49ec7015d85664`
加密方式：`AES-256-CBC`

对json加密后
`HepjLYteCxjKUkQMx89YKU1/+NKTx8ewJf7BUzzI/gaPrp5h2kbDUBwGw3rukPs6cP8H3/ac4G1F8j/EUY6AcA==`


### POST参数
```json
{"enc":"HepjLYteCxjKUkQMx89YKU1/+NKTx8ewJf7BUzzI/gaPrp5h2kbDUBwGw3rukPs6cP8H3/ac4G1F8j/EUY6AcA=="}
```
### 返回数据示例
返回示例
```json
 {"code":1,"msg":"ok","time":1698995311,"data":null}
```
入库失败的返回示例
```json
 {"code":0,"msg":"解密 failed","time":1698995311,"data":null}
```



## 2. `短信入库`


URL: `/index.php/api/sms/addsms`

类型： `POST`  
`Content-Type: application/json`  


| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| enc | string | 是 | 加密内容 |


### ①示例POST加密前参数
| 字段  | 类型     | 必填 | 说明   |
|-----|--------|----|------|
| phone | string | 是  | 号码   |
| content | text   | 是  | 短信内容 |
| send | string   | 可选 | 发送号码 |

```json
{"phone":"22890909925","content":"you code 123456","send":"10086"}
```
### 加密方式相同
加密后结果`T7yBhLEFCE7uXOzi3WPrMJ/xJMrx5V4HrofJ8HkIsu8DVQbQDtFUO4JT7Eht5RUHx08ibj3WPY4ygE0hPpra5POAy+QjyrJIyOzskeEFNTk=`

### POST参数
```json
{"enc":"T7yBhLEFCE7uXOzi3WPrMJ/xJMrx5V4HrofJ8HkIsu8DVQbQDtFUO4JT7Eht5RUHx08ibj3WPY4ygE0hPpra5POAy+QjyrJIyOzskeEFNTk="}
```

### 返回数据示例
返回示例
```json
{
  "code": 1,
  "msg": "ok",
  "time": 1698999518,
  "data": null
}
```
## 3. `查询结果`


URL: `/index.php/api/sms/task`

类型： `post`  
`Content-Type: application/json`  


| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| phone | string | 是 | 号码 |




### 加密前请求POST参数

{"phone":["22890909927","22890909926","22890909921"]}



### 返回数据示例
```json
{
    "code": 1,
    "msg": "操作成功",
    "time": 1699607537,
    "data": {
        "22890909927": "封号",
        "22890909926": "暂无结果",
        "22890909921": "暂无结果"
    }
}
```

### 请求全部POST参数
请求参数:   {}
```json
{"code":0,"msg":"同步缓存中","time":1699642213,"data":null}
```
