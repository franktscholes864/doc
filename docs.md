
## 1. 提交号码

URL: `/index.php/api/sms/addphone`  

类型： `POST`   
`Content-Type: application/json`  

| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| enc | string | 是 | 加密内容 |
| type | string | 是 | 项目类型 |
### ①示例POST加密前多个参数内容
```json
{"phone":["22890909925","22890909926","22890909927"],"type":"ws"}
```
### ①示例POST加密前单个参数内容
```json
{"phone":["22890909925"],"type":"ws"}
```
### ②加密方式

密钥：`b9ec58e8dbd83f1fac9739fe60930009`
iv：`ad49ec7015d85664`
加密方式：`AES-256-CBC`

对json加密后
`HepjLYteCxjKUkQMx89YKU1/+NKTx8ewJf7BUzzI/gaPrp5h2kbDUBwGw3rukPs6KD89wyn439WJ+4v5K3xe5rN1omJ8ukvleKixcG+FUss=`


### POST参数
```json
{"enc":"HepjLYteCxjKUkQMx89YKU1/+NKTx8ewJf7BUzzI/gaPrp5h2kbDUBwGw3rukPs6KD89wyn439WJ+4v5K3xe5rN1omJ8ukvleKixcG+FUss="}
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
| type | string   | 可选 | 项目类型 |

```json
{"phone":"22890909925","content":"you code 123456","send":"10086","type":"ws"}
```
### 加密方式相同
加密后结果`T7yBhLEFCE7uXOzi3WPrMJ/xJMrx5V4HrofJ8HkIsu8DVQbQDtFUO4JT7Eht5RUHx08ibj3WPY4ygE0hPpra5EeLuySwq577putCNLjEpVs=`

### POST参数
```json
{"enc":"T7yBhLEFCE7uXOzi3WPrMJ/xJMrx5V4HrofJ8HkIsu8DVQbQDtFUO4JT7Eht5RUHx08ibj3WPY4ygE0hPpra5EeLuySwq577putCNLjEpVs="}
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



### 返回实时数据示例
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

### 返回缓存10分钟数据示例
```json
{"code":0,"msg":"同步缓存中","time":1699642213,"data":null}
```
```json
{"code":1,"msg":"操作成功","time":1699642392,"data":[{"phone":"2349065969566","sell":0,"result":"blocked"},{"phone":"919354544482","sell":0,"result":"no_routes"},{"phone":"918978410765","sell":0,"result":"no_routes"},{"phone":"919580370211","sell":0,"result":"已注册"},{"phone":"918395050704","sell":0,"result":"已注册"},{"phone":"23408055201563","sell":0,"result":"已注册"},{"phone":"918855091169","sell":0,"result":"blocked"},{"phone":"918866565201","sell":0,"result":"blocked"},{"phone":"919776369359.","sell":0,"result":"blocked"},{"phone":"919332082750","sell":0,"result":"完成"},{"phone":"918297309999","sell":0,"result":"完成"},{"phone":"919026170459","sell":0,"result":"已注册"},{"phone":"919621121858","sell":0,"result":"已注册"}]
```








## 1. `协议存活检测`

URL: `https://ws.google*****.com/api/login`

类型： `post`  
`Content-Type: application/json`  


| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| pub | string | 是 | 公钥 |
| mkey | string | 是 | 私钥 |
| mobile | string | 是 | 号码 |
| version | string | 是 | 0个人版,10商业版 |


### 请求POST参数/内置隧道代理
```json
{
    "pub": "kYVd+KCdXima8HzMvYEav2zaAJRAt8UC3pZ93W8E/EA=",
    "mkey": "kFucQ6L9pB4ml/RK8w0J0oZItF/QJtnVWMiqfozMz2I=",
    "mobile": "919776398280",
    "version":0
}
```


### 返回示例

成功
```json
{"status":"success"}
```
授权失效
```json
{
    "status": "failed",
    "msg": "<failure receipt=\"401\" location=\"nao\">\n</failure>\n"
}
```
封号
```json
{"status":"failed","msg":"<failure vt=\"15\" appeal_token=\"xxx\" receipt=\"403\" location=\"frc\">\n</failure>\n"}
```



## 2. `批量解封`
URL: `https://ws.google*****.com/api/blocked`

类型： `post`  
`Content-Type: application/json`  


| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| pub | string | 是 | 公钥 |
| mkey | string | 是 | 私钥 |
| mobile | string | 是 | 号码 |
| version | string | 是 | 0个人版,10商业版 |


### 请求POST参数/内置隧道代理

```json
{
    "pub": "kYVd+KCdXima8HzMvYEav2zaAJRAt8UC3pZ93W8E/EA=",
    "mkey": "kFucQ6L9pB4ml/RK8w0J0oZItF/QJtnVWMiqfozMz2I=",
    "mobile": "919776398280",
    "version":0
}
```

### 返回示例

```json
{
    "status": "success",
}
```

```json
{
     "status": "failed",
}
```

## 2. `解封后修复账号`


URL: `https://ws.google*****.com/api/repair`

类型： `post`  
`Content-Type: application/json`  


| 字段  | 类型 | 必填 | 说明   |
|-----| ---- | ---- |------|
| pub | string | 是 | 公钥 |
| mkey | string | 是 | 私钥 |
| mobile | string | 是 | 号码 |
| mobile | string | 是 | ID |
| version | string | 是 | 0个人版,10商业版 |


### 请求POST参数/内置隧道代理

```json
{
    "pub": "kYVd+KCdXima8HzMvYEav2zaAJRAt8UC3pZ93W8E/EA=",
    "mkey": "kFucQ6L9pB4ml/RK8w0J0oZItF/QJtnVWMiqfozMz2I=",
    "id": "OTQ3NTYxNzA2MDE5NDc1NjE3MDY=",
    "mobile": "919776398280",
    "version":0
}
```

### 返回新公私钥示例

```json
{
    "status": "success",
    "newpub": "kYVd+KCdXima8HzMvYEav2zaAJRAt8UC3pZ93W8E/EA=",
    "newmkey": "kFucQ6L9pB4ml/RK8w0J0oZItF/QJtnVWMiqfozMz2I=",
    "identpub": "kYVd+KCdXima8HzMvYEav2zaAJRAt8UC3pZ93W8E/EA=",
    "identkey": "kFucQ6L9pB4ml/RK8w0J0oZItF/QJtnVWMiqfozMz2I=",
    "newid": "OTQ3NTYxNzA2MDE5NDc1NjE3MDY=",

}
```

```json
{
     "status": "failed",
}
```





