# Requests库详解
#爬虫

```
用法方便，基于urllib库
```

## 实例

```python
import requests

response =  requests.get("http://www.baidu.com")
print(type(response))
print(response.status_code)
print(response.text)
print(response.cookies)
```

```
<class 'requests.models.Response'>
200
<!DOCTYPE html>
<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=http://s1.bdstatic.com/r/www/cache/bdorz/baidu.min.css><title>ç¾åº¦ä¸ä¸ï¼ä½ å°±ç¥é</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=ç¾åº¦ä¸ä¸ class="bg s_btn"></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>æ°é»</a> <a href=http://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>å°å¾</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>è§é¢</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>è´´å§</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>ç»å½</a> </noscript> <script>document.write('<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ '" name="tj_login" class="lb">ç»å½</a>');</script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">æ´å¤äº§å</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>å³äºç¾åº¦</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>ä½¿ç¨ç¾åº¦åå¿è¯»</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>æè§åé¦</a>&nbsp;äº¬ICPè¯030173å·&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>

<RequestsCookieJar[<Cookie BDORZ=27315 for .baidu.com/>]>
```

## 各种请求方式

```python
import requests

requests.post("http://httpbin/post")
requests.put("http://httpbin/put")
requests.delete("http://httpbin/delete")
requests.head("http://httpbin/get")
requests.options("http://httpbin/get")
```

## 请求

### 基本的GET请求

#### 基本使用

```python
import requests

response = requests.get("http://httpbin.org/get")

print(response.text)
```

```
{
  "args": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.23.0", 
    "X-Amzn-Trace-Id": "Root=1-5e6894cf-dd476ea0264c09203cb3eb4c"
  }, 
  "origin": "27.205.175.189", 
  "url": "http://httpbin.org/get"
}
```

```python
import requests

params = {
    'name':'test',
    'age':33
}
response = requests.get("http://httpbin.org/get",params=params)

print(response.text)
```

```
{
  "args": {
    "age": "33", 
    "name": "test"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.23.0", 
    "X-Amzn-Trace-Id": "Root=1-5e689536-ae4ddf7caa1c912651d621fa"
  }, 
  "origin": "27.205.175.189", 
  "url": "http://httpbin.org/get?name=test&age=33"
}
```

## 解析Json

```python
import requests
import json

response = requests.get("http://httpbin.org/get")
print(type(response.text))

# 结果一样
print(response.json())
print(json.loads(response.text))

print(type(response.json()))
```

```
<class 'str'>
{'args': {}, 'headers': {'Accept': '*/*', 'Accept-Encoding': 'gzip, deflate', 'Host': 'httpbin.org', 'User-Agent': 'python-requests/2.23.0', 'X-Amzn-Trace-Id': 'Root=1-5e6895d6-1aad3eb76a5c7c63c7fea561'}, 'origin': '27.205.175.189', 'url': 'http://httpbin.org/get'}
{'args': {}, 'headers': {'Accept': '*/*', 'Accept-Encoding': 'gzip, deflate', 'Host': 'httpbin.org', 'User-Agent': 'python-requests/2.23.0', 'X-Amzn-Trace-Id': 'Root=1-5e6895d6-1aad3eb76a5c7c63c7fea561'}, 'origin': '27.205.175.189', 'url': 'http://httpbin.org/get'}
<class 'dict'>
```

## 解析二进制文件

```python
import requests

response = requests.get('https://github.com/favicon.ico')

with open("/Users/mac/MyCodes/python/github.ico",'wb') as f:
    f.write(response.content)
    f.close()
print('finish!')
```

```
finish!
```

## 添加 headers

```python
import requests

response = requests.get("https://www.zhihu.com/explore")
print(response.text)
```

```
<html>
<head><title>400 Bad Request</title></head>
<body bgcolor="white">
<center><h1>400 Bad Request</h1></center>
<hr><center>openresty</center>
</body>
</html>
```

```python
import requests
from bs4 import BeautifulSoup 

headers = {
    'User-Agent':'Mozilla/5.0(Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Safari/537.36',
}
response = requests.get(r"https://www.zhipin.com/c100010000/?page=4",headers=headers)
soup = BeautifulSoup(response.text)

print(soup.body)
```

```
<body>
<div class="data-tips">
<div class="tip-inner">
<div class="boss-loading">
<span class="component-b">B</span><span class="component-o">O</span><span class="component-s1">S</span><span class="component-s2">S</span>
<p class="gray">æ­£å¨å è½½ä¸­...</p>
</div>
</div>
</div>
<script>
            (function() {
                var script = document.createElement("script");
                script.src = "https://static.zhipin.com/library/js/analytics/ka.js";
                var s = document.getElementsByTagName("script")[0];
                s.parentNode.insertBefore(script, s);
            })();
            (function() {
                function isSeo(url){
                    return url.indexOf('baidu.com') > -1 || url.indexOf('sogou.com') > -1;
                }
                function init(frame) {
                    var COOKIE_DOMAIN = (function() {
                        var hostName = location.hostname;
                        if (hostName === "localhost" || /^(\d+\.){3}\d+$/.test(hostName)) {
                            return hostName;
                        }

                        return (
                            "." +
                            hostName
                                .split(".")
                                .slice(-2)
                                .join(".")
                        );
                    })();
                    var seriesLoadScripts = function(scripts, callback) {
                        if (typeof scripts != "object") var scripts = [scripts];
                        var s = new Array(),
                            last = scripts.length - 1,
                            recursiveLoad = function(i) {
                                s[i] = document.createElement("script");
                                s[i].setAttribute("type", "text/javascript");
                                s[i].setAttribute("charset", "UTF-8");
                                s[i].onload = s[i].onreadystatechange = function() {
                                    if (!/*@cc_on!@*/ 0 || this.readyState == "loaded" || this.readyState == "complete") {
                                        this.onload = this.onreadystatechange = null;
                                        this.parentNode.removeChild(this);
                                        if (i != last) recursiveLoad(i + 1);
                                        else if (typeof callback == "function") callback();
                                    }
                                };
                                s[i].setAttribute("src", scripts[i]);
                                if (frame.tagName != "IFRAME") {
                                    frame.appendChild(s[i]);
                                } else if (frame.contentDocument) {
                                    if (frame.contentDocument.body) {

                                        frame.contentDocument.body.appendChild(s[i]);
                                    } else {
                                        frame.contentDocument.documentElement.appendChild(s[i]);
                                    }
                                } else if (frame.document) {
                                    if (frame.document.body) {
                                        frame.document.body.appendChild(s[i]);
                                    } else {
                                        frame.document.documentElement.appendChild(s[i]);
                                    }
                                }
                            };
                        recursiveLoad(0);
                    };
                    var getQueryString = function(name) {
                        var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
                        var r = window.location.search.substr(1).match(reg);
                        if (r != null) return unescape(r[2]);
                        return null;
                    };
                    var Cookie = {
                        get: function(name) {
                            var arr,
                                reg = new RegExp("(^| )" + name + "=([^;]*)(;|$)");
                            if ((arr = document.cookie.match(reg))) {
                                return unescape(arr[2]);
                            } else {
                                return null;
                            }
                        },
                        set: function(name, value, time, domain, path) {
                            var str = name + "=" + encodeURIComponent(value);
                            if (time) {
                                var date = new Date(time).toGMTString();
                                str += ";expires=" + date;
                            }
                            str = domain ? str + ";domain=" + domain : str;
                            str = path ? str + ";path=" + path : str;
                            document.cookie = str;
                        }
                    };

                    var jumpReplace = function(url) {
                        window.location.replace(url);
                    }
                    
                    var url = window.location.href;
                    var seed = decodeURIComponent(getQueryString("seed")) || "";
                    var ts = getQueryString("ts");
                    var fileName = getQueryString("name");
                    var callbackUrl = decodeURIComponent(getQueryString("callbackUrl"));
                    var srcReferer = decodeURIComponent(getQueryString("srcReferer")||'');
                    
                    
                    if (seed && ts && fileName) {
                        seriesLoadScripts("security-js/" + fileName + ".js", function() {
                            var expiredate = new Date().getTime() + 32 * 60 * 60 * 1000 * 2;
                            var code = "";
                            var nativeParams = {};
                            var ABC = window.ABC || frame.contentWindow.ABC;
                            try {
                                code = new ABC().z(seed, parseInt(ts)+(480+new Date().getTimezoneOffset())*60*1000);
                            } catch (e) {}
                            if (code && callbackUrl) {
                                Cookie.set("__zp_stoken__", code, expiredate, COOKIE_DOMAIN, "/");
                                // æ®è¯´iOS å®¢æ·ç«¯å­å¨ææ¶åcookieå¤±è´¥çæåµï¼å æ­¤è°ç¨å®¢æ·ç«¯æä¾çæ¹æ³ï¼äº¤ç±å®¢æ·ç«¯é¢å¤åä¸æ¬¡cookie
                                if (typeof window.wst != "undefined" && typeof wst.postMessage == "function") {
                                    nativeParams = {
                                        name: "setWKCookie",
                                        params: {
                                            url: COOKIE_DOMAIN,
                                            name: "__zp_stoken__",
                                            value: encodeURIComponent(code),
                                            expiredate: expiredate,
                                            path: "/"
                                        }
                                    };
                                    window.wst.postMessage(JSON.stringify(nativeParams));
                                }

                                if(srcReferer && isSeo(srcReferer) && srcReferer != 'https://m.baidu.com/'){
                                    jumpReplace(srcReferer);
                                } else {
                                    jumpReplace(callbackUrl);
                                }
                            } else {
                                window.history.back();
                            }
                        });
                    } else {
                        if(srcReferer && isSeo(srcReferer) && srcReferer != 'https://m.baidu.com/'){
                            jumpReplace(srcReferer);
                        }else if (callbackUrl) {
                            jumpReplace(callbackUrl);
                        } else {
                            window.history.back();
                        }
                    }
                }
                var ie = !!(window.attachEvent && !window.opera);
                var wk = /webkit\/(\d+)/i.test(navigator.userAgent) && RegExp.$1 < 525;
                var fn = [];
                var run = function() {
                    for (var i = 0; i < fn.length; i++) fn[i]();
                };
                function ready(f) {
                    if (!ie && !wk && document.addEventListener) return document.addEventListener("DOMContentLoaded", f, false);
                    if (fn.push(f) > 1) return;
                    if (ie)
                        (function() {
                            try {
                                document.documentElement.doScroll("left");
                                run();
                            } catch (err) {
                                setTimeout(arguments.callee, 0);
                            }
                        })();
                    else if (wk)
                        var t = setInterval(function() {
                            if (/^(loaded|complete)$/.test(document.readyState)) clearInterval(t), run();
                        }, 0);
                }
                ready(function() {
                    var na = window.navigator.userAgent.toLowerCase();
                    if (na.match(/micromessenger/i) == 'micromessenger' || na.match(/wkwebview/i) == 'wkwebview') {
                        init(document.getElementsByTagName("head").item(0));
                        return;
                    }
                    var frame = document.createElement("iframe");
                    // frame.style.display = "none";
                    frame.style.height = 0;
                    frame.style.width = 0;
                    frame.style.margin = 0;
                    frame.style.padding = 0;
                    frame.style.border = "0 none";
                    frame.name = "zhipinFrame";
                    frame.src = "about:blank";

                    if (frame.attachEvent) {
                        frame.attachEvent("onload", function() {
                            init(frame);
                        });
                    } else {
                        frame.onload = function() {
                            init(frame);
                        };
                    }
                    (document.body || document.documentElement).appendChild(frame);
                });
            })();
        </script>
</body>
```

## 基本POST 请求

```python
import requests

data = {'name':'test'}
headers = {
    'User-Agent':'Mozilla/5.0(Macintosh; Intel Mac OS X 10_15_3)AppleWebKit/537.36(KHTML, like Gecko) Chrome/80.0.3987.132 Safari/537.36',
}

response = requests.post("http://httpbin.org/post",data=data,headers=headers)

print(response.text)
```

```
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "test"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Content-Length": "9", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Mozilla/5.0(Macintosh; Intel Mac OS X 10_15_3)AppleWebKit/537.36(KHTML, like Gecko) Chrome/80.0.3987.132 Safari/537.36", 
    "X-Amzn-Trace-Id": "Root=1-5e689a93-f3271ea041ec2120f9e5bc20"
  }, 
  "json": null, 
  "origin": "27.205.175.189", 
  "url": "http://httpbin.org/post"
}
```

## 响应

### response 属性

```python
import requests

response = requests.get("http://www.baidu.com")
print(response.status_code)
print(response.headers)
print(response.cookies)
print(response.url)
print(response.history)

```

```
200
{'Cache-Control': 'private, no-cache, no-store, proxy-revalidate, no-transform', 'Connection': 'keep-alive', 'Content-Encoding': 'gzip', 'Content-Type': 'text/html', 'Date': 'Wed, 11 Mar 2020 08:19:20 GMT', 'Last-Modified': 'Mon, 23 Jan 2017 13:27:32 GMT', 'Pragma': 'no-cache', 'Server': 'bfe/1.0.8.18', 'Set-Cookie': 'BDORZ=27315; max-age=86400; domain=.baidu.com; path=/', 'Transfer-Encoding': 'chunked'}
<RequestsCookieJar[<Cookie BDORZ=27315 for .baidu.com/>]>
http://www.baidu.com/
[]
```

### 状态码判断

```python
import requests

response = requests.get("http://www.baidu.com")
exit() if not response.status_code == requests.codes.ok else print("finish")
```

```
finish
```

# 高级操作
## 文件上传

```python
import requests

file = {'file':open("/Users/mac/MyCodes/python/github.ico",'rb')}
response = requests.post('http://httpbin.org/post',files=file)
print(response.text)
```

```
{
  "args": {}, 
  "data": "", 
  "files": {
    "file": "data:application/octet-stream;base64,AAABAAIAEBAAAAEAIAAoBQAAJgAAACAgAAABACAAKBQAAE4FAAAoAAAAEAAAACAAAAABACAAAAAAAAAFAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABERE3YTExPFDg4OEgAAAAAAAAAADw8PERERFLETExNpAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABQUFJYTExT8ExMU7QAAABkAAAAAAAAAAAAAABgVFRf/FRUX/xERE4UAAAAAAAAAAAAAAAAAAAAAAAAAABEREsETExTuERERHhAQEBAAAAAAAAAAAAAAAAAAAAANExMU9RUVF/8VFRf/EREUrwAAAAAAAAAAAAAAABQUFJkVFRf/BgYRLA4ODlwPDw/BDw8PIgAAAAAAAAAADw8PNBAQEP8VFRf/FRUX/xUVF/8UFBSPAAAAABAQEDAPDQ//AAAA+QEBAe0CAgL/AgIC9g4ODjgAAAAAAAAAAAgICEACAgLrFRUX/xUVF/8VFRf/FRUX/xERES0UFBWcFBQV/wEBAfwPDxH7DQ0ROwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA0NEjoTExTnFRUX/xUVF/8SEhKaExMT2RUVF/8VFRf/ExMTTwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAERERTBUVF/8VFRf/ExMT2hMTFPYVFRf/FBQU8AAAAAIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAITExTxFRUX/xMTFPYTExT3FRUX/xQUFOEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAFBQU4RUVF/8TExT3FBQU3hUVF/8TExT5Dw8PIQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEBAQHxMTFPgVFRf/FBQU3hERFKIVFRf/FRUX/w8PDzQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAQEEAVFRf/FRUX/FRUX8RYWGJcVFSAYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKysrBhYWGUcWFhiVFRUYvxUVGNkWFhfzFhYX8xUVGNkVFRi/FhYYlRYWGUcrKysGAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA="
  }, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Content-Length": "6664", 
    "Content-Type": "multipart/form-data; boundary=28fce0800b1ded6aed8db6c1a4acce7f", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.23.0", 
    "X-Amzn-Trace-Id": "Root=1-5e68a090-b62f797cf14d9e1b07a80229"
  }, 
  "json": null, 
  "origin": "27.205.175.189", 
  "url": "http://httpbin.org/post"
}
```

## 获取Cookie

```python
import requests

response = requests.get("http://www.baidu.com")
print(response.cookies)
for key,value in response.cookies.items():
    print(key+"="+value)
```

```
<RequestsCookieJar[<Cookie BDORZ=27315 for .baidu.com/>]>
BDORZ=27315
```

## 会话维持
### 模拟登陆

```python
import requests

#两个过程相对独立
# 相当于 一个浏览器设置cookie 另一个浏览器访问
requests.get("http://httpbin.org/cookies/set/number/12345")
response = requests.get("http://httpbin.org/cookies")
print(response.text)
```

```
{
  "cookies": {}
}
```

```python
import requests

s = requests.Session();

# 维持回话信息 自动处理
s.get("http://httpbin.org/cookies/set/number/12345")
response = s.get("http://httpbin.org/cookies")


print(response.text)
```

```
{
  "cookies": {
    "number": "12345"
  }
}
```

### 证书验证
https 监测整数 如果不合法 抛出 SSLError

```python
import requests

response = requests.get("https://www.12306.cn",verify = False)
print(response)
```

```
<Response [200]>
```

```
/Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages/urllib3/connectionpool.py:997: InsecureRequestWarning: Unverified HTTPS request is being made to host 'www.12306.cn'. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
  warnings.warn(
/Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages/urllib3/connectionpool.py:997: InsecureRequestWarning: Unverified HTTPS request is being made to host 'www.12306.cn'. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
  warnings.warn(
```

```python
import requests

from requests.packages import urllib3
urllib3.disable_warnings()

response = requests.get("https://www.12306.cn",verify = False)
print(response)
```

```
<Response [200]>
```

### 代理设置

```python
import requests

proxies = {
    'http':'http://user:password@127.0.0.0.1:9743'
}

response = requests.get("http://www.baidu.com",proxies=proxies)

print(response.status_code)
```


```
ProxyError: HTTPConnectionPool(host='127.0.0.0.1', port=9743): Max retries exceeded with url: http://www.baidu.com/ (Caused by ProxyError('Cannot connect to proxy.', NewConnectionError('<urllib3.connection.HTTPConnection object at 0x111b30220>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known')))
```

```python
# socks 代理
pip3 install 'requests[socks]'

import requests

proxies = {
    'http':'sock5:http://user:password@127.0.0.0.1:9743'
}

response = requests.get("http://www.baidu.com",proxies=proxies)

print(response.status_code)
```

## 超时设置
抛出ReadTimeout

```python
import requests

requests.get(url,timeout=1)
```

## 认证设

```python
import requests

from requests.auth import HTTPBasicAuth

r = requests.get("http://120.27.34.24:9001",auth=HTTPBasicAuth('user','123'))
print(r.status_code)
```

```
KeyboardInterrupt: 
```

```python
import requests

from requests.auth import HTTPBasicAuth

r = requests.get("http://120.27.34.24:9001",auth=('user','123'))
print(r.status_code)
```

## 异常处理
先捕捉子类异常 然后捕捉父类异常

```python
import requests

headers = {
               'User-Agent': 'Mozilla/5.0 (Windows NT 5.1; U; en; rv:1.8.1) Gecko/20061208 Firefox/2.0.0 Opera 9.50'
        }
proxies = {
  "http": "http://60.216.20.213:8001",
  "https": "https://60.216.20.214:8001"
}

#http://www.dianping.com/shop/129152119
try:
    for i in range(129152000,129152119):
        print(requests.get('http://www.baidu.com',proxies=proxies))
        print(requests.get('http://www.dianping.com/shop/'+str(i), headers=headers,proxies=proxies))
        print('http://www.dianping.com/shop/'+str(i))
except Exception as e:
    print(e)
```

```
HTTPConnectionPool(host='60.216.20.213', port=8001): Max retries exceeded with url: http://www.baidu.com/ (Caused by ProxyError('Cannot connect to proxy.', NewConnectionError('<urllib3.connection.HTTPConnection object at 0x1135dd880>: Failed to establish a new connection: [Errno 60] Operation timed out')))
```

```python

```