---
layout: default
---

## Welcome to another page

[back](./)

  <div class="ms-list">
  <h2>h5调用Native方法（js）</h2>
  <ul>
      <li>
          <a class="btn" href="javascript:;" id="share">分享url</a>
          <div class="text" id="share_back">分享结果</div>
      </li>

      <li>
          <a class="btn" href="javascript:;" id="sharePoster">分享海报</a>
          <div class="text" id="sharePoster_back">分享海报结果</div>
      </li>
      <li>
          <a class="btn" href='https://kxtapp.oss-cn-zhangjiakou.aliyuncs.com/KxtApp_17.apk'>直接访问下载链接</a>
          <div class="text">应用内下载apk 下载链接</br>
              https://kxtapp.oss-cn-zhangjiakou.aliyuncs.com/KxtApp_17.apk
          </div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="saveImg">保存海报</a>
          <div class="text" id="saveImg_back">保存海报回调</div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="showToast">显示一个toast</a>
          <div class="text">我是要显示的内容</div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="refreshWebView">刷新当前页</a>
          <div class="text" id="refreshWebView_back">刷新当前页面</div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="loadUrl">加载指定页面</a>
          <div class="text" id="loadUrl_back">http://baidu.com</div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="goBack">回退到上一页</a>
          <div class="text">回退到上一页</div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="getString">从app获取之前存入的一个字符串</a>
          <div id="getStringBak" class="text"></div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="saveString">存入一个字符串</a>
          <div class="text" id="saveString_back">key:'abc',content:'getbak'</div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="wxPay">微信支付</a>
          <div class="text" id="wxPay_back"></div>
      </li>
      <li>
          <a class="btn" href="javascript:;" id="openWhithLocalBrowser">用自带浏览器打开url</a>
          <div class="text" id="openWhithLocalBrowser_back"></div>
      </li>
      <li>
          <a  class="btn" href="jin://jinzb" >打开app</a>
          <div class="text" >jin://jinzb</div>
      </li>
      <li>
          <a class="btn" href="telprompt://13175137233" >拨打电话</a>
          <div class="text" >13175137233</div>
      </li>

  </ul>
</div>
<div class="route-list">
// 款爷帮2.0 新接口
<ul>
  <li>
      <a class="btn" href="javascript:;" id="openWhithNewPage">用新页面打开url 并显示导航</a>
      <div class="text" id="openWhithNewPage_back"></div>
  </li>
  <li>
    <a class="btn" href="javascript:;" id="initUMPush">初始化umeng推送</a>
    <div class="text" id="initUMPush_back"></div>
  </li>
  <li>
    <a class="btn" href="javascript:;" id="uninitUMPush">注销umeng推送</a>
    <div class="text" id="uninitUMPush_back"></div>
  </li>
  <li>
      <a class="btn" href="javascript:;" id="openNotifySetting">开启推送</a>
      <div class="text" id="openNotifySetting_back"></div>
  </li>
  <li>
      <a class="btn" href="javascript:;" id="closeNotifySetting">关闭推送</a>
      <div class="text" id="closeNotifySetting_back"></div>
  </li>
  <li>
      <a class="btn" href="javascript:;" id="getNotifyStatus">获取推送开关状态</a>
      <div class="text" id="getNotifyStatus_back"></div>
  </li>
  <li>
      <a class="btn" href="javascript:;" id="finishCurrentPage">关闭当前页面</a>
      <div class="text" id="finishCurrentPage_back"></div>
  </li>
  <li>
      <a class="btn" href="javascript:;" id="clearCache">清除缓存</a>
      <div class="text" id="clearCache_back"></div>
  </li>
  <li>
      <a  class="btn" href="javascript:;" id ="updateImg">拨打电话</a>
      <div class="text" id="updateImg_back" >上传图片回调</div>
  </li>
</ul>

</div>

<div id='log'></div>

<script>
      var bridge = window.__SHANGHAIWEICHUANG_KUANYEBANG__web2app__;
      function global(name, val) {
          var iName = '__SHANGHAIWEICHUANG_KUANYEBANG__' + name + '__';
          return arguments.length > 1 ? (window[iName] = val) : window[iName];
      }
    function log(message, data) {
    var log = document.getElementById('log')
    var el = document.createElement('div')
    el.className = 'logLine'
    el.innerHTML = uniqueId++ + '. ' + message + ':<br/>' + JSON.stringify(data)
    if (log.children.length) { log.insertBefore(el, log.children[0]) }
    else { log.appendChild(el) }
  }
// web调用app
function web2app(name, aData, fn, aCallback) {
  var data = aData || {};
  var callback = typeof aCallback === 'function' ? aCallback : function() {};
  var iosInterfaces, interfaces;
  if (window.webkit && window.webkit.messageHandlers && window.webkit.messageHandlers.web2app && typeof window.webkit.messageHandlers.web2app.postMessage === 'function') {
    iosInterfaces = window.webkit.messageHandlers.web2app.postMessage;
  } else {
    interfaces = global('web2app');
  }
  if (iosInterfaces || (interfaces && typeof interfaces[name] === 'function')) {
    if (data && data.callback) {
      var callbackName = 'web2app_callbacks__callback'.toLocaleLowerCase();
      global(callbackName, function(data) {
        callback(data);
        delete global(callbackName);
      });
      data.callback = callbackName;
    }
    if (iosInterfaces) {
      var iData = {
        method: name,
        params: data
      };
      console.log('调起', {
        iosInterfaces: window.webkit.messageHandlers.web2app.postMessage,
        methodName: name,
        iData: iData
      });
      try {
        window.webkit.messageHandlers.web2app.postMessage(JSON.stringify(iData));
      } catch (err) {
        console.error(err);
        typeof fn === 'function' ? callback(fn(data)) : callback();
      }
    } else {
      console.log('调起', {
        interfaces: interfaces,
        methodName: name,
        'interfaces[methodName]': interfaces[name],
        data: data
      });
      try {
        interfaces[name](JSON.stringify(data));
      } catch (err) {
        console.error(err);
        typeof fn === 'function' ? callback(fn(data)) : callback();
      }
    }
    if (!data || !data.callback) {
      callback();
    }
  } else {
    typeof fn === 'function' ? callback(fn(data)) : callback();
  }
}

 // app回调web
   global('app2web', function(name, data) {
      var fn = global(name);
      console.log('回调', {
              name: name,
              fn: fn,
              data: data,
              parseDataRet: JSON.parse(data)
         });
  typeof fn === 'function' && fn(JSON.parse(data));
    });


      /****web调用app***/
  //分享url
    document.querySelector('#share').onclick = function() {
      web2app('share',{title:'金主邦分享',desc:'http://baidu.com',link:'http://baidu.com',imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1536565376247&di=2e3be825e12331d268301f962a052194&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01f09e577b85450000012e7e182cf0.jpg%401280w_1l_2o_100sh.jpg',way:'1',callback:'e'},
      function(){},function(result){
          var log = document.getElementById('share_back')
        log.innerHTML = 'result :<br/>' + JSON.stringify(result)
      });
      }
      //分享海报
    document.querySelector('#sharePoster').onclick = function() {
      web2app('sharePoster',{title:'http://baidu.com',desc:'http://baidu.com',link:'http://baidu.com',way:'wxTimeline',imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1536565376247&di=2e3be825e12331d268301f962a052194&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01f09e577b85450000012e7e182cf0.jpg%401280w_1l_2o_100sh.jpg',callback:'e'},
          function(){},function(result){
          var log = document.getElementById('sharePoster_back')
        log.innerHTML = 'result :<br/>' + JSON.stringify(result)
      });
      }
      //保存海报
    document.querySelector('#saveImg').onclick = function() {
      web2app('saveImg',{callback:'w',imgUrl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1536565376247&di=2e3be825e12331d268301f962a052194&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01f09e577b85450000012e7e182cf0.jpg%401280w_1l_2o_100sh.jpg'},
      function(){},function(result){
          var log = document.getElementById('saveImg_back')
        log.innerHTML = 'result :<br/>' + JSON.stringify(result)
      });
      }
       //显示一个toast
    document.querySelector('#showToast').onclick = function() {
      web2app('showToast',{content:'我是要显示的内容'},function(){},function(){});
      }
        //刷新当前页面
    document.querySelector('#refreshWebView').onclick = function() {
       web2app('refreshWebView',{},function(){},function(){});
      }
        //加载指定页面
    document.querySelector('#loadUrl').onclick = function() {
      web2app('openWebPage',{link:'https://baidu.com'},function(){},function(){});
      }
        //回退到上一页
    document.querySelector('#goBack').onclick = function() {
      web2app('goBack',{},function(result){},function(result){})
      }
       //取值
    document.querySelector('#getString').onclick = function() {
          web2app('getString',{key:'abc',callback:'a'},function(result){
          },function(result){
              var log = document.getElementById('getStringBak')
              log.innerHTML = 'result :<br/>' + JSON.stringify(result)
          });
      }
       //放值
    document.querySelector('#saveString').onclick = function() {
          web2app('saveString',{key:'abc',content:'getbak',callback:'b'},function(result){},function(result){
              var log = document.getElementById('saveString_back')
              log.innerHTML = 'result :<br/>' + JSON.stringify(result)
          })
      }
       //微信支付
    document.querySelector('#wxPay').onclick = function() {
      web2app('wxPay',{appId:'wx735d3e44bc0b0ca2',partnerId:'1514386351',prepayId:'wx13143313010589b2c7c3aef13555396903',nonceStr:'514a02b6808a89dd1c4c2e89293b9c89',timeStamp:'1536820393',sign:'F4561BBE8A6478F5BBE44063F5EF85D6',callback:'abc'},
          function(){},function(result){
              var log = document.getElementById('wxPay_back')
              log.innerHTML = 'result :<br/>' + JSON.stringify(result)
          });
      }
      //用自带浏览器打开url
    document.querySelector('#openWhithLocalBrowser').onclick = function() {
          web2app('openWhithLocalBrowser',{link:'http://baidu.com',callback:'b'},function(result){},function(result){
              var log = document.getElementById('openWhithLocalBrowser_back')
              log.innerHTML = 'result :<br/>' + JSON.stringify(result)
          })
      }
      //用自带浏览器打开url
    document.querySelector('#openWhithLocalBrowser').onclick = function() {
          web2app('openWhithLocalBrowser',{link:'http://baidu.com',callback:'b'},function(result){},function(result){
              var log = document.getElementById('openWhithLocalBrowser_back')
              log.innerHTML = 'result :<br/>' + JSON.stringify(result)
          })
      }
       //初始化umeng 推送
     document.querySelector('#initUMPush').onclick = function() {
          web2app('initUMPush',{uid:'weithink',islogin:'1',callback:'b'},function(result){},function(result){
                var log = document.getElementById('initUMPush_back')
                log.innerHTML = 'result :<br/>' + JSON.stringify(result)
          })
      }
      //注销umeng 推送
    document.querySelector('#uninitUMPush').onclick = function() {
         web2app('initUMPush',{uid:'weithink',islogin:'2',callback:'b'},function(result){},function(result){
               var log = document.getElementById('uninitUMPush_back')
               log.innerHTML = 'result :<br/>' + JSON.stringify(result)
         })
     }
      //用新界面打开一个连接
    document.querySelector('#openWhithNewPage').onclick = function() {
         web2app('openWhithNewPage',{link:'http://baidu.com/',callback:'b',showBar:'show'},function(result){},function(result){
               var log = document.getElementById('openWhithNewPage_back')
               log.innerHTML = 'result :<br/>' + JSON.stringify(result)
         })
     }
     //开启推送开关
   document.querySelector('#openNotifySetting').onclick = function() {
        web2app('openNotifySetting',{uid:'weithink',isOpen:'1',callback:'b'},function(result){},function(result){
              var log = document.getElementById('openNotifySetting_back')
              log.innerHTML = 'result :<br/>' + JSON.stringify(result)
        })
    }
    document.querySelector('#closeNotifySetting').onclick = function() {
         web2app('openNotifySetting',{uid:'weithink',isOpen:'2',callback:'b'},function(result){},function(result){
               var log = document.getElementById('closeNotifySetting_back')
               log.innerHTML = 'result :<br/>' + JSON.stringify(result)
         })
     }
    //开启推送开关
  document.querySelector('#getNotifyStatus').onclick = function() {
       web2app('getNotifyStatus',{callback:'b'},function(result){},function(result){
             var log = document.getElementById('getNotifyStatus_back')
             log.innerHTML = 'result :<br/>' + JSON.stringify(result)
       })
   }
   //关闭当前页面
 document.querySelector('#finishCurrentPage').onclick = function() {
      web2app('finishCurrentPage',{callback:'b'},function(result){},function(result){
            var log = document.getElementById('finishCurrentPage_back')
            log.innerHTML = 'result :<br/>' + JSON.stringify(result)
      })
  }
  //清除缓存
document.querySelector('#clearCache').onclick = function() {
     web2app('clearCache',{callback:'b'},function(result){},function(result){
           var log = document.getElementById('clearCache_back')
           log.innerHTML = 'result :<br/>' + JSON.stringify(result)
     })
 }

 document.getElementById('updateImg').onclick=function(){
   web2app('updateImgByQiniu',{callback:'b',filePath: [
    "/storage/emulated/0/Pictures/PIC-20190305-1548021063004719.png","/storage/emulated/0/Pictures/PIC-20190305-1548021063004719.png"
],key:['111','222'],token:'XaHBTm32-TgI9cj3HST-c7cLtJe8ruqjLaPEMF4v:VcKyi5j8z9MSJ0UjLp2L9agigK4=:eyJzY29wZSI6Imt5Yi1waWMiLCJkZWFkbGluZSI6MTU1MTc4ODU4M30='},function(result){},function(result){
         var log = document.getElementById('updateImg_back')
         log.innerHTML = 'result :<br/>' + JSON.stringify(result)
   })
 }
</script>
