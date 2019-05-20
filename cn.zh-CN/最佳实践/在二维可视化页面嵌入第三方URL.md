# 在二维可视化页面嵌入第三方URL {#concept_228079 .concept}

本文描述如何在物联网数据分析中的二维数据可视化场景中，嵌入第三方连接。例如，二维场景中有监控摄像头等设备，且设备本身具有自定义气泡弹框需求等场景，可以在二维场景中嵌入URL，在查看设备的运行状态、管理设备的同时查看监控画面。

实现此功能，需要二维数据可视化场景与IoT Studio中的Web可视化配合使用，详细步骤请见下文。

## 步骤一、创建产品并添加设备 {#section_d3v_7rf_32v .section}

1.  参考[创建产品](../../../../cn.zh-CN/用户指南/产品与设备/创建产品.md#)，创建一个产品。本文以test\_product为例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271946819_zh-CN.png)

2.  参考[新增物模型](../../../../cn.zh-CN/用户指南/产品与设备/物模型/新增物模型.md#)，在产品详情页面，为test\_product产品添加自定义功能。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271946823_zh-CN.png)

3.  参考[产品标签](../../../../cn.zh-CN/用户指南/产品与设备/标签.md#section_u23_ssb_wdb)，为test\_product产品添加标签。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271946826_zh-CN.png)

    其中，标签key设置为studioType，标签value设置为url。

4.  参考[单个创建设备](../../../../cn.zh-CN/用户指南/产品与设备/创建设备/单个创建设备.md#)，为产品添加设备。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271946827_zh-CN.png)


## 步骤二、创建二维数据可视化场景 {#section_6ts_4y7_7fj .section}

1.  参考[二维数据可视化设备定位](../../../../cn.zh-CN/空间数据可视化/二维数据可视化设备定位.md#)，为设备设置地理位置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271946828_zh-CN.png)

2.  参考[二维数据可视化](../../../../cn.zh-CN/空间数据可视化/二维数据可视化.md#)，使用test\_product产品创建一个二维数据可视化场景。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271946939_zh-CN.png)

3.  设置设备的WEB\_URL属性的值为设备需要链接到的第三方页面地址。可以使用**在线调试**功能，上报属性值。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271947168_zh-CN.png)

    添加第三方链接后，单击二维数据场景中设备气泡后，如下所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271947169_zh-CN.png)


## 步骤三、IoT Studio可视化大屏搭建 {#section_h8r_aut_0kf .section}

IoT Studio可视化相关详细内容，请参考[Web可视化开发](https://help.aliyun.com/document_detail/110475.html)。

1.  拖动二维数据可视化场景（**地图**组件）到IoT Studio大屏中，占满整个屏幕。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271947112_zh-CN.png)

2.  添加一个**iframe**组件到大屏中，用于在点击设备气泡时，弹出一个第三方窗口。

    同时为了能够在不需要的时候关闭第三方窗口，需要添加一个**关闭**按钮到**iframe**的右上角。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834271947113_zh-CN.png)

3.  配置变量的联动关系。

    为了点击设备气泡的时候，能够打开第三方地址，需要设置地图和iframe组件的交互关系，让iframe组件中设置的地址能够从设备传入iframe。

    1.  单击地图，新增一个**交互**，并设置动作为赋值给变量。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047146_zh-CN.png)

    2.  新增一个变量。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047173_zh-CN.png)

        设置变量的名称，默认值设置为第三方URL。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047217_zh-CN.png)

    3.  配置变量。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047182_zh-CN.png)

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047194_zh-CN.png)

4.  单击**iframe**组件，配置关联链接。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047196_zh-CN.png)

    在弹出框中单击**绑定变量**，选择已配置好的第三方链接变量。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047198_zh-CN.png)

5.  因为只有点击设备气泡时，才显示第三方窗口，并且第三方窗口显示后，才可看到关闭按钮，因此需要默认隐藏组件。关闭**iframe**组件和**按钮**组件的可见性。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047199_zh-CN.png)

6.  单击地图，配置隐藏组件与地图的交互关系，实现单击设备气泡时，弹出三方页面和关闭按钮的功能。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047203_zh-CN.png)

7.  为**按钮**组件添加交互，实现单击关闭按钮后关闭iframe。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047205_zh-CN.png)

8.  在界面右上方单击**保存**，然后单击**预览**，查看已配置完成的Web可视化大屏。

    单击设备气泡，在弹出窗口中单击第三方连接，则显示第三方弹窗，单击**关闭**按钮，可关闭弹窗。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190853/155834272047212_zh-CN.png)


