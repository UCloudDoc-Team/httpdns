
# UCloud HttpDns iOS SDK 接入文档

| 日期 | 版本 | 说明 |
| --- | --- | --- |
| 2021-12-08 | 1.0.0 | UCloud HttpDns域名解析iOS SDK。 |

## 一、目录
  - [一、目录](#一、目录)
  - [二、接入说明](#二、接入说明)
  - [三、SDK接口说明](#三、sdk接口说明)
      - [3.0 初始化SDK](#3-0初始化-sdk)
      - [3.1 自定义服务器地址](#3-1自定义服务器地址)
      - [3.2 域名预解析](#3-2域名预解析)
      - [3.3 域名解析（IPv4）](#3-3域名解析（-ipv4）)
      - [3.4 域名解析（IPv6）](#3-4域名解析（-ipv6）)
      - [3.5 开启IP缓存](#3-5开启-ip缓存)
      - [3.6 返回过期的IP](#3-6返回过期的-ip)
      - [3.7 清除所有缓存](#3-7清除所有缓存)
      - [3.8 日志打印](#3-8日志打印)
      - [3.9 SDK版本](#3-9-sdk版本)
  - [四、其他注意事项](#四、其他注意事项)

## 二、接入说明

开发环境：
* 最低部署版本：iOS 10.0及以上。
* Xcode开发工具：12.0及以上。

集成方式：

* 将`UHttpDnsSDK.xcframework`拖拽到Xcode工程内（需要勾选Copy items if needed选项）。
* 点击项目target -> General -> Frameworks,Libraries,and Embedded Content -> UHttpDnsSDK.xcframework，在Embed选项下，选择`Embed & Sign`。

-------

**使用步骤：**

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

## 三、SDK接口说明

#### 3.0 初始化SDK
    
**接口示例**

```oc
/**
 *  @abstract 初始化SDK
 *
 *  @param authId 鉴权Id，UCloud HttpDns平台申请。
 *  @param authSecret 鉴权Secret，UCloud HttpDns平台申请。
 */
- (void)registerAuthId:(NSString *)authId authSecret:(NSString *)authSecret;
```

#### 3.1 自定义服务器地址

**接口示例**

```oc
/**
 *  @abstract 自定义服务器地址，常用于私有化部署（默认使用UCloud HttpDns平台）
 *
 *  @param url 自定义服务器地址
 */
- (void)customServerUrl:(NSString *)url;
```
-------

#### 3.2 域名预解析

**接口示例**

```oc
/**
 *  @abstract 域名预解析（注意：只有开启域名缓存时，才有效）
 *
 *  @param domains 需要解析的域名信息，UDNSPreResolveModel详情查看SDK定义。
 */
- (void)preGetIPsWithDomains:(NSArray <UDNSPreResolveModel *> *)domains;
```

#### 3.3 域名解析（IPv4）

**接口示例**

```oc
/**
 *  @abstract 获取域名解析IP（IPv4）
 *
 *  @param domain 需要解析的域名
 *  @param returnBlock 解析结果回调。
 */
- (void)getIPV4ByDomain:(NSString *)domain returnBlock:(ReturnBlock)handler;
```

#### 3.4 域名解析（IPv6）

**接口示例**

```oc
/**
 *  @abstract 获取域名解析IP（IPv6）
 *
 *  @param domain 需要解析的域名
 *  @param returnBlcok 解析结果回调。
 */
- (void)getIPV6ByDomain:(NSString *)domain returnBlcok:(ReturnBlock)handler;
```

#### 3.5 开启IP缓存

**接口示例**

```oc
/**
 *  @abstract 是否允许缓存IP（开启后，域名解析时返回缓存命中的值）
 *
 *  @param enable 开关
 */
- (void)enableCacheIP:(BOOL)enable;
```

#### 3.6 返回过期的IP

**接口示例**

```oc
/**
 *  @abstract 开启后，获取域名对应的解析IP时，过期IP也会被返回
 *
 *  @param enable 开关
 */
- (void)enableExpiredIp:(BOOL)enable;
```

#### 3.7 清除所有缓存

**接口示例**

```oc
/**
 *  @abstract 清除所有缓存的IP
 */
- (void)cleanAllCache;
```

#### 3.8 日志打印

**接口示例**

```oc
/**
 *  @abstract 控制台输出日志开关
 *
 *  @param enable 日志输出开关
 */
- (void)consolePrintLogEnable:(BOOL)enable;
```

#### 3.9 SDK版本

**接口示例**

```oc
/**
 *  @abstract SDK版本
 */
+ (NSString *)sdkVersion;
```

## 四、其他注意事项

其它接口的使用方法，请参考Demo中的示例。
        

	
