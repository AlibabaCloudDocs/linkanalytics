---
keyword: [Python SDK, 数据分析, 数据服务, API]
---

# Python SDK调用示例

您可使用阿里云提供的Python SDK，来调用数据服务的API，从而更便捷地获取指定数据。本文以调用基础API为例，介绍Java SDK调用API的方法及示例。

## 前提条件

已开通数据分析功能，更多信息，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。

## 安装SDK

1.  安装Python开发环境。

    访问[Python官网](https://www.python.org/downloads/)，下载Python安装包，并完成安装。目前，Python SDK支持Python的2.7.x和3.x版本。

2.  安装Python的包管理工具pip。（如果您已安装pip，请忽略此步骤。）

    访问 [pip 官网](https://pip.pypa.io/en/stable/installing/)，下载pip安装包，并完成安装。

3.  以管理员权限执以下命令，安装IoT Python SDK。

    以管理员权限执以下命令，安装IoT Python SDK。请参见最新版[aliyun-python-sdk-iot](https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-iot)信息。

    ```
    sudo pip install aliyun-python-sdk-core
    sudo pip install alibabacloud-iot20180120==2.2.0
    ```

4.  将IoT Python SDK相关文件引入Python文件。

    ```
    from alibabacloud_iot20180120.client import Client
    from alibabacloud_iot20180120.models import ListAnalyticsDataRequest, ListAnalyticsDataRequestCondition
    from alibabacloud_tea_openapi.models import Config
    ```


## 发起调用

以下为调用**数据服务**下基础API历史至今设备数量相关统计的示例代码。您可参照参数说明，修改对应代码，调用指定的API。

```
from alibabacloud_iot20180120.client import Client
from alibabacloud_iot20180120.models import ListAnalyticsDataRequest, ListAnalyticsDataRequestCondition
from alibabacloud_tea_openapi.models import Config

config = Config(
    access_key_id='LTAI4FyDFmKN************',
    access_key_secret='WF3onkl8cq3cTyVW8n************',
    region_id='cn-shanghai'
)


client = Client(config)

request = ListAnalyticsDataRequest()

#您的API Path
request.api_path = '/iot-cn-npk1v******/system/query/hist_dev_cnt_stat'
#您的API所在的实例ID
request.iot_instance_id = 'iot-cn-npk1v******'
#分页参数：页号
request.page_num = 1
#分页参数：页大小
request.page_size = 100
#您的业务相关的请求参数。Condition的配置说明，请参见下文的相关说明。
conditions = []

condition = ListAnalyticsDataRequestCondition("__instance_id__")
condition.operate = '='
condition.value = 'iot-public'
conditions.append(condition)

condition1 = ListAnalyticsDataRequestCondition("entityId")
condition1.operate = '='
condition1.value = 'all'
conditions.append(condition1)

condition2 = ListAnalyticsDataRequestCondition("statDate")
condition2.operate = '='
condition2.value = '20210221'
conditions.append(condition2)

request.condition = conditions

response = client.list_analytics_data(request)
print(response.body.data)
```

-   系统请求参数：

    |名称|类型|是否必传|示例值|描述|
    |--|--|----|---|--|
    |access\_key\_id|String|是|LTAI4FyDFmKN\*\*\*\*\*\*\*\*\*\*\*\*|登录物联网平台控制台，将鼠标移至账号头像上，然后单击**AccessKey管理**，获取AccessKey ID和AccessKey Secret。

**说明：** 如果使用RAM用户，您需授予该用户管理物联网平台的权限（AliyunIOTFullAccess），否则将连接失败。授权方法请参见[授权RAM用户访问物联网平台](/cn.zh-CN/权限管理/账号授权/RAM授权管理/RAM用户访问.md)。 |
    |access\_key\_secret|String|是|WF3onkl8cq3cTyVW8n\*\*\*\*\*\*\*\*\*\*\*\*|
    |region\_id|String|是|cn-shanghai|您的物联网平台服务所在地域ID。 在物联网平台控制台左上方可查看地域。RegionId的表达方法，请参见[地域和可用区]()。 |
    |api\_path|String|是|/iot-cn-npk1v\*\*\*\*\*\*/system/query/hist\_dev\_cnt\_stat|API路径。在**数据服务**的API列表下，单击API对应的**查看**，进入API详情页，可查看API Patch的值。更多信息，请参见[查看与使用](/cn.zh-CN/数据服务/使用数据服务.mdsection_mky_acn_k91)。|
    |page\_num|Integer|开启分页时必传|1|分页的页码。|
    |page\_size|Integer|开启分页时必传|100|每页显示结果的条数，最大值为100。|
    |iot\_instance\_id|String|是|iot-cn-npk1u\*\*\*\*\*\*|API所在的实例ID。|

-   业务相关的请求参数：

    |名称|类型|是否必传|说明|相关代码|
    |--|--|----|--|----|
    |ListAnalyticsDataRequestCondition|String|是|请求参数名称。|    ```
condition = ListAnayticsDataRequestCondition("__instance_id__")
    ``` |
    |operate|String|是|请求参数对应的操作符。可选：    -   `=`：指定请求参数为特定值。
    -   `BETWEEN`：指定请求参数为特定范围。
    -   `IN`：指定请求参数为多个值。
    -   `!=`：指定请求参数不可为特定值。
|    ```
condition.operate = '='
    ``` |
    |value|String|否|请求参数的赋值。**说明：** 当操作符为非`BETWEEN`时，该参数必传。

|    ```
condition.value = 'iot-public'
    ``` |
    |between\_start|String|否|请求参数表示范围时的起始值。**说明：** 当操作符为`BETWEEN`时，该参数必传。

|    ```
condition.between_start = '0'
    ``` |
    |between\_end|String|否|请求参数表示范围时的终止值。**说明：** 当操作符为`BETWEEN`时，该参数必传。

|    ```
condition.between_end = '1000'
    ``` |

    一个请求参数对应一个`Condition`。在API详情页，查看API的请求参数，您可配置指定数量的`Condition`。关于如何查看API请求参数的信息，请参见[查看与使用](/cn.zh-CN/数据服务/使用数据服务.mdsection_mky_acn_k91)。

    本文示例代码中，该API有3个请求参数（\_\_instance\_id\_\_、entityId、statDate分别对应`condition`、`condition 1`、`condition 2`）。


## 运行结果

-   成功：

    在对应API的详情页，您可查看返回参数的详细说明。具体操作，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。

    以下示例为调用API成功后的结果，即：从2021年2月21日起至调用API时，公共实例下的设备数量相关统计情况。

    ```
    {'HasNext': False, 'ResultJson': '[{"statDate":"20210221","actDevCnt":2942,"onlineDevCntCompare":0.00,"livelyDevCntCompare":8.99,"livelyDevCnt":1527,"onlineDevRate":23.08,"crtDevCnt":169025,"livelyDevRate":51.90,"crtDevCntCompare":0.08,"onlineDevCnt":679,"actDevRate":1.74,"actDevCntCompare":4.55}]', 'PageNum': 1, 'PageSize': 100}
    ```

-   失败：

    通过调用失败结果中的错误码，您可了解失败的原因。关于错误码更多信息，请参见[错误码](/cn.zh-CN/数据服务/错误码.md)。

    以下示例为调用API失败后的结果，即：参数`__instance_idd__`为无效的请求参数，将其更正为`__instance_id__`后，重新发起调用。

    ![Python调用失败](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9784885161/p250800.gif)


