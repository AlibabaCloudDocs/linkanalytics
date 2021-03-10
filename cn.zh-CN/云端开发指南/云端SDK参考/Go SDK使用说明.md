# Go SDK使用说明

物联网平台提供Go语言的云端SDK供开发人员使用。本文介绍云端Go SDK的安装和配置，及使用Go SDK调用云端API的示例。

## 安装SDK

1.  安装Go开发环境。

    目前支持Go 1.6及以上版本。请访问[Go官网](https://golang.org/doc/install/source?spm=a2c4g.11186623.2.11.4c1dc4862n20n9)获取。

2.  Go安装完毕后，新建系统变量GOPATH，并将其指向您的代码目录。

    了解更多GOPATH相关信息，请执行命令`go help gopath`。

3.  执行以下命令安装阿里云Go SDK。

    ```
    go get -u github.com/aliyun/alibaba-cloud-sdk-go/sdk
    ```

    了解Go SDK最新信息，请访问[alibaba-cloud-sdk-go](https://github.com/aliyun/alibaba-cloud-sdk-go/tree/master)。

4.  执行以下命令将IoT Go SDK相关文件引入Go文件。

    ```
    import "github.com/aliyun/alibaba-cloud-sdk-go/services/iot"
    ```


## 初始化SDK

```
package main

import "github.com/aliyun/alibaba-cloud-sdk-go/services/iot"

func main() {

    client, err := sdk.NewClientWithAccessKey("<your regionId>", "<your accessKey>", 
                                              "<your accessSecret>")
    if err != nil {
        // Handle exceptions
        panic(err)
    }
}
```

|参数|说明|
|--|--|
|regionId|阿里云服务地域代码，例如华东2为`cn-shanghai`。请参见[地域和可用区]()。|
|accessKey|您的阿里云账号的AccessKey ID。您可在[阿里云官网控制台AccessKey管理](https://ak-console.aliyun.com)中，创建或查看您的AccessKey。|
|accessSecret|AccessKey ID对应的AccessKey Secret。在[阿里云官网控制台AccessKey管理](https://ak-console.aliyun.com)中查看。|

## 发起调用

物联网平台云端API，请参见[API列表](/cn.zh-CN/云端开发指南/云端API参考/API列表.md)。

以调用Pub接口发布消息到自定义Topic为例。

**说明：** 以下代码中iotInstanceId为实例ID，企业版实例填写实例ID，公共实例要删除代码`request.IotInstanceId = "<your iotInstanceId>"`。

关于如何购买企业版实例，请参见[实例管理](/cn.zh-CN/.md)。

```
request := iot.CreatePubRequest()
request.AcceptFormat = "json"
request.IotInstanceId = "<your iotInstanceId>"
request.ProductKey = "<your productKey>"
var builder strings.Builder
builder.WriteString("/")
builder.WriteString(request.ProductKey)
builder.WriteString("/")
builder.WriteString("<your deviceName>")
builder.WriteString("/user/update")
request.TopicFullName = builder.String()
request.MessageContent = base64.StdEncoding.EncodeToString([]byte("hello world"))
request.Qos = "0"
response, err := client.Pub(request)
if err != nil {
    fmt.Print(err.Error())
}
fmt.Printf("response is %#v\n", response)
```

## 附录：Demo

下载[物联网平台云端SDK Demo](https://github.com/aliyun/iotx-api-demo)。Demo中包含Java、Python、PHP、.NET和Go版本SDK示例。

阿里云OpenAPI开发者门户提供[API在线调试工具](https://next.api.aliyun.com/api/Iot)。在**API调试**页面，您可以快速检索和体验调用API。系统会根据您输入的参数同步生成各语言SDK的Demo代码。各语言SDK Demo显示在页面右侧**SDK示例**页签下供您参考。在**调用结果**页签下，查看API调用的真实请求URL和JSON格式的返回结果。

