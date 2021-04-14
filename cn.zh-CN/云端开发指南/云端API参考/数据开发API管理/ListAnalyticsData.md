# ListAnalyticsData

调用该接口执行数据服务API对应的查询任务，从而获取数据集里的指定数据。

## 使用限制

单阿里云账号调用该接口的每秒请求数（QPS）最大限制为500。

**说明：** RAM用户共享阿里云账号配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Iot&api=ListAnalyticsData&type=RPC&version=2018-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAnalyticsData|系统规定参数。取值：ListAnalyticsData。 |
|ApiPath|String|是|/iot-cn-npk1v\*\*\*\*\*\*/system/query/hist\_dev\_cnt\_stat|API路径。您可在**物联网平台** \> **数据分析** \> **数据服务**的API详情页面，查看**API Path**的值。更多信息，请参见[查看与使用](~~206247~~)。 |
|Condition.N.FieldName|String|是|testCode|对应服务API设置的请求参数名。 |
|Condition.N.Operate|String|是|=|比较运算符。

 仅支持`bt`、`eq`、`neq`、`rlike`、`in`或`nin`，及其对应的操作符`BETWEEN`、`=`、`!=`、`LIKE`、`IN`、`NIN`。

 您可在**物联网平台** \> **数据分析** \> **数据服务**的API详情页面，查看API请求参数的赋值情况，然后选择对应操作符。

 -   `BETWEEN`：请求参数赋值为特定范围。
-   `=`：请求参数赋值为特定值。
-   `!=`：请求参数赋值不为特定值。
-   `LIKE`：请求参数赋值以特定值为首。
-   `IN`：请求参数赋值属于特定集合。
-   `NIN`：请求参数赋值不属于特定集合。

 例如，数据集有6条记录（对应的`time`分别为`abcd`、`abce`、`abcf`、`abcg`、`aabc`和`abbc`），调用该接口时，`Condition.N.FieldName="time"`：

 -   如果`Condition.N.Operate="LIKE"`、`Condition.N.Value="abc"`，则返回`time=abcd`、`time=abce`、`time=abcf`和`time=abcg`的所有记录。
-   如果`Condition.N.Operate="IN"`、`Condition.N.Value="[abcd,abce,abcf]"`，则返回`time=abcd`、`time=abce`和`time=abcf`的所有记录。

 **说明：** 如果该参数取值为`BETWEEN`，则**Condition.N.BetweenStart**和**Condition.N.BetweenEnd**必传。如果该参数取值不为`BETWEEN`，则**Condition.N.Value**必传。 |
|IotInstanceId|String|是|iot-cn-npk1u\*\*\*\*\*\*|API所在的实例ID。 |
|IsoId|String|否|oxs\_iso\_id|逻辑隔离ID。请忽略该参数。 |
|PageSize|Integer|否|100|每页显示结果的条数，最大值为200。

 **说明：** 开启分页时必传。 |
|Condition.N.Value|String|否|4|比较值。即服务API请求参数的赋值。

 **说明：** 当**Condition.N.Operate**取值不为`BETWEEN`或`bt`时，该参数必传，且不传**Condition.N.BetweenStart**和**Condition.N.BetweenEnd**。 |
|Condition.N.BetweenStart|String|否|1|服务API请求参数表示范围时的起始值。

 **说明：** 当**Condition.N.Operate**取值为`BETWEEN`或`bt`时，该参数必传，且不传**Condition.N.Value**。 |
|Condition.N.BetweenEnd|String|否|5|服务API请求参数表示范围时的起始值。

 **说明：** 当**Condition.N.Operate**取值为`BETWEEN`或`bt`时，该参数必传，且不传**Condition.N.Value**。 |
|PageNum|Integer|否|1|分页的页码。 |

调用API时，除了本文介绍的该API的特有请求参数，还需传入公共请求参数。公共请求参数说明，请参见[公共参数文档](~~30561~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|Success|调用失败时，返回的错误码。更多信息，请参见[错误码](~~135176~~)。 |
|Data|Struct| |调用成功时，返回的数据信息。 |
|Count|Long|3|符合查询条件的记录总条数。 |
|HasNext|Boolean|false|符合条件的数据是否有下一页。

 -   **true**：有。
-   **false**：没有。 |
|PageNum|Integer|1|分页的页码。 |
|PageSize|Integer|100|每页显示结果的最大条数。 |
|ResultJson|String|\[\{\\"testCode\\":\\"TBB186\\",\\"testLevel\\":5,\\"testWorkYears\\":3,\\"testName\\":\\"王五\\"\},\{\\"testCode\\":\\"TBB1314\\",\\"testLevel\\":2,\\"testWorkYears\\":4,\\"testName\\":\\"李四\\"\},\{\\"testCode\\":\\"TBB8888\\",\\"testLevel\\":2,\\"testWorkYears\\":5,\\"testName\\":\\"熊大\\"\}\]"|符合条件的数据详情。 |
|ErrorMessage|String|insuficient auth:无访问权限|调用失败时，返回的错误信息。 |
|RequestId|String|7EC5B624-AF1B-4C4D-BA82-A02BA1\*\*\*\*\*\*|阿里云为该请求生成的唯一标识符。 |
|Success|Boolean|false|表示是否调用成功。

 -   **true**：调用成功。
-   **false**：调用失败。 |

## 示例

请求示例

```
http(s)://iot.cn-shanghai.aliyuncs.com/?Action=ListAnalyticsData
&ApiPath=/iot-cn-npk1v******/system/query/hist_dev_cnt_stat
&Condition.1.FieldName=testCode
&Condition.1.Operate==
&IotInstanceId=iot-cn-npk1u******
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<RequestId> 7EC5B624-AF1B-4C4D-BA82-A02BA1******</RequestId>
<Data>
    <ResultJson>[{\"testCode\":\"TBB186\",\"testLevel\":5,\"testWorkYears\":3,\"testName\":\"王五\"},{\"testCode\":\"TBB1314\",\"testLevel\":2,\"testWorkYears\":4,\"testName\":\"李四\"},{\"testCode\":\"TBB8888\",\"testLevel\":2,\"testWorkYears\":5,\"testName\":\"熊大\"}]"</ResultJson>
    <PageSize>100</PageSize>
    <PageNum>1</PageNum>
    <Count>3</Count>
    <HasNext>false</HasNext>
</Data>
<ErrorMessage>insuficient auth:无访问权限</ErrorMessage>
<Code>Success</Code>
<Success>false</Success>
```

`JSON`格式

```
{
    "RequestId": "7EC5B624-AF1B-4C4D-BA82-A02BA1******",
    "Data": {
        "ResultJson": "[{\"testCode\":\"TBB186\",\"testLevel\":5,\"testWorkYears\":3,\"testName\":\"王五\"},{\"testCode\":\"TBB1314\",\"testLevel\":2,\"testWorkYears\":4,\"testName\":\"李四\"},{\"testCode\":\"TBB8888\",\"testLevel\":2,\"testWorkYears\":5,\"testName\":\"熊大\"}]",
        "PageSize": 100,
        "PageNum": 1,
        "Count": 3,
        "HasNext": false
    },
    "ErrorMessage": "insuficient auth:无访问权限",
    "Code": "Success",
    "Success": false
}
```

