# iOS SDK接入

本文介绍iOS SDK的接入说明。

## 操作指南

### 使用前提
* 已创建应用，记录对应应用的**AppKey**和**AppSecret**。
* 已添加域名，**不在域名管理中的域名，sdk将无法解析**。
* 下载iOS SDK安装包。


### 开发环境
* 最低部署版本：iOS 10.0及以上。
* Xcode开发工具：12.0及以上。


### 使用说明

* 导入头文件
```oc
#import <UHttpDnsSDK/UHttpDnsSDK.h>
```

* 初始化
```oc
// 自定义serverUrl（不设置，默认使用UCloud HttpDns平台服务）
[[UHttpDnsManager shared] customServerUrl:@"http://xxx"];
// authId、authSecret在UCloud HttpDns平台申请
[[UHttpDnsManager shared] registerAuthId:@"xxx" authSecret:@"xxx"];
// 开启日志
[[UHttpDnsManager shared] consolePrintLogEnable:YES];
// 可开启是否缓存解析的IP
[[UHttpDnsManager shared] enableCacheIP:YES];
```

* 域名预解析
```oc
 [[UHttpDnsManager shared] preGetIPsWithDomains:@[xxx]];
```

* 域名解析（IPv4）
```oc
- (void)getIPV4ByDomain:(NSString *)domain returnBlock:(ReturnBlock)handler;
```

* 域名解析（IPv6）
```oc
- (void)getIPV6ByDomain:(NSString *)domain returnBlcok:(ReturnBlock)handler;
```

## SDK接口说明

### 初始化SDK
    
**接口描述** 

>  初始化SDK。

**接口示例**

```oc
- (void)registerAuthId:(NSString *)authId authSecret:(NSString *)authSecret;
```

**参数说明**

> authId：鉴权Id，UCloud HttpDns平台申请。
> authSecret：鉴权Secret，UCloud HttpDns平台申请。

-------

### 自定义服务器地址

**接口描述** 

>  自定义服务器地址，常用于私有化部署（默认使用UCloud HttpDns平台）。

**接口示例**

```oc
- (void)customServerUrl:(NSString *)url;
```
-------

### 域名预解析

**接口描述** 

>  在应用调用相关接口之前解析，提升速度。

**接口示例**

```oc
- (void)preGetIPsWithDomains:(NSArray <UDNSPreResolveModel *> *)domains;
```

**参数说明**

> domains: 需要解析的域名信息，UDNSPreResolveModel详情查看SDK定义。

-------

### 域名解析（IPv4）

**接口描述** 

>  域名解析为IPv4地址。

**接口示例**

```oc
- (void)getIPV4ByDomain:(NSString *)domain returnBlock:(ReturnBlock)handler;
```

**参数说明**

> domain：待解析的域名。
> returnBlock：解析结果回调。

-------

### 域名解析（IPv6）

**接口描述** 

>  域名解析为IPv6地址。

**接口示例**

```oc
- (void)getIPV6ByDomain:(NSString *)domain returnBlcok:(ReturnBlock)handler;
```

**参数说明**

> domain：待解析的域名。
> returnBlock：解析结果回调。

-------

### 开启IP缓存

**接口描述** 

> 开启后，域名解析成功的IP会被持久化缓存。

**接口示例**

```oc
- (void)enableCacheIP:(BOOL)enable;
```

**参数说明**

> enable: 是否开启IP持久化缓存。

-------

### 返回过期的IP

**接口描述** 

>  开启后，获取域名对应的解析IP时，过期IP也会被返回。

**接口示例**

```oc
- (void)enableExpiredIp:(BOOL)enable;
```

**参数说明**

> enable: 是否允许过期IP返回。

-------

### 清除所有缓存

**接口描述** 

>  清除所有缓存的IP。

**接口示例**

```oc
- (void)cleanAllCache;
```
-------

### 日志打印

**接口描述** 

>  SDK内部日志打印。

**接口示例**

```oc
- (void)consolePrintLogEnable:(BOOL)enable;
```

**参数说明**

> enable: 是否开启SDK日志打印。

-------

### SDK版本

**接口描述** 

>  SDK当前版本。

**接口示例**

```oc
+ (NSString *)sdkVersion;
```
-------

## 其他注意事项

其它接口的使用方法，请参考Demo中的示例。
        

	
