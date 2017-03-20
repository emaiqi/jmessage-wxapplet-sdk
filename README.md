# jmessage-wxapplet-sdk集成指南

本文说明如何在小程序中集成JMessage。jmessage-wxapplet-sdk是JMessage专门为适配小程序应用而开发的，其功能基本涵盖所有[WEB SDK](https://docs.jiguang.cn/jmessage/client/im_sdk_js_v2/)所提供的功能


## 项目配置

socket合法域名：wss://ws.im.jiguang.cn

uploadFile合法域名：https://sdk.im.jiguang.cn

downloadFile合法域名：https://dl.im.jiguang.cn


## 使用

1.下载jmessage-wxapplet-sdk.js,移动到libs目录下

2.在app.js中引入：

```
var JMessage=require('./libs/jmessage-wxapplet-sdk-<version>.min.js')
```

新建JMessage对象：

```
var jim = new JMessage({
       // debug : true
    });
```

初始化连接：

```
 jim.init({
            "appkey"    : "<appkey>",
            "random_str": "<random_str>",
            "signature" : "<signature>",
            "timestamp" : "<timestamp>"
        }).onSuccess(function(data) {
          //TODO
        }).onFail(function(data) {
          //TODO
        });  
```

所有api操作跟WEB SDK类似，可以直接参考[WEB SDK API](https://docs.jiguang.cn/jmessage/client/im_sdk_js_v2/)

## 其他说明

1. 小程序不支持文件传输，所以单聊以及群聊文件发送相关api不可用

2. 发送图片(单聊和群聊)接口跟WEB SDK API有所差异

   ```
         //先通过小程序API获取图片
         wx.chooseImage({
                   count: 1, //
                   sizeType: ['original', 'compressed'], // 可以指定是原图还是压缩图，默认二者都有
                 sourceType: ['album', 'camera'], // 可以指定来源是相册还是相机，默认二者都有
                    success: function (res) {
                       var tempFilePaths = res.tempFilePaths[0]; //获取成功，读取文件路径
                          jim.sendSinglePic({
                             'target_username' : '<target_username>',
   			              'target_nickname' : '<target_nickname>',
   		                        	'appkey' : '<appkey>',
                                        'image' : tempFilePaths //设置图片参数
                              }).onSuccess(function(data,msg) {
                                 //TODO
                              }).onFail(function(data) {
                                 //TODO
                               });
                    }
             })
   ```
   ​

