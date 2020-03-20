---
title: Frida Skill：奇技淫巧
date: 2020-03-07 17:22:48
categories:
- [Frida, Skill]

tags:
- Frida
---







## 遍历Java List

`requestHeaders`是一个Java的List对象，遍历其内容如下：

```javascript
log += "  request.headers: " + rObject.$methods.find("toString").call(rObject, requestHeaders) + "\n";
for (var i = 0; i < requestHeaders.size(); i++)
  log += "    headers[" + i + "]: " + requestHeaders.get(i) + "\n";
```

输出：

```
request.headers: [com.sankuai.meituan.retrofit2.Header@a671e8]
  headers[0]: com.sankuai.meituan.retrofit2.Header@a671e8
```





## Hook Native

静态注册或动态注册的Native函数，第二个参数总是一个`jobject`，标识了调用者的信息；

例如Java层有以下声明代码：

```java
private native String TestNative(int arg1, int arg2, String arg3);
```

在Frida hook时：

```javascript
const nativeHook_TestNative = {
  onEnter: function (args) {
    this.env = args[0];
    //this.caller = args[1]; // jobject of the caller.
    this.arg1 = args[2];
    this.arg2 = args[3];
    this.arg3 = args[4];
    this.tag = "nativeHook_TestNative";
    this.log = "";
    this.log += "> - - - - - - - - <\n";
    this.log += this.tag + " Enter.\n";
    this.log += "  JNIEnv: " + this.env + "\n";
    this.log += "  arg1: " + this.arg1 + "\n";
    this.log += "  arg2: " + this.arg2 + "\n";
    this.log += "  arg3: " + this.arg3 + ", " + GetStringUTFChars(this.env, this.arg3, NULL).readCString() + "\n";
    console.log(this.log);
  },
  onLeave: function (ret) {
    const tid = gettid();
    this.log = this.tag + " Leave.\n";
    this.log += "  ret: " + ret + ", str:" + GetStringUTFChars(this.env, ret, NULL).readCString() + "\n";
    this.log += "^ - - - - - - - - ^\n";
    console.log(this.log);
  }
};
```