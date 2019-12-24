# 文本纠错小助手APP

## 加值宣言
- 一段文字

## 核心价值
- 帮助用户减少校对文本的时间，指出他们文字中的敏感的内容。

## 需求背景
- 目前国内互联网对非法内容监督得越来越严格，不论是哪个社交平台都要求用户不可发布非法内容。然而即便用户知道这个要求，他们也很难保证自己发布的内容不会有敏感字眼。与此同时，用户在日常生活因各种原因会编写文档，他们常常需要花费大量的时间去检查自己的文字，查找其中的错别字。

## 需求目的
- 帮助用户找出他们文本中的敏感内容。
- 减少用户寻找错别字的时间。

## 需要的API
### API来自百度AI开放平台下的自然语言处理模块。
- 文本审核。
- 本文纠错。

## API的价值主张
- 文本审核：在用户输入一段文字后，该APP可判断一段文本内容是否符合网络发文规范，对文本中内容进行识别。
- 文本纠错：在用户输入文本内容后，该API可准确识别输入文本中出现的拼写错别字及其段落位置信息，并针对性给出正确的建议文本内容。该API支持短文本、长文本、语音识别结果等多种文本内容，在搜索引擎、语音识别、内容审核有广泛应用，能显著提高各场景下语义的准确性和用户阅读体验。

## APP价值主张
- 用户进入APP后，可检查自己的文本是否有出现错字病句的情况。
- 用户进入APP后，可检查自己的文本是否含有敏感内容，如低俗色情内容，暴力内容，政治敏感内容等。

## APP价值核心
### 由于我国有着特殊的国情，国内定义的敏感内容有别于其他国家，故本项目使用的是百度AI开放平台内的API，而不是国外互联网公司旗下的API。
- 用户将文本输入APP后，APP将会判断一段文本内容是否符合网络发文规范，是否含有不适当内容。
- 在用户输入一段文字后，APP可以准确识别输入文本中出现的拼写错别字及其段落位置信息，并针对性给出正确的建议文本内容。

## 针对用户
- 文字工作者/文字爱好者。
- 对检查文字缺少耐心的人。

## 用户痛点
- 我国现在对互联网上发布的文本抓得越来越严，很多用户都遇到过在社交平台上发布内容后文字被屏蔽的情况。有些时候用户并不知道自己的内容哪里不合适，违反了互联网上的规则，故用户可在发布文本内容前将文字输入到APP内，检查自己的文字是否存在不和谐的内容。
- 当今时代，许多互联网用户很难有耐心花时间去检查自己编写的文字。如果是文字工作者（或者是文字爱好者），他们在读自己的文章时很容易带着自己的想法检查自己的文章（即自己默读检查时，明明句子里面的文字有错，却在读的时候带着自我意识读），从而看不出本文中的错字或者病句。本APP可帮助用户在较短的时间内找出文字中的错字和病句，并随之给予相应的修改建议。

## 产品原型
### 首页
![首页](/picture/首页.png)
### 文本纠错
![文本纠错](/picture/文本纠错.png)
### 文本审核
![文本审核](/picture/文本审核.png)
### 一键并用
![一键并用](/picture/一键并用.png)

## 产品结构图
### 产品功能结构图
![产品功能](/picture/产品功能.png)

## API的运用
### 文本审核
- 调用方法：向API服务地址使用POST发送请求，必须在URL中带上参数；access_token: 必须参数，参考“Access Token获取；POST中参数按照API接口说明调用即可；例如自然语言处理API，使用HTTPS POST发送：
- 注意：如有疑问，进入AI社区交流：http://ai.baidu.com/forum/topic/list/172。
- 请求方式：POST。
- 请求URL：https://aip.baidubce.com/rest/2.0/solution/v1/text_censor/v2/user_defined 
- 使用示例：
```
https://aip.baidubce.com/rpc/2.0/nlp/v1/lexer?access_token=24.f9ba9c5241b67688bb4adbed8bc91dec.2592000.1485570332.282335-8574074
```
![输入例子](/picture/输入1.png)
- 返回示例：<br></br>
![返回示例](/picture/输出2.png)
- 成功响应示例 ——合规：
```
{
	"log_id": 15556561295920002,
	"conclusion": "合规",
	"conclusionType": 1
}

或者

{
    "log_id": 15572142621780024,
    "conclusion": "合规",
    "conclusionType": 1,
    "data": [{
        "type": 14,
        "subType": 0,
        "conclusion": "合规",
        "conclusionType": 1,
        "msg": "自定义文本白名单审核通过",
        "hits": [{
            "datasetName": "SLK-测试-自定义文本白名单",
            "words": ["习大大"]
        }]
    }]
}
```
- 成功响应示例——不合规：
```
{
    "log_id": 123456789,
    "conclusion": "不合规",
    "conclusionType": 2,
    "data": [{
        "type": 11,
        "subType": 0,
        "conclusion": "不合规",
        "conclusionType": 2,
        "msg": "存在百度官方默认违禁词库不合规",
        "hits": [{
            "datasetName": "百度默认黑词库",
            "words": ["免费翻墙"]
        }]
    }, {
        "type": 12,
        "subType": 2,
        "conclusion": "不合规",
        "conclusionType": 2,
        "msg": "存在文本色情不合规",
        "hits": [{
            "datasetName": "百度默认文本反作弊库",
            "probability": 1.0,
            "words": ["电话 找小姐"]
        }]
    }, {
        "type": 12,
        "subType": 3,
        "conclusion": "不合规",
        "conclusionType": 2,
        "msg": "存在政治敏感不合规",
        "hits": [{
            "probability": 1.0,
            "datasetName": "百度默认文本反作弊库",
            "words": ["敏感人物A"]
        }]
    }, {
        "type": 12,
        "subType": 4,
        "conclusion": "不合规",
        "conclusionType": 2,
        "msg": "存在恶意推广不合规",
        "hits": [{
            "probability": 1.0,
            "datasetName": "百度默认文本反作弊库",
            "words": [""]
        }]
    }, {
        "type": 13,
        "subType": 0,
        "conclusion": "不合规",
        "conclusionType": 2,
        "msg": "存在自定义文本黑名单不合规",
        "hits": [{
            "datasetName": "SLK-测试-自定义黑名单",
            "words": ["我是你爹", "他妈的"]
        }]
    }]
}
```

- 失败响应示例：
```
{
    "log_id": 149319909347709, 
    "error_code": 0,
    "error_msg":"configId error"
}
```

### 文本纠错
- 调用方法：通过API Key和Secret Key获取的access_token。
- 注意：GBK支持：默认按GBK进行编码，输入内容为GBK编码，输出内容为GBK编码，否则会接口报错编码错误；UTF-8支持：若文本需要使用UTF-8编码，请在url参数中添加charset=UTF-8 （大小写敏感）。
- 请求方式：POST。
- 请求URL：https://aip.baidubce.com/rpc/2.0/nlp/v1/ecnet
- 使用示例：
```
{
    "text": "百度是一家人工只能公司"
}
```
- 返回示例：
```
{
    "log_id": 6770395607901559829,
    "item": {
        "vec_fragment": [
            {
                "ori_frag": "只能",
                "begin_pos": 21,
                "correct_frag": "智能",
                "end_pos": 27
            }
        ],
        "score": 0.875169,
        "correct_query": "百度是一家人工智能公司"
    },
    "text": "百度是一家人工只能公司"
}
```
