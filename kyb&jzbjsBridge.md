
## 款爷邦&金主邦jsBridge文档
> 款爷帮的js调用，和开心淘调用方式使用同一种，接口名和参数不同  
> 调用App的jsBridge window对象为  `__SHANGHAIWEICHUANG_KUANYEBANG__web2app__`   
> 回调给js 的函数，调用对象为 `__SHANGHAIWEICHUANG_KUANYEBANG__app2web__`    
> 使用函数传递过来的callback函数
---
> 唯一的不同地方是：
> 金主邦使用 `__SHANGHAIWEICHUANG_JINZHUBANG__web2app__ ` 
> 其他的都一样
---
---
## 文档 目录
>点击快速跳转至指定接口

### 1.[**款爷邦2.0接口**](#款爷帮2.0新增接口)
---
---

### 1.分享连接

> share(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| title    | 是    | 分享标题     |
| desc    | 是    | 分享描述     |
| link    | 是    | 分享跳转的连接     |
| imgUrl    | 是    | 分享连接的缩略图     |
| way    | 是    | 标示分享到朋友圈，还是发送给朋友  wxTimeline ---分享到朋友圈，其他值为分享给朋友     |
| callback    | 是    | App 调用js的函数对象     |

>回调结果 以key:value 的形式  
|参数 | 是否必填 | 类型| 释义 |
| -------- | --------|--- | -------- |
| code    | 是   | number  | 返回状态 0 为分享成功，-1为分享失败，-2 为用户取消分享 -3:用户未安装微信|
| msg    | 是    | String | 错误信息    |

```java
{code:'0',msg:'参数错误'}
```


调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.share("{title:'款爷帮分享',//分享标题
        desc:'http://baidu.com',//分享描述
        link:'http://baidu.com',//分享跳转的连接
        imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1536565376247&di=2e3be825e12331d268301f962a052194&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01f09e577b85450000012e7e182cf0.jpg%401280w_1l_2o_100sh.jpg',//分享连接前面的缩略图
        way:'wxTimeline'}"// 标示分享到朋友圈，还是发送给朋友  wxTimeline ---分享到朋友圈，其他值为分享给朋友
        );
        }

```

### 2.分享海报

> sharePoster(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| imgUrl    | 是    | 分享的海报图url     |
| way    | 是    | 标示分享到朋友圈，还是发送给朋友  wxTimeline ---分享到朋友圈，其他值为分享给朋友     |
| callback    | 是    | App 调用js的函数对象     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | -----|--|--- | -------- |
| code    | 是 | number    | 返回状态 0 为分享成功，-1为分享失败，-2 为用户取消分享|
| msg    | 是  | String   | 错误信息    |

```java
{code:'0',msg:'参数错误'}
```

调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.sharePoster("{callback:'',
        imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1536565376247&di=2e3be825e12331d268301f962a052194&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01f09e577b85450000012e7e182cf0.jpg%401280w_1l_2o_100sh.jpg',//分享海报的图片
        way:'wxTimeline'}"// 标示分享到朋友圈，还是发送给朋友  wxTimeline ---分享到朋友圈，其他值为分享给朋友
        );
        }

```

### 3.显示一个Toast

> showToast(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| content    | 是    | 要提示的内容     |



调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.showToast("{content:'要显示的内容'}"
        );

```

### 4.保存海报到相册

> saveImg(String data)

>调用参数
|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| imgUrl    | 是    | 要保存的图片url     |
| callback    | 否   | 为空则不回调结果     |

>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | -------|---|- | -------- |
| code    | 是  | number   | 返回状态 0 保存成功，-1为保存失败|
| msg    | 是  | String   | 错误信息    |

调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.saveImg("{callback:'',imgUrl:'图片地址'}"
        );

```
### 5.刷新当前页面

> refreshWebView()



不需要参数



调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.refreshWebView();

```

### 6.加载指定页面

> openWebPage(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| link    | 是    | 要加载的url     |



调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.openWebPage("{url:'baidu.com'}"
        );

```

### 7.回退到上一页

> goBack()



不需要参数



调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.goBack();

```

### 8.保存一个字符串到本地持久化

> saveString(String data)

> 调用参数

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| key    | 是    | 要保存的key 唯一标识     |
| content    | 是    | 要保存的内容     |
| callback    | 否   | 为空则不回调结果     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ----|---- | -------- |
| code    | 是  | number   | 返回状态 0 保存成功，-1为保存失败|
| msg    | 是  | String   | 错误信息    |


调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.saveString("{key:'baidu.com',content:'内容',callback:''}"
        );

```

### 9.从android本地储存中获取之前存入的字符串值

> getString(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| key    | 是    | 要保存的key 唯一标识     |
| callback    | 是    | 回调函数     |

>回调结果 以key:value 的形式  
```java
{result:''}
```



调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.getString("{key:'baidu.com',callback:'回调函数'}"
        );

```

### 10.调起微信支付

> wxPay(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| appId    | 是    | 微信开放平台审核通过的应用APPID    |
| partnerId    | 是    | 微信支付分配的商户号   |
| prepayId    | 是    | 预支付交易会话 微信返回的支付交易会话ID     |
| nonceStr    | 是    | 随机字符串，不长于32位     |
| timeStamp    | 是    |时间戳     |
| sign    | 是    | 签名    |
| callback    | 是    | 回调函数     |

>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0 为支付完成，  -1 错误 可能的原因：签名错误、未注册APPID、项目设置APPID不正确、注册的APPID与设置的不匹配、其他异常等  -2 用户取消 无需处理。发生场景：用户不支付了，点击取消 -3 传递给app的参数错误 -4用户未安装微信|
| msg    | 是  | String   | 支付失败的错误信息    |

```java
{code:'0',msg:'参数错误'}
```



调用方式
```java
 window.__SHANGHAIWEICHUANG_KUANYB__web2app__.wxPay("{appId:'wx684f1d41b0d691d9',partnerId:'1514386351',prepayId:'',nonceStr:'',timeStamp:'',sign:'',callback:''}");

```

### 11.调起自带浏览器打开一个连接

> openWhithLocalBrowser(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| link    | 是    | 需要使用自带浏览器打开的连接    |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0打开成功 -1 打开失败|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('openWhithLocalBrowser',{link:'http://baidu.com',callback:'b'},function(result){},function(result){
                 
              })
```

---
---
<a name="款爷帮2.0新增接口"></a>
## 款爷帮2.0新增接口

### 12.调用app初始化推送通知

> initUMPush(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| uid    | 是    | 用来标示推送用户的唯一标示，使用服务端的uid    |
| islogin    | 是    | 1.是注册，2,是取消注册    |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0初始化成功 -1 初始化失败|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('initUMPush',{uid:'123456',callback:'b',islogin:'1'},function(result){},function(result){
                 
              })
```

### 13.用新界面打开一个连接

> openWhithNewPage(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| link    | 是    | 需要使用新页面打开的连接    |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0打开成功 -1 打开失败|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('openWhithNewPage',{link:'http://baidu.com',callback:'b'},function(result){},function(result){
                 
              })
```



### 14.开启或关闭推送开关

> openNotifySetting(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| uid    | 是    | 用来标示推送用户的唯一标示，使用服务端的uid    |
| isOpen    | 是    | 1.是开，2,是关    |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0打开成功 -1 打开失败|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('openNotifySetting',{isopen:'1',uid:'abc',callback:'b'},function(result){},function(result){
                 
              })
```

### 15.获取推送开关状态

> getNotifyStatus(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 1已经打开 0 未打开|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('getNotifyStatus',{callback:'b'},function(result){},function(result){
                 
              })
```

### 16.关闭当前页面

> finishCurrentPage(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0 关闭成功，-1 关闭失败|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('finishCurrentPage',{callback:'b'},function(result){},function(result){
                 
              })
```

### 17.清除缓存

> clearCache(String data)

|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| callback    | 是    | 回调函数     |


>回调结果 以key:value 的形式  
|参数 | 是否必填|类型 | 释义 |
| -------- | ------|-- | -------- |
| code    | 是 | number    | 返回状态 0 成功，-1 失败|
| msg    | 是  | String   |成功或者失败的返回信息    |

调用方式
```java
web2app('clearCache',{callback:'b'},function(result){},function(result){
                 
              })
```

### 18.七牛图片上传

> updateImgByQiniu(String data)



|参数 | 是否必填 | 释义 |
| -------- | -------- | -------- |
| key    | 是    | JSONArray格式 -  存放多个图片key  -保存在服务器上的资源唯一标识，请参阅键值对  也是用来判断哪一张图片没有上传成功  |
| filePath    | 是    | 文件路径  JSONArray格式 存放多个图片路径     |
| token    | 是    | 服务端返回的七牛token  |
| callback    | 是    | App 调用js的函数对象     |
```java
{
    "filePath": [
        "/storage/emulated/0/Pictures/PIC-20190305-1548021063004719.png"
    ],
    "key ": ["key1","key2"],
    "token": "token ",
		"callback": "callback "
}
```

>回调结果 以key:value 的形式  
>由于上传是异步操作，所以不能保证回调时效，每上传一张就回调一次结果，由key 来标示哪一张图片，直至七牛不再回调上传结果
|参数 | 是否必填 | 类型| 释义 |
| -------- | --------|--- | -------- |
| code    | 是   | number  | 返回状态 0 为上传成功，-1为上传失败|
| msg    | 是    | String | 错误信息    |
| key    | 是    | String | 上传图片时传入的key    |
| path    | 是    | String | 如果上传成功 值不为空，否则值为空 null   |

```java
{code:'0',msg:'参数错误',path:'path',key:'keyValue'}
```
