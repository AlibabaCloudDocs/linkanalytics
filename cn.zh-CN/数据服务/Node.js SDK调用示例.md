---
keyword: [Node.js SDK, 数据分析, 数据服务, API]
---

# Node.js SDK调用示例

您可使用阿里云提供的Node.js SDK，来调用数据服务的API，从而更便捷地获取指定数据。本文以调用基础API为例，介绍Node.js SDK调用API的方法及示例。

## 前提条件

已开通数据分析功能，更多信息，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。

## 安装SDK

1.  登录[Node.js官方网站](https://nodejs.org/en/download/)，按照说明安装Node.js开发环境。

2.  执行以下命令，安装阿里云OpenAPI SDK。

    ```
    npm install @alicloud/openapi-client
    npm install @alicloud/iot20180120
    ```


## 发起调用

以下为调用**数据服务**下基础API历史至今设备数量相关统计的示例代码。您可参照参数说明，修改对应代码，调用指定的API。

```
const Config = require('@alicloud/openapi-client').Config;
const ListAnalyticsDataRequest = require('@alicloud/iot20180120').ListAnalyticsDataRequest;
const IotClient = require('@alicloud/iot20180120');
const ListAnalyticsDataRequestCondition = require('@alicloud/iot20180120/dist/client').ListAnalyticsDataRequestCondition;

// 创建客户端
const config = new Config();
config.endpoint = "iot.cn-shanghai.aliyuncs.com";
config.accessKeyId = "LTAI4FyDFmKN************";
config.accessKeySecret = "WF3onkl8cq3cTyVW8n************";
config.regionId = "cn-shanghai";

async function main() {
    const client = new IotClient.default(config);

    // 创建请求对象
    const listAnalyticsDataRequest = new ListAnalyticsDataRequest();
    // 您的API Path
    listAnalyticsDataRequest.apiPath = '/iot-cn-npk1v******/system/query/hist_dev_cnt_stat'
    // 分页参数：页号
    listAnalyticsDataRequest.pageNum = 1;
    // 分页参数：页大小
    listAnalyticsDataRequest.pageSize = 100;
    // 您的API所在的实例id
    listAnalyticsDataRequest.iotInstanceId = 'iot-cn-npk1v******' 
    //您的API业务相关的请求参数。Condition的配置说明，请参见下文的相关说明。
    const conditions = [];

    const condition = new ListAnalyticsDataRequestCondition();
    condition.operate = '=';
    condition.fieldName = '__instance_id__';
    condition.value = 'iot-public'
    conditions.push(condition)

    const condition1 = new ListAnalyticsDataRequestCondition();
    condition1.operate = '=';
    condition1.fieldName = 'entityId';
    condition1.value = 'all'
    conditions.push(condition1)

    const condition2 = new ListAnalyticsDataRequestCondition();
    condition2.operate = '=';
    condition2.fieldName = 'statDate';
    condition2.value = '20210221'
    conditions.push(condition2)

    listAnalyticsDataRequest.condition = conditions;

    try {
        const response = await client.listAnalyticsData(listAnalyticsDataRequest)
        console.log(response)
    } catch (ex) {
        console.log(ex);
    }
}

main();
```

-   系统请求参数：

    |名称|类型|是否必传|示例值|描述|
    |--|--|----|---|--|
    |endpoint|String|是|iot.cn-shanghai.aliyuncs.com|阿里云服务的API服务端地址。其中，地域需与物联网平台产品地域保持一致。在物联网平台控制台左上方可查看地域。RegionId的表达方法，请参见[地域和可用区]()。

本示例中，地域为华东2（cn-shanghai）。 |
    |accessKeyId|String|是|LTAI4FyDFmKN\*\*\*\*\*\*\*\*\*\*\*\*|登录物联网平台控制台，将鼠标移至账号头像上，然后单击**AccessKey管理**，获取AccessKey ID和AccessKey Secret。

**说明：** 如果使用RAM用户，您需授予该用户管理物联网平台的权限（AliyunIOTFullAccess），否则将连接失败。授权方法请参见[授权RAM用户访问物联网平台](/cn.zh-CN/权限管理/账号授权/RAM授权管理/RAM用户访问.md)。 |
    |accessKeySecret|String|是|WF3onkl8cq3cTyVW8n\*\*\*\*\*\*\*\*\*\*\*\*|
    |regionId|String|是|cn-shanghai|您的物联网平台服务所在地域ID。 在物联网平台控制台左上方可查看地域。RegionId的表达方法，请参见[地域和可用区]()。 |
    |apiPath|String|是|/iot-cn-npk1v\*\*\*\*\*\*/system/query/hist\_dev\_cnt\_stat|API路径。在**数据服务**的API列表下，单击API对应的**查看**，进入API详情页，可查看API Patch的值。更多信息，请参见[查看与使用](/cn.zh-CN/数据服务/使用数据服务.mdsection_mky_acn_k91)。|
    |pageNum|Integer|开启分页时必传|1|分页的页码。|
    |pageSize|Integer|开启分页时必传|100|每页显示结果的条数，最大值为200。|
    |iotInstanceId|String|是|iot-cn-npk1u\*\*\*\*\*\*|API所在的实例ID。|

-   业务相关的请求参数：

    |名称|类型|是否必传|说明|相关代码|
    |--|--|----|--|----|
    |fieldName|String|是|请求参数名称。|    ```
 condition.fieldName = '__instance_id__';
    ``` |
    |operate|String|是|请求参数对应的操作符。可选：    -   `=`：指定请求参数为特定值。
    -   `BETWEEN`：指定请求参数为特定范围。
    -   `IN`：指定请求参数为多个值。
    -   `!=`：指定请求参数不可为特定值。
|    ```
 condition.operate = '=';
    ``` |
    |value|String|否|请求参数的赋值。**说明：** 当操作符为非`BETWEEN`时，该参数必传。

|    ```
 condition.value = 'iot-public';
    ``` |
    |betweenStart|String|否|请求参数表示范围时的起始值。**说明：** 当操作符为`BETWEEN`时，该参数必传。

|    ```
 condition.betweenStart = '0';
    ``` |
    |betweenEnd|String|否|请求参数表示范围时的终止值。**说明：** 当操作符为`BETWEEN`时，该参数必传。

|    ```
 condition.betweenEnd = '1000';
    ``` |

    一个请求参数对应一个`Condition`。在API详情页，查看API的请求参数，您可配置指定数量的`Condition`。关于如何查看API请求参数的信息，请参见[查看与使用](/cn.zh-CN/数据服务/使用数据服务.mdsection_mky_acn_k91)。

    本文示例代码中，该API有3个请求参数（\_\_instance\_id\_\_、entityId、statDate分别对应`condition`、`condition 1`、`condition 2`）。


## 运行结果

-   成功：

    在对应API的详情页，您可查看返回参数的详细说明。具体操作，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。

    以下示例为调用API成功后的结果，即：从2021年2月21日起至调用API时，公共实例下的设备数量相关统计情况。

    ```
    ListAnalyticsDataResponse {
      headers: {
        date: 'Mon, 15 Mar 2021 10:40:58 GMT',
        'content-type': 'application/json;charset=utf-8',
        'content-length': '425',
        connection: 'keep-alive',
        'access-control-allow-origin': '*',
        'access-control-allow-methods': 'POST, GET, OPTIONS',
        'access-control-allow-headers': 'X-Requested-With, X-Sequence, _aop_secret, _aop_signature',
        'access-control-max-age': '172800',
        'x-acs-request-id': 'F278FA13-11E6-42BC-9883-3566AC******'
      },
      body: ListAnalyticsDataResponseBody {
        requestId: 'F278FA13-11E6-42BC-9883-3566AC******',
        success: true,
        data: ListAnalyticsDataResponseBodyData {
          hasNext: false,
          resultJson: '[{"statDate":"20210221","actDevCnt":2942,"onlineDevCntCompare":0.00,"livelyDevCntCompare":8.99,"livelyDevCnt":1527,"onlineDevRate":23.08,"crtDevCnt":169025,"livelyDevRate":51.90,"crtDevCntCompare":0.08,"onlineDevCnt":679,"actDevRate":1.74,"actDevCntCompare":4.55}]',
          pageNum: 1,
          pageSize: 200
        }
      }
    }
    ```

-   失败：

    通过调用失败结果中的错误码，您可了解失败的原因。关于错误码更多信息，请参见[错误码](/cn.zh-CN/数据服务/错误码.md)。

    以下示例为调用API失败后的结果，即：参数`__instance_idd__`为无效的请求参数，将其更正为`__instance_id__`后，重新发起调用。

    ![Node.js调用失败](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3984885161/p249901.gif)


