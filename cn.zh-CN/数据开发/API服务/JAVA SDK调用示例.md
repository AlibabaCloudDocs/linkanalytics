# JAVA SDK调用示例 {#concept_266261 .concept}

本文描述如何通过Java SDK，调用物联网平台**数据分析** \> **数据开发**中生成的API。物联网平台的Java SDK让开发人员可以方便地使用Java程序操作物联网平台。开发者可以使用Maven依赖添加SDK，也可以下载安装包到本地直接安装。

## 安装SDK {#section_gba_2an_rzm .section}

1.  安装Java开发环境。您可以从[Java官方网站](http://developers.sun.com/downloads/)下载，并按说明安装Java开发环境。
2.  安装IoT Java SDK。
    1.  访问[Apache Maven官网](http://maven.apache.org/)，下载Maven软件。
    2.  添加Maven项目依赖。IoT Java SDK的Maven依赖包坐标如下：

        ``` {#codeblock_lmr_909_ko9}
        <!-- https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-iot -->
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-iot</artifactId>
            <version>7.0.0</version>
        </dependency>
        ```

    3.  依赖公共包如下：

        ``` {#codeblock_p9l_m3q_pxt}
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
            <version>4.3.5</version>
        </dependency>
        ```


## 初始化SDK {#section_7ke_zgt_pc7 .section}

参考如下内容，初始化SDK。

**说明：** 以下示例以华东2地域及其服务接入地址为例。您在设置时，需使用您自己的物联网平台地域和对应的服务接入地址。

``` {#codeblock_rcl_85c_f7u}
String accessKey = "<your accessKey>";
String accessSecret = "<your accessSecret>";
DefaultProfile.addEndpoint("cn-shanghai", "cn-shanghai", "Iot", "iot.cn-shanghai.aliyuncs.com");
IClientProfile profile = DefaultProfile.getProfile("cn-shanghai", accessKey, accessSecret);
DefaultAcsClient client = new DefaultAcsClient(profile); //初始化SDK客户端
```

其中，<your accessKey\>为您账号的AccessKeyId， <your accessSecret\>为AccessKeyId对应的AccessKeySecret。您可在阿里云官网控制台AccessKey管理中创建或查看您的AccessKey。

## 发起调用 {#section_jfq_ep2_a5e .section}

以调用服务端订阅API接口，查询数据结果为例。

``` {#codeblock_r9a_bua_gre}
String apiSrn = "acs:iot:*:1271039834613374:serveapi/device/getDeviceCountByStatus";

InvokeDataAlgoServeApiRequest.Param param = new InvokeDataAlgoServeApiRequest.Param();
// 请求参数名称
param.setParamName("status");
// 在线状态
param.setParamValue("1");

InvokeDataAlgoServeApiRequest request = new InvokeDataAlgoServeApiRequest();
request.setApiSrn(apiSrn);
request.setParams(Arrays.asList(param));
// 请求方法 POST
request.setSysMethod(MethodType.POST);

try {
    InvokeDataAlgoServeApiResponse response = acsClient.getAcsResponse(request);

    System.out.println(response.getSuccess());
    System.out.println(response.getErrorMessage());

    // 服务API指定的SQL查询结果
    List<Map<Object, Object>> result = response.getData().getResultList();
    System.out.println(result);

} catch (ClientException ce) {
    ce.printStackTrace();
}
```

