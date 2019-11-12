---
title: ORC文字识别
date: 2019-11-12 17:30:30
tags:
---

![OCR文字识别](https://photogallery.oss.aliyuncs.com/photo/1048850682116167/14020/00c2a149-1778-4ec4-836d-efb4a6ff1882.png)
# 阿里API市场
[通用类文字图片识别](https://ai.aliyun.com/ocr/general?spm=5176.12127985.1248150.9.a3534f58twAhtK)
## Python
~~~python
import urllib, urllib2, sys
import ssl

host = 'https://tysbgpu.market.alicloudapi.com'
path = '/api/predict/ocr_general'
method = 'POST'
appcode = '你自己的AppCode'
querys = ''
bodys = {}
url = host + path

bodys[''] = "{\"image\":\"图片二进制数据的base64编码或者图片url\",\"configure\":\"{\\\"min_size\\\":16,#图片中文字的最小高度\\\"output_prob\\\":true#是否输出文字框的概率}\"}"
post_data = bodys['']
request = urllib2.Request(url, post_data)
request.add_header('Authorization', 'APPCODE ' + appcode)
//根据API的要求，定义相对应的Content-Type
request.add_header('Content-Type', 'application/json; charset=UTF-8')
ctx = ssl.create_default_context()
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE
response = urllib2.urlopen(request, context=ctx)
content = response.read()
if (content):
    print(content)
~~~
## Java
~~~java
public static void main(String[] args) {
    String host = "https://tysbgpu.market.alicloudapi.com";
    String path = "/api/predict/ocr_general";
    String method = "POST";
    String appcode = "你自己的AppCode";
    Map<String, String> headers = new HashMap<String, String>();
    //最后在header中的格式(中间是英文空格)为Authorization:APPCODE 83359fd73fe94948385f570e3c139105
    headers.put("Authorization", "APPCODE " + appcode);
    //根据API的要求，定义相对应的Content-Type
    headers.put("Content-Type", "application/json; charset=UTF-8");
    Map<String, String> querys = new HashMap<String, String>();
    String bodys = "{\"image\":\"图片二进制数据的base64编码或者图片url\",\"configure\":\"{\\\"min_size\\\":16,#图片中文字的最小高度\\\"output_prob\\\":true#是否输出文字框的概率}\"}";

    try {
      /**
      * 重要提示如下:
      * HttpUtils请从
      * https://github.com/aliyun/api-gateway-demo-sign-java/blob/master/src/main/java/com/aliyun/api/gateway/demo/util/HttpUtils.java
      * 下载
      *
      * 相应的依赖请参照
      * https://github.com/aliyun/api-gateway-demo-sign-java/blob/master/pom.xml
      */
      HttpResponse response = HttpUtils.doPost(host, path, method, headers, querys, bodys);
      System.out.println(response.toString());
      //获取response的body
      //System.out.println(EntityUtils.toString(response.getEntity()));
    } catch (Exception e) {
      e.printStackTrace();
    }
}
~~~
