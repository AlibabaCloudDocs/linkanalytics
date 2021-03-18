---
keyword: [数据分析, 数据服务, API, Java SDK]
---

# Java SDK调用示例

您可使用阿里云提供的Java SDK，来调用数据服务的API，从而更便捷地获取指定数据。您可添加包含Maven依赖的SDK，也可下载安装包到本地直接安装。本文以调用基础API为例，介绍Java SDK调用API的方法及示例。

## 前提条件

已开通数据分析功能，更多信息，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。

## 安装SDK

1.  安装Java开发环境。

    您可以从[Java 官方网站](http://developers.sun.com/downloads/)下载，并按说明安装Java开发环境。

2.  安装IoT Java SDK。

    1.  访问[Apache Maven 官网](http://maven.apache.org/)下载Maven软件。

    2.  安装IoT Java SDK。

        ```
                <dependency>
                    <groupId>com.aliyun</groupId>
                    <artifactId>tea-openapi</artifactId>
                    <version>0.0.11</version>
                </dependency>
                <dependency>
                    <groupId>com.aliyun</groupId>
                    <artifactId>iot20180120</artifactId>
                    <version>1.1.0</version>
                </dependency>
                <dependency>    
                    <groupId>com.alibaba</groupId>
                    <artifactId>fastjson</artifactId>
                     <version>1.2.61</version>
                </dependency>
        ```


## 发起调用

以下为调用**数据服务**下基础API历史至今设备数量相关统计的示例代码。您可参照参数说明，修改对应代码，调用指定的API。

```
import com.alibaba.fastjson.JSON;
import com.aliyun.iot20180120.Client;
import com.aliyun.iot20180120.models.*;
import com.aliyun.teaopenapi.models.Config;

public class JavaDemo {

    /**
     * 使用AccessKey ID和AccessKey Secret初始化账号Client
     * @param accessKeyId
     * @param accessKeySecret
     * @return Client
     * @throws Exception
     */
    public static Client createClient(String accessKeyId, String accessKeySecret) throws Exception {
        Config config = new Config();
        config.setAccessKeyId(accessKeyId);
        config.setAccessKeySecret(accessKeySecret);
        // 您的接入域名
        config.setEndpoint("iot.cn-shanghai.aliyuncs.com");
        return new Client(config);
    }

    public static void main(String[] args_) throws Exception {
        // 您的AccessKey ID和AccessKey Secret
        Client client = JavaDemo.createClient("LTAI4FyDFmKNBV**********", "WF3onkl8cq3cTyVW8nku**********"));

        ListAnalyticsDataRequest request = new ListAnalyticsDataRequest();
        // 您的API Path
        request.setApiPath("/iot-cn-npk1v******/system/query/hist_dev_cnt_stat");
        // 您的API所在实例ID
        request.setIotInstanceId("iot-cn-npk1v******");
        //分页参数：页号
        request.setPageNum(1);
        //分页参数：页大小
        request.setPageSize(100);
        List<ListAnalyticsDataRequest.ListAnalyticsDataRequestCondition> conditions = new ArrayList<>();
        //您的业务相关的请求参数。Condition的配置说明，请参见下文的相关说明。
        ListAnalyticsDataRequest.ListAnalyticsDataRequestCondition condition = new ListAnalyticsDataRequest
                .ListAnalyticsDataRequestCondition();
        condition.setFieldName("__instance_id__");
        condition.setOperate("=");
        condition.setValue("iot-public");
        conditions.add(condition);

        ListAnalyticsDataRequest.ListAnalyticsDataRequestCondition condition1 = new ListAnalyticsDataRequest
                .ListAnalyticsDataRequestCondition();
        condition1.setFieldName("entityId");
        condition1.setOperate("=");
        condition1.setValue("all");
        conditions.add(condition1);

        ListAnalyticsDataRequest.ListAnalyticsDataRequestCondition condition2 = new ListAnalyticsDataRequest
                .ListAnalyticsDataRequestCondition();
        condition2.setFieldName("statDate");
        condition2.setOperate("=");
        condition2.setValue("20210221");
        conditions.add(condition2);

                request.setCondition(conditions);
        ListAnalyticsDataResponse listAnalyticsDataResponse = client.listAnalyticsData(request);
        System.out.println(JSON.toJSONString(listAnalyticsDataResponse));    }
}
```

-   系统请求参数：

    |名称|类型|是否必传|示例值|描述|
    |--|--|----|---|--|
    |accessKeyId|String|是|LTAI4FyDFmKNBV\*\*\*\*\*\*\*\*\*\*|登录物联网平台控制台，将鼠标移至账号头像上，然后单击**AccessKey管理**，获取AccessKey ID和AccessKey Secret。

**说明：** 如果使用RAM用户，您需授予该用户管理物联网平台的权限（AliyunIOTFullAccess），否则将连接失败。授权方法请参见[授权RAM用户访问物联网平台](/cn.zh-CN/权限管理/账号授权/RAM授权管理/RAM用户访问.md)。 |
    |accessKeySecret|String|是|WF3onkl8cq3cTyVW8nku\*\*\*\*\*\*\*\*\*\*|
    |Endpoint|String|是|iot.cn-shanghai.aliyuncs.com|阿里云服务的API服务端地址。其中，地域需与物联网平台产品地域保持一致。在物联网平台控制台左上方可查看地域。RegionId的表达方法，请参见[地域和可用区]()。

本示例中，地域为华东2（cn-shanghai）。 |
    |apiPath|String|是|/iot-cn-npk1v\*\*\*\*\*\*/system/query/hist\_dev\_cnt\_stat|API路径。在**数据服务**的API列表下，单击API对应的**查看**，进入API详情页，可查看API Patch的值。更多信息，请参见[查看与使用](/cn.zh-CN/数据服务/使用数据服务.mdsection_mky_acn_k91)。|
    |iotInstanceId|String|是|iot-cn-npk1u\*\*\*\*\*\*|API所在的实例ID。|
    |pageNum|Integer|开启分页时必传|10|分页的页码。|
    |pageSize|Integer|开启分页时必传|100|每页显示结果的条数，最大值为200。|

-   业务相关的请求参数：

    |名称|类型|是否必传|说明|相关代码|
    |--|--|----|--|----|
    |FieldName|String|是|请求参数名称。|    ```
 condition.setFieldName("entityId");
    ``` |
    |Operate|String|是|请求参数对应的操作符。可选：    -   `=`：指定请求参数为特定值。
    -   `BETWEEN`：指定请求参数为特定范围。
    -   `IN`：指定请求参数为多个值。
    -   `!=`：指定请求参数不可为特定值。
|    ```
 condition.setOperate("=");
    ``` |
    |Value|String|否|请求参数的赋值。**说明：** 当操作符为非`BETWEEN`时，该参数必传。

|    ```
 condition.setValue("all");
    ``` |
    |BetweenStart|String|否|请求参数表示范围时的起始值。**说明：** 当操作符为`BETWEEN`时，该参数必传。

|    ```
 condition.setBetweenStart("0");
    ``` |
    |BetweenEnd|String|否|请求参数表示范围时的终止值。**说明：** 当操作符为`BETWEEN`时，该参数必传。

|    ```
condition.setBetweenEnd("100");
    ``` |

    一个请求参数对应一个`Condition`。在API详情页，查看API的请求参数，您可配置指定数量的`Condition`。关于如何查看API请求参数的信息，请参见[查看与使用](/cn.zh-CN/数据服务/使用数据服务.mdsection_mky_acn_k91)。

    本文示例代码中，该API有3个请求参数（\_\_instance\_id\_\_、entityId、statDate分别对应`condition`、`condition 1`、`condition 2`）。


## 运行结果

-   成功：

    在对应API的详情页，您可查看返回参数的详细说明。具体操作，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。

    以下示例为调用API成功后的结果，即：从2021年2月21日起至调用API时，公共实例下的设备数量相关统计情况。

    ```
    {"body":{"data":{"hasNext":false,"pageNum":1,"pageSize":200,"resultJson":"[{\"statDate\":\"20210221\",\"actDevCnt\":2942,\"onlineDevCntCompare\":0.00,\"livelyDevCntCompare\":8.99,\"livelyDevCnt\":1527,\"onlineDevRate\":23.08,\"crtDevCnt\":169025,\"livelyDevRate\":51.90,\"crtDevCntCompare\":0.08,\"onlineDevCnt\":679,\"actDevRate\":1.74,\"actDevCntCompare\":4.55}]"},"requestId":"6B78B8DB-EBDB-4451-BE30-893714******","success":true},"headers":{"access-control-allow-origin":"*","date":"Mon, 15 Mar 2021 07:24:01 GMT","content-length":"425","access-control-max-age":"172800","x-acs-request-id":"6B78B8DB-EBDB-4451-BE30-893714******","access-control-allow-headers":"X-Requested-With, X-Sequence, _aop_secret, _aop_signature","connection":"keep-alive","content-type":"application/json;charset=utf-8","access-control-allow-methods":"POST, GET, OPTIONS"}}
    ```

-   失败：

    通过调用失败结果中的错误码，您可了解失败的原因。关于错误码更多信息，请参见[错误码]()。

    以下示例为调用API失败后的结果，即：参数`__instance_idd__`为无效的请求参数，将其更正为`__instance_id__`后，重新发起调用。

    ![Java调用失败](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2910085161/p249798.gif)


