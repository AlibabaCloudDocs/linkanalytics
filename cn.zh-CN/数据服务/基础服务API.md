# 基础服务API

基础服务API分为设备原始数据API和系统指标数据API，系统指标数据API由系统预置，可以直接查看并调用。当产品中有设备上报数据时，将生成设备原始数据API，您可以调用来获取设备数据。本文介绍如何查看基础服务API。

## 前提条件

查看设备原始数据API，需已创建产品和设备，并备份。具体操作，请参见[数据存储备份]()。

## 操作步骤

1.  登录[物联网平台控制台](http://iot.console.aliyun.com/)。

2.  在实例概览页面，找到对应的数据型实例，单击实例进入实例详情页面。

3.  在左侧导航栏，选择**数据分析** \> **数据服务**。

4.  在**基础服务API**页面，查看设备原始数据API和系统指标数据API。

    -   设备原始数据API

        当产品中有设备上报数据时，将生成设备原始数据API。您可以调用该API查看指定产品中设备上报的历史数据。

        -   API 名称为：`${productName}原始数据查询`，`${productName}`为产品名称。
        -   API Path为：`/${productKey}/rawDate/get`，`${productKey}`为产品的唯一标识。
        如下图所示：

        ![设备上报的原始数据API](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4502072261/p280188.png)

    -   系统指标数据API

        由系统预置，您可以调用该API来查看实例中所有设备的运行情况。已提供的系统指标数据API，如下表所示：

        |API名称|API Path|说明|
        |-----|--------|--|
        |任意时间段内每小时设备数量相关统计|/iot-060a\*\*\*\*/system/query/hourly\_slot\_dev\_cnt\_stat|统计实例中每小时在线设备的数量。|
        |任意时间段内每小时设备上报事件数统计|/iot-060a\*\*\*\*/system/query/hourly\_slot\_dev\_event\_cnt\_stat|统计实例中每小时设备上报的事件数量。|
        |任意时间段内每日设备上报事件数统计|/iot-060a\*\*\*\*/system/query/daily\_slot\_dev\_event\_cnt\_stat|统计每日设备上报的事件数量。|
        |任意时间段内每小时设备连接次数统计|/iot-060a\*\*\*\*/system/query/hourly\_slot\_dev\_connect\_cnt\_stat|统计每小时设备的连接次数。|
        |任意时间段内每小时设备在线时长统计|/iot-060a\*\*\*\*/system/query/hourly\_slot\_dev\_online\_time\_stat|统计每小时设备的在线时长。|
        |任意时间段内每日设备上下行消息统计|/iot-060a\*\*\*\*/system/query/daily\_slot\_dev\_fee\_msg\_stat|统计每日设备的上下行消息。|
        |任意时间段内每日设备连接次数统计|/iot-060a\*\*\*\*/system/query/daily\_slot\_dev\_connect\_cnt\_stat|统计每日设备的连接次数。|
        |任意时间段内每小时设备上下行消息统计|/iot-060a\*\*\*\*/system/query/hourly\_slot\_dev\_fee\_msg\_stat|统计每小时设备的上下行消息。|
        |任意一日设备SDK版本分布排行|/iot-060a\*\*\*\*/system/query/1d\_dev\_cnt\_sdk\_dist|查询任意一日设备的SDK版本。|
        |任意时间段内每日设备在线时长统计|/iot-060a\*\*\*\*/system/query/daily\_slot\_dev\_online\_time\_stat|统计每日设备的在线时长。|
        |历史至今设备SDK版本分布排行|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_sdk\_dist|查询设备历史至今的SDK版本。|
        |历史至今设备连网协议分布排行|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_connect\_protocol\_dist|查询设备历史至今的连网协议。|
        |任意一日设备连网协议分布排行|/iot-060a\*\*\*\*/system/query/1d\_dev\_cnt\_connect\_protocol\_dist|查询任意一日设备的连网协议。|
        |任意一日设备连网方式分布排行|/iot-060a\*\*\*\*/system/query/1d\_dev\_cnt\_connect\_mode\_dist|查询任意一日设备的连网方式。|
        |历史至今设备连网方式分布排行|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_connect\_mode\_dist|查询设备历史至今的连网方式。|
        |历史至今设备品类分布排行|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_category\_dist|查询设备历史至今的种类。|
        |任意一日设备品类分布排行|/iot-060a\*\*\*\*/system/query/1d\_dev\_cnt\_category\_dist|查询设备任意一日的种类。|
        |历史至今设备省份区域分布排行|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_district\_dist\_rank|查询设备历史至今的省份区域。|
        |任意一日设备区域分布排行|/iot-060a\*\*\*\*/system/query/1d\_dev\_cnt\_district\_dist\_rank|查询设备任意一日的省份区域。|
        |历史至今地区设备数统计|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_district\_dist\_detail|查询设备历史至今的地区数量。|
        |任意1日地区设备数统计|/iot-060a\*\*\*\*/system/query/1d\_dev\_cnt\_district\_dist\_detail|查询任意一日设备的地区数量。|
        |历史至今设备数量相关统计|/iot-060a\*\*\*\*/system/query/hist\_dev\_cnt\_stat|统计历史至今设备的数量。|
        |任意时间段内每日设备数量相关统计|/iot-060a\*\*\*\*/system/query/slot\_1d\_dev\_cnt\_stat|统计每日设备的数量。|

    **说明：** 单击对应API右侧的**查看**，可以查看API的**基础信息**、**API监控**和**参数**。更多信息，请参见[使用数据服务](/cn.zh-CN/数据服务/使用数据服务.md)。


