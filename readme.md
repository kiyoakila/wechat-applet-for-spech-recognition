# A wechat applet using Baidu API for speech recognition

## Introduction

On the client end press the "record" button. The applet will transcode your voice by ffmegp, and call the baidu-aip-sdk to output your speech content.

## Parameters
### client/pages/index/index.js

```javascript
const recorderManager = wx.getRecorderManager();

function sendRecord(src) {
  var obj = {
    // 需要替换为本地或外网的地址（server端服务映射的地址）
    url: "http://ai.xxx.com:3001/baiduAI2/recognition",
    filePath: src,
    name: "fffile",
    header: {
      'Content-Type': 'application/json'
    },
    success: function (result) {
      var data = JSON.parse(result.data);
      // msg 为最终语音识别的字符串
      var msg = data.result;
      // 获取当前页面对象
      var page = getCurrentPages()[0];
      page.setData({ msg: msg });
    },
    fail: function (err) {
      console.log(err);
    }
  };
  wx.uploadFile(obj)
}

```

### server/routes/aiSpeechRecognition.js

```javascript

// 设置APPID/AK/SK
var APP_ID = "xxx";
var API_KEY = "xxx";
var SECRET_KEY = "xxx";

```
