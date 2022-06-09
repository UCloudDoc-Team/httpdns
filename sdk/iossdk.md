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

#### 导入头文件
```oc
#import <UHttpDnsSDK/UHttpDnsSDK.h>
```

#### 初始化
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

#### 域名预解析
```oc
 [[UHttpDnsManager shared] preGetIPsWithDomains:@[xxx]];
```

#### 域名解析（IPv4）
```oc
- (void)getIPV4ByDomain:(NSString *)domain returnBlock:(ReturnBlock)handler;
```

#### 域名解析（IPv6）
```oc
- (void)getIPV6ByDomain:(NSString *)domain returnBlcok:(ReturnBlock)handler;
```

## SDK接口说明

### 初始化SDK
    
#### 接口说明

```oc
/**
 *  @abstract 初始化SDK
 *
 *  @param authId 鉴权Id，UCloud HttpDns平台申请。
 *  @param authSecret 鉴权Secret，UCloud HttpDns平台申请。
 */
- (void)registerAuthId:(NSString *)authId authSecret:(NSString *)authSecret;
```

### 自定义服务器地址

#### 接口说明

```oc
/**
 *  @abstract 自定义服务器地址，常用于私有化部署（默认使用UCloud HttpDns平台）
 *
 *  @param url 自定义服务器地址
 */
- (void)customServerUrl:(NSString *)url;
```
-------

### 域名预解析

#### 接口说明

```oc
/**
 *  @abstract 域名预解析（注意：只有开启域名缓存时，才有效）
 *
 *  @param domains 需要解析的域名信息，UDNSPreResolveModel详情查看SDK定义。
 */
- (void)preGetIPsWithDomains:(NSArray <UDNSPreResolveModel *> *)domains;
```

### 域名解析（IPv4）

#### 接口说明

```oc
/**
 *  @abstract 获取域名解析IP（IPv4）
 *
 *  @param domain 需要解析的域名
 *  @param returnBlock 解析结果回调。
 */
- (void)getIPV4ByDomain:(NSString *)domain returnBlock:(ReturnBlock)handler;
```

### 域名解析（IPv6）

#### 接口说明

```oc
/**
 *  @abstract 获取域名解析IP（IPv6）
 *
 *  @param domain 需要解析的域名
 *  @param returnBlcok 解析结果回调。
 */
- (void)getIPV6ByDomain:(NSString *)domain returnBlcok:(ReturnBlock)handler;
```

### 开启IP缓存

#### 接口说明

```oc
/**
 *  @abstract 是否允许缓存IP（开启后，域名解析时返回缓存命中的值）
 *
 *  @param enable 开关
 */
- (void)enableCacheIP:(BOOL)enable;
```

### 返回过期的IP

#### 接口说明

```oc
/**
 *  @abstract 开启后，获取域名对应的解析IP时，过期IP也会被返回
 *
 *  @param enable 开关
 */
- (void)enableExpiredIp:(BOOL)enable;
```

### 清除所有缓存

#### 接口说明

```oc
/**
 *  @abstract 清除所有缓存的IP
 */
- (void)cleanAllCache;
```

### 日志打印

#### 接口说明

```oc
/**
 *  @abstract 控制台输出日志开关
 *
 *  @param enable 日志输出开关
 */
- (void)consolePrintLogEnable:(BOOL)enable;
```

### SDK版本

#### 接口说明

```oc
/**
 *  @abstract SDK版本
 */
+ (NSString *)sdkVersion;
```

## 其他注意事项

其它接口的使用方法，请参考Demo中的示例。
        

	

        

	
