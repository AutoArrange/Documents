# 接口文档



## 用户管理模块

### 用户注册

```http
POST /register
```

#### 请求参数

| 参数        | 名称     | 类型   | 必选   | 说明                                  |
| ----------- | -------- | ------ | ------ | ------------------------------------- |
| username    | 账户     | String | 是     |                                       |
| password    | 密码     | String | 是     | md5加密                               |
| description | 个人介绍 | String | 否     |                                       |
| contact     | 联系方式 | json   | 否     | 如果是对象数据库直接将json储存即可    |
| method      | 验证方式 | int    | 是     | 如果是1则手机号验证，如果2则email验证 |
| phone       |          |        | 二选一 |                                       |
| email       |          |        | 二选一 | 后端应发送验证邮件到邮箱当中          |

#### 返回参数

以json形式返回

| 参数  | 名称         | 类型   | 必选 | 说明                   |
| ----- | ------------ | ------ | ---- | ---------------------- |
| msg   | 结果信息     | String | 否   | 消息直接弹窗回显给用户 |
| code  | 状态码       | int    | 是   | 200代表成功            |
| token | 令牌         | String | 否   | 注册成功则返回         |
| info  | 用户相关信息 | json   | 否   | 注册成功则返回         |

info中的（key，value）

| 参数        | 名称     | 类型   | 必选 | 说明 |
| ----------- | -------- | ------ | ---- | ---- |
| username    | 用户名   | String | 是   |      |
| contact     | 联系方式 | json   | 否   |      |
| description | 个人介绍 | String | 否   |      |

contact中的（key，value）

| 参数   | 名称 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| email  | 电邮 | String | 否   |      |
| phone  | 电话 | String | 否   |      |
| qq     | QQ   | String | 否   |      |
| wechat | 微信 | String | 否   |      |

##### 示例数据

```json
{
    "msg": "登录成功！",
    "code": 200,
    "token": "ae123nfiajo190139ndkaefn", 
    "info": 
    {
        "username": "peter",
        "description": "山东大学的一名学生",
        "contact": 
        {
            "phone": "110",
            "email": "email@example.com"
        }
    }
}
```



### 用户登录

```http
GET /login?id=13579&passwd=md5(123456)
```

#### 请求参数

| 参数     | 名称 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| id       | 账户 | String | 是   |      |
| password | 密码 | String | 是   |      |

#### 返回参数

以json形式返回

| 参数  | 名称         | 类型   | 必选 | 说明                   |
| ----- | ------------ | ------ | ---- | ---------------------- |
| msg   | 结果信息     | String | 否   | 消息直接弹窗回显给用户 |
| code  | 状态码       | int    | 是   | 200代表成功            |
| info  | 用户相关信息 | json   | 否   | 登录成功则返回         |
| token | 令牌         | String | 否   | 登陆成功则返回         |

info中的（key，value）

| 参数        | 名称     | 类型   | 必选 | 说明 |
| ----------- | -------- | ------ | ---- | ---- |
| username    | 用户名   | String | 是   |      |
| contact     | 联系方式 | json   | 否   |      |
| description | 个人介绍 | String | 否   |      |

contact中的（key，value）

| 参数   | 名称 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| email  | 电邮 | String | 否   |      |
| phone  | 电话 | String | 否   |      |
| qq     | QQ   | String | 否   |      |
| wechat | 微信 | String | 否   |      |

##### 示例数据

```json
{
    "msg": "登录成功！",
    "code": 200,
    "token": "ae123nfiajo190139ndkaefn", 
    "info": 
    {
        "username": "peter",
        "description": "山东大学的一名学生",
        "contact": 
        {
            "phone": "110",
            "email": "email@example.com"
        }
    }
}
```



### 修改/忘记密码

```http
GET /change-password?id=13579&step=1
```

#### 请求参数

| 参数         | 名称   | 类型   | 必选 | 说明   |
| ------------ | ------ | ------ | ---- | ------ |
| id           | 账户   | String | 是   |        |
| step         | 步骤   | int    | 是   |        |
| verification | 验证码 | String | 否   | step=2 |

#### 示例代码

```http
GET /change-password?id=13579&step=2&verification=ae86
```



#### 返回参数

- step=1时，

| 参数 | 名称     | 类型   | 必选 | 说明                                   |
| ---- | -------- | ------ | ---- | -------------------------------------- |
| msg  | 结果信息 | String | 否   | 消息直接弹窗回显给用户                 |
| code | 状态码   | int    | 是   | 200代表正常                            |
| img  | 验证码   | String | 否   | 状态正常则返回验证码，以base64格式返回 |

##### 示例数据

```json
{
    "code": 200, 
    "img": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgUAAAHOCAYAAAAIW3rnAAAgAElEQVR4XuydCZxUxfHHf9VvZvbgBkEUVFR0F0RYRGM0JvGK8Yz/qEvUaNTI4YXxgAU8smIUEFCUSyVGjUmMitEYFTQRMDHGk1u5ROOBUUFABPaYo+v/6dlFl92ZnbfL7Dm/9/kQJNOvu+rbNfPqdVdXCXiRAAmQAAmQAAmQAAAhBRIgARIgARIgARJwBOgU0A5IgARIgARIgATiBOgU0BBIgARIgARIgAToFNAGSIAESIAESIAEviXAlQJaAwmQAAmQAAmQAFcKaAMkQAIkQAIkQAJcKaANkAAJkAAJkAAJVCPA7QOaBAmQAAmQAAmQALcPaAMkQAIkQAIkQALcPqANkAAJkAAJkAAJcPuANkACJEACJEACJJCIAGMKaBckQAIkQAIkQAKMKaANkAAJkAAJkAAJMKaANkACJEACJEACJMCYAtoACZAACZAACZAAYwpoAyRAAiRAAiRAAkkJMNCQxkECJEACJEACJBAnQKeAhkACJEACJEACJECngDZAAiRAAiRAAiTwLQGuFNAaSIAESIAESIAEuFJAGyABEiABEiABEuBKAW2ABEiABEiABEigGgFuH9AkSIAESIAESIAEuH1AGyABEiABEiABEuD2AW2ABEiABEiABEiA2we0ARIgARIgARIggUQEGFNAuyABEiABEiABEmBMAW2ABEiABEiABEiAMQW0ARIgARIgARIgAcYU0AZIgARIgARIgAQYU0AbIAESIAESIAESSEqAgYY0DhIgARIgARI"
}
```

- step=2时，

| 参数 | 名称     | 类型   | 必选 | 说明            |
| ---- | -------- | ------ | ---- | --------------- |
| msg  | 结果信息 | String | 否   |                 |
| code | 状态码   | int    | 是   | 200代表验证成功 |



### 修改用户信息

```http
POST /update-info
```

#### 请求参数

| 参数  | 名称       | 类型   | 必选 | 说明                                                 |
| ----- | ---------- | ------ | ---- | ---------------------------------------------------- |
| token | 令牌       | String | 是   |                                                      |
| info  | 更新的信息 | json   | 是   | 更新可能会发送空json，服务器直接将数据库info替换即可 |

#### 示例代码

```http
GET /change-password?id=13579&step=2&verification=ae86
```



#### 返回参数

| 参数 | 名称         | 类型   | 必选 | 说明                                                         |
| ---- | ------------ | ------ | ---- | ------------------------------------------------------------ |
| msg  | 结果信息     | String | 否   | 消息直接弹窗回显给用户                                       |
| code | 状态码       | int    | 是   | 200代表正常                                                  |
| info | 更新后的信息 | json   | 是   | 如果更新成功，服务器直接返回请求的info即可，否则返回数据库中info信息 |



---



## 消息推送

采用WebSocket方式进行消息交互，客户端/服务器发送的数据一律用json格式传送，

### 通知推送

后台发送的数据应如下

```json
{
    "type": "notification",
    "content": "<html>...</html>",
    "priority": "critical"
}
```

#### 参数说明

| 参数     | 名称     | 类型   | 必选 | 说明                                              |
| -------- | -------- | ------ | ---- | ------------------------------------------------- |
| type     | 通知种类 | String | 是   | 在此场景下固定为“notification”                    |
| content  | 通知内容 | String | 是   | 可以是纯文本，也可以是html形式的富文本            |
| priority | 优先级   | String | 否   | 暂分为三个等级，"critical", "important", "normal" |



### 海报具体信息推送

后台发送的数据应如下，注意posters是一个JSON数组

```json
{
    "type": "posters",
    "posters": 
    [
        {"title": "山东大学校招", "content": "<html>...<html>"},
        {"title": "opps社团纳新", "content": "<html>...<html>"},
    ]
}
```

#### 参数说明

| 参数    | 名称     | 类型   | 必选 | 说明                      |
| ------- | -------- | ------ | ---- | ------------------------- |
| type    | 通知种类 | String | 是   | 在此场景下固定为“posters” |
| posters | 海报数组 | json   | 是   |                           |

posters数组内每个item均是一个json字典，包含以下（key，value）

| 参数    | 名称     | 类型   | 必选 | 说明                                   |
| ------- | -------- | ------ | ---- | -------------------------------------- |
| title   | 海报标题 | String | 否   |                                        |
| content | 海报内容 | String | 是   | 可以是纯文本，也可以是html形式的富文本 |



---



## 权限更改

​	对于每个app用户，针对单一海报/活动有三种不同角色，分别是海报设计者（发布者，后续还可以更改海报），通知推送者，受众；一张海报刚上传时，发布者默认双重身份（设计者/通知者）；而权限只能从一个用户转移到另一个用户

```http
GET /transfer-privilege?token=ae123nfiajo190139ndkaefn&id=13579&to=201805130000&step=1
```

```http
GET /transfer-privilege?validation=aeoiefojw2891fae2121&step=2
```



### 请求参数

step=1的时候发送请求，服务器传送验证性token码给客户端，step=2时，客户端传送刚获取的验证性token发给服务器，服务器进行验证后，验证性token推荐包含用户信息，项目信息，转让权限，有效时效等信息，此举出于安全考虑

| 参数       | 名称        | 类型   | 必选       | 说明                              |
| ---------- | ----------- | ------ | ---------- | --------------------------------- |
| to         | 转让的账号  | String | step=1必需 |                                   |
| id         | 海报id      | String | step=1必需 |                                   |
| token      | 用户令牌    | String | step=1必需 |                                   |
| privilege  | 转让的权限  | String | step=1必需 | 只可能两个值"designer", "manager" |
| step       | 步骤        | int    | 是         |                                   |
| validation | 验证性token | String | step=2必需 |                                   |

### 返回参数

- step=1时，

| 参数       | 名称        | 类型   | 必选 | 说明                   |
| ---------- | ----------- | ------ | ---- | ---------------------- |
| msg        | 结果信息    | String | 否   | 消息直接弹窗回显给用户 |
| code       | 状态码      | int    | 是   | 200代表正常            |
| validation | 验证性token | String | 是   |                        |

- step=2时，

| 参数 | 名称     | 类型   | 必选 | 说明                   |
| ---- | -------- | ------ | ---- | ---------------------- |
| msg  | 结果信息 | String | 否   | 消息直接弹窗回显给用户 |
| code | 状态码   | int    | 是   | 200代表转让成功        |



---



## 上传

### 上传海报

形式等同于如此上传，对于服务器端，如果用php直接$_FILES就可以获取，NodeJS用express框架可用req.files方式获取

```html
<form action="/upload-poster" method="post" enctype="multipart/form-data">
    <h2>单图上传</h2>
    <input type="file" name="logo">
    <input type="submit" value="提交">
</form>
```



#### 请求参数

此部分参数将放在header中

| 参数  | 名称     | 类型   | 必选 | 说明 |
| ----- | -------- | ------ | ---- | ---- |
| title | 海报标题 | String | 否   |      |
| token | 用户令牌 | String | 是   |      |

#### 返回参数

| 参数 | 名称     | 类型   | 必选 | 说明                   |
| ---- | -------- | ------ | ---- | ---------------------- |
| msg  | 结果信息 | String | 否   | 消息直接弹窗回显给用户 |
| code | 状态码   | int    | 是   | 200代表成功            |
| id   | 海报id   | String | 是   |                        |



### 发送通知

形式等同于如此上传，对于服务器端，如果用php直接$_FILES就可以获取，NodeJS用express框架可用req.files方式获取

```http
POST /upload-notification
```



#### 请求参数

此部分参数将放在header中

| 参数     | 名称     | 类型   | 必选 | 说明                                              |
| -------- | -------- | ------ | ---- | ------------------------------------------------- |
| title    | 消息标题 | String | 否   |                                                   |
| token    | 用户令牌 | String | 是   |                                                   |
| priority | 优先级   | String | 否   | 暂分为三个等级，"critical", "important", "normal" |
| content  | 通知内容 | String | 是   | 富文本信息                                        |

#### 返回参数

| 参数 | 名称     | 类型   | 必选 | 说明                   |
| ---- | -------- | ------ | ---- | ---------------------- |
| msg  | 结果信息 | String | 否   | 消息直接弹窗回显给用户 |
| code | 状态码   | int    | 是   | 200代表成功            |