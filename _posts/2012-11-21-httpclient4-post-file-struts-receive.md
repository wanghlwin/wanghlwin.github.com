---
layout: page
title: "HttpClient4 的使用（post上传文件）struts action 接收"
category: 
tags: [httpclient4.1,上传文件,MultipartEntity,FileBody,httpclient4.1上传文件]
description: 
---

# httpclient 4.1 很好的支持了 上传file的功能，下面来看一下具体的代码实现。
 
Java代码
{% highlight javascript %}
package com.whl.httpclient;  
import java.io.File;  
import java.io.IOException;  
  
import org.apache.http.HttpEntity;  
import org.apache.http.HttpResponse;  
import org.apache.http.HttpStatus;  
import org.apache.http.client.ClientProtocolException;  
import org.apache.http.client.HttpClient;  
import org.apache.http.client.methods.HttpPost;  
import org.apache.http.entity.mime.MultipartEntity;  
import org.apache.http.entity.mime.content.FileBody;  
import org.apache.http.entity.mime.content.StringBody;  
import org.apache.http.impl.client.DefaultHttpClient;  
import org.apache.http.util.EntityUtils;  
  
public class ClientMultipartFormPost {  
  
    public static void main(String[] args) throws ClientProtocolException, IOException {  
          
      HttpClient httpclient = new DefaultHttpClient();  
          
      try {  
            HttpPost httppost = new HttpPost("http://localhost:8080/table!uploadFile");  
          
            FileBody bin = new FileBody(new File("d:/whlwhlwhl.txt"));  
              
            StringBody comment = new StringBody("just test");  
          
            MultipartEntity reqEntity = new MultipartEntity();  
             
            reqEntity.addPart("upload", bin);//upload为请求后台的File upload;属性  
              
            reqEntity.addPart("str", comment);//str 为请求后台的String str;属性  
          
            httppost.setEntity(reqEntity);  
          
            HttpResponse response = httpclient.execute(httppost);  
              
            int statusCode = response.getStatusLine().getStatusCode();  
              
            if(statusCode == HttpStatus.SC_OK){  
                  
                HttpEntity resEntity = response.getEntity();  
                  
                System.out.println(EntityUtils.toString(resEntity));//httpclient自带的工具类读取返回数据  
              
                EntityUtils.consume(resEntity);  
  
            }  
              
        } finally {  
            try {   
                httpclient.getConnectionManager().shutdown();   
            } catch (Exception ignore) {  
                  
            }  
        }  
    }  
}  
{% endhighlight%} 

#不过如果遇到上传的文件名是中文的名字的话，该如何解决呢？
 
#求解答？