# 调用API {#reference_vy5_swc_xdb .reference}

本文档主要介绍调用物联网平台云端API的请求结构和请求示例。

## 请求结构 {#section_qjd_4t5_ydb .section}

您可以通过发送HTTP或HTTPS请求调用物联网平台API。

请求结构如下：

``` {#codeblock_3m3_f0x_vvy}
http://Endpoint/?Action=xx&Parameters
```

|参数|说明|
|:-|:-|
|Endpoint|调用云服务的接入地址。物联网平台的接入地址格式：`iot.${RegionId}.aliyuncs.com`。其中，变量$\{RegionId\}需替换为您的物联网平台服务的地域代码。阿里云地域代码，请参见[地域和可用区](../../../../cn.zh-CN/通用参考/地域和可用区.md#)。 接入地址示例：

 -   华东2（上海）：`iot.cn-shanghai.aliyuncs.com`
-   新加坡：`iot.ap-southeast-1.aliyuncs.com`
-   美国（硅谷）：`iot.us-west-1.aliyuncs.com`
-   日本（东京）：`iot.ap-northeast-1.aliyuncs.com`
-   德国（法兰克福）：`iot.eu-central-1.aliyuncs.com`

 |
|Action|要执行的操作，即云端API接口的名称。例如，调用Pub接口向指定Topic发布消息，Action对应的值就是Pub，即`Action=Pub`。|
|Parameters|请求参数。每个参数之间用（&）符号分隔。 请求参数由[公共请求参数](cn.zh-CN/云端开发指南/云端API参考/公共参数.md#)和API自定义参数组成。公共参数中包含API版本号、身份验证等信息。

 |

下面以调用Pub接口向指定Topic发布消息为例：

**说明：** 本文档示例均使用华东2（上海）地域的接入地址。为了便于阅读，本文档中的示例均做了格式化处理。

``` {#codeblock_3ee_5ha_vu3}
https://iot.cn-shanghai.aliyuncs.com/?Action=Pub
&Format=XML
&Version=2017-04-20
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dgI%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=...
&Timestamp=2017-07-19T12:00:00Z
&RegionId=cn-shanghai
...
```

## API在线调试 {#section_iyj_mmq_bhb .section}

阿里云提供API在线调试工具 [OpenAPI Explorer](https://api.aliyun.com)。在OpenAPI Explorer页，您可以快速检索和试验调用API。系统会根据您输入的参数同步生成各语言SDK的Demo代码。各语言SDK Demo显示在页面右侧**示例代码**页签下供您参考。在**调试结果**页签下，查看API调用的真实请求URL和JSON格式的返回结果。

![物联网平台API](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7563/156766724640697_zh-CN.png)

## API授权 {#section_qd5_fx5_ydb .section}

为了确保您的账号安全，建议您使用子账号的身份凭证调用API。如果您使用RAM子账号调用物联网平台API，您需要为该RAM子账号创建、授予相应的授权策略。

为子账号授权调用API，请参见[IoT API 授权映射表](../../../../cn.zh-CN/用户指南/账号与登录/RAM授权管理/IoT API 授权映射表.md#)。

