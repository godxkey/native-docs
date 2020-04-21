目前支付模块有支付宝、微信支付和苹果内购支付：

支付模块首先需要到各开放平台申请帐号,申请查看该[文档](http://ask.dcloud.net.cn/article/71)

## 支付宝支付配置

注: Linker Flags、framework添加方法参考该[文档](/5PlusDocs/usemodule/iOSModuleConfig/common.md)
 
1.配置库和资源文件
| 依赖库|系统库 |资源文件 | 
|  -:-  |  -:-  |  -:-  |
| liblibPayment.a，libalixpayment.a，AlipaySDK.framework|Security.framework，CoreMotion.framework，SystemConfiguration.framework，CFNetwork.framework，libc++.dylib| AlipaySDK.bundle |

2.配置支付平台参数

在工程中搜索 feature.plist 文件（位于PandoraApi.bundle中），在 Payment-> extend 节点下添加对应平台的配置

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/52440.png)

3.配置URL Schemes 

在URL Types 中添加配置： identifier 填写 alixpay ，URL Schemes 填写 alix[后面是您在支付宝平台申请的appid] ,如果没有该项按照图中的格式创建

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/52442.png)

**注意:**
iOS9.0以上版本需要在info.plist增加以下配置

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/52443.png)


## 微信支付配置
注: Linker Flags、framework添加方法参考该[文档](/5PlusDocs/usemodule/iOSModuleConfig/common.md)

1.配置库和资源文件
| 依赖库 | 系统库 | 资源文件 |
|  -:-  |  -:-  |  -:-  |
|liblibPayment.a, libwxpay.a, libWeChatSDK_pay.a | libsqlite3.0.dylib, libz.dylib, CoreTelephony.framework, SystemConfiguration.framework  |  |


2.配置支付平台参数

在工程中搜索 feature.plist 文件（位于PandoraApi.bundle中），在 Payment-> extend 节点下添加对应平台的配置

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/52440.png)



3.配置URL Schemes 
在URL Types 中添加配置： identifier 填写 weixin ，URL Schemes 填写wx[后面是您在微信平台申请的appkey] ,如果没有该项按照图中的格式创建

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/52441.png)

4.配置通用链接
HBuilderX2.3.4+ 版本需要配置 Universal Link在info.plist root 节点添加UniversalLinks项，值和微信开放平台配置的一致，参考如下：

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/42488.png)

查看工程里的AppDelegate.m文件里是否有下面的方法：

> //@Summary:通用链接
-(BOOL)application:(UIApplication *)application continueUserActivity:(NSUserActivity *)userActivity restorationHandler:(void(^)(NSArray<id<UIUserActivityRestoring>> * __nullable restorableObjects))restorationHandler {
    [PDRCore handleSysEvent:PDRCoreSysEventContinueUserActivity withObject:userActivity];
    restorationHandler(nil);
    return YES;
}

**注意:**

iOS9.0以上版本需要在info.plist增加以下配置

![](https://img.cdn.aliyun.dcloud.net.cn/nativedocs/5SDKiOS/pay/45099.png)
