# API服务开发 {#concept_244168 .concept}

API服务指可以将数据开发中的数据任务（使用SQL开发的数据任务）封装成API，方便开发者调用，既可以直接响应设备端请求，也可以用来做服务端数据对接。

生成API服务的方式有两种，通过数据任务生成API或在API服务目录下开发API服务。

## 方式一、生成API {#section_ddi_ffk .section}

1.  登录[物联网平台控制台](http://iot.console.aliyun.com/)。
2.  左侧导航栏选择 **数据分析** \> **数据开发** \> **数据开发** 。
3.  选择已经运行通过的数据任务，单击上方操作栏中的**生成API**。

    **说明：** 数据任务必须为运行成功任务。若无数据任务，请参考[开发任务](cn.zh-CN/数据开发/数据开发/开发任务.md#)编写SQL语句，完成数据任务的开发。

4.  在弹出页面中设置API名称，选择要保存API的目录（默认选项为API列表，也可以选择已有的自建目录）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156747545_zh-CN.png)

5.  单击**确定**，生成API。

    系统跳转至新创建的API任务，SQL已经进行转换，`where`语句后的查询条件变成参数形式，并默认展开属性参数设置面板。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156747546_zh-CN.png)


## 方式二、API服务开发 {#section_ddi_ffk_whb .section}

1.  登录[物联网平台控制台](http://iot.console.aliyun.com/)。
2.  左侧导航栏选择 **数据分析** \> **数据开发** \> **API服务** 。
3.  单击**API服务**后的“`+`”号图标新增服务开发文件夹。

    支持在API服务目录下新建一级文件夹，文件夹用于保存开发服务，可以添加、删除和编辑。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156747576_zh-CN.png)

4.  在已创建的文件夹名称后面，单击“`+`”号图标。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156747585_zh-CN.png)

5.  在弹出框中设置参数，并单击**确定**。

    |参数|描述|
    |--|--|
    |API名称|设置API名称。仅支持中文、英文大小写、数字、下划线（\_）、中划线（-）、英文括号（\(\)）和空格，不能为空且长度不超过20个字符。|
    |数据任务拷入|可选参数。     -   可以选择已运行成功的数据任务，作为生成API的数据模板。
    -   也可以不设置该参数，则系统使用默认的SQL模板。默认的SQL模板如下：

        ``` {#codeblock_ceb_7l9_o21}
select name,nickname,iot_id from ${system.device} where status != ${status} and name != ${name} limit ${pageNo} , ${pageSize}
        ```

 |

    创建API完成后，可修改API名称、或删除API。

6.  在编写查询SQL页面中，设置API相关参数。

    您可以编写SQL，并根据SQL中设置的变量，单击右上角**属性参数设置**（新建API完成后**属性参数设置**页面会默认打开），设置API属性参数。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156847607_zh-CN.png)

    参数说明如下：

    |参数|是否必填|说明|示例|
    |--|----|--|--|
    |API Path|是|API路径，用于后续调用API服务的路径。API路径的前一段部分由系统生成，您只需要填写后一段路径。|testNewApi|
    |描述|否|API描述。|无|

    |参数|说明|
    |--|--|
    |参数类型|根据请求参数的类型，选择对应的参数类型。例如请求参数的类型为String，则选择VARCHAR。|
    |是否必填|指调用API时，此参数是否必填。|
    |示例值|参数值的示例，可以为空。|
    |描述|描述请求参数，可以为空。|

    |参数|说明|
    |--|--|
    |参数类型|根据返回参数的类型，选择对应的参数类型。|
    |示例值|参数值的示例，可以为空。|
    |描述|描述返回参数，可以为空。|

    例如，查询所有已激活设备的名称、昵称、ID，有如下两种方式修改模板SQL：

    -   固定请求参数。例如从起始页开始查询，每页显示20条已激活设备的记录，则SQL语句如下：

        ``` {#codeblock_zao_6yk_q2z}
        select name,nickname,iot_id from ${system.device} where status != 0 limit 0 , 20;
        ```

        **说明：** `status != 0`表示设备状态为已激活。

        此时，在**属性参数设置**页面中，仅需设置属性和返回参数。

    -   直接封装模板SQL，通过**属性参数设置**设置属性、请求参数和返回参数。
7.  配置参数完成后，单击**保存**，并进行**语法校验**且需要校验成功。
8.  单击服务开发页面右上角**测试**，进行API测试。

    在API测试页面，若没有固定请求参数，则可以填写请求参数值，然后单击**开始测试**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156847621_zh-CN.png)

    查看是否成功获取**返回内容**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/203173/156196156847623_zh-CN.png)

9.  测试成功后，在服务开发页面右上角单击**发布**，发布API服务。

    发布成功后，可下载SDK，调用API服务。

    **说明：** API发布成功后，服务开发页面将不可编辑。

10. API发布成功后，参考[JAVA SDK调用示例](cn.zh-CN/数据开发/API服务/JAVA SDK调用示例.md#)调用API。

