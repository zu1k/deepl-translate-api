# DeepL Free API

- Free, 无需注册帐号
- 暂时仅提供二进制，不开源
- 请求过于频繁仍会触发DeepL封IP

## 两个版本说明

**standalone**

可独立运行，使用Rocket提供http服务，可通过修改rocket配置文件覆盖某些配置

**lambda**

供aws lambda使用

## 使用说明

### Docker方式（唯一推荐方式）

```sh
docker run -itd -p 8080:80 zu1k/deepl
```

### deepl-standalone

这个版本与直接使用zu1k/deepl镜像类似

```
docker load < deepl-standalone.tar
```

### deepl-lambda

这个版本供aws lambda使用，使用时先导入本地docker中

```
docker load < deepl-lambda.tar
```

然后根据aws给出的提示推到Amazon ECR中，最后创建lambda函数和api网关

## API说明

### Request

- Method: `POST`  
- Path: `/translate`  
- Content-Type: `application/json`  

```json
{
    "text": "text to be translated",
    "source_lang": "auto",
    "target_lang": "ZH"
}
```

**language supported:**

- `DE`: 德语
- `EN`: 英语
- `ES`: 西班牙语
- `FR`: 法语
- `IT`: 意大利语
- `JA`: 日语
- `NL`: 荷兰语
- `PL`: 波兰语
- `PT`: 葡萄牙语
- `RU`: 俄语
- `ZH`: 中文
- `BG`: 保加利亚语
- `CS`: 捷克语
- `DA`: 丹麦语
- `EL`: 希腊语
- `ET`: 爱沙尼亚语
- `FI`: 芬兰语
- `HU`: 匈牙利语
- `LT`: 立陶宛语
- `LV`: 拉脱维亚语
- `RO`: 罗马尼亚语
- `SK`: 斯洛伐克语
- `SL`: 斯洛文尼亚语
- `SV`: 瑞典语

### Response

Content-Type: `application/json`  

```json
{
    "code": 200,
    "msg": "only if there is an error",
    "data": "translate result"
}
```

**code:**

- `200`: ok
- `500`: internal error
- `404`: what are you doing?

**msg**: if the code is not 200

**data**: if the code is 200
