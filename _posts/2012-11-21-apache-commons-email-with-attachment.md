---
layout: page
title: "使用apache commons email 发送带附件邮件（可中文） "
category:java
tags: [javamail,commons,email,邮件附件,邮件为中文]
description: 
---

# Java Mail 实在难用，伤不起，发现个简单方便的邮件组件，在Java Mail的基础上又包了一层，代码如下：附件可以是中文（有问题和意见的欢迎拍砖）

{% highlight javascript %}
package com.richmobi.util;  
  
import java.io.File;  
import java.io.UnsupportedEncodingException;  
import java.net.MalformedURLException;  
import java.net.URLDecoder;  
import java.util.concurrent.ExecutorService;  
import java.util.concurrent.Executors;  
  
import javax.mail.internet.MimeUtility;  
  
import org.apache.commons.mail.EmailAttachment;  
import org.apache.commons.mail.EmailException;  
import org.apache.commons.mail.HtmlEmail;  
import org.apache.log4j.Logger;  
  
/** 
     * 创建日期:2011-12-14 
     * Title: 邮件发送工具类 
     * Description：对本文件的详细描述，原则上不能少于50字 
     * @author hongliang.wang 
     * @mender：（文件的修改者，文件创建者之外的人） 
     * @version 1.0 
     * Remark：认为有必要的其他信息 
 */  
public class SendMailUtil {  
      
    private static final Logger log = Logger.getLogger(SendMailUtil.class);  
    private static ExecutorService executor;  
      
    static{  
        executor = Executors.newFixedThreadPool(50);  
    }  
  
    /** 
     * 功能:发送邮件  
     * 作者: hongliang.wang 
     * 创建日期:2011-12-14 
     * 修改者: mender 
     * 修改日期: modifydate 
     * @param mialTitle 邮件主题 
     * @param attachPath 附件地址 
     * @param attachName 附件显示名称 
     * @param toEmail 收件人 
     * @param mailContent 邮件内容 
     * @throws MalformedURLException  
     * @throws UnsupportedEncodingException  
     * @throws EmailException  
     */  
    public static  void sendEmail(final String mialTitle,final String attachPath,final String attachName,final String toEmail,final String mailContent) throws MalformedURLException, UnsupportedEncodingException, EmailException{  
        final String mailServer = Configer.get("smtpServer");  
        final String mailName = Configer.get("mailName");  
        final String mailPwd = Configer.get("mailPassword");  
          
          
          
        executor.execute(new Runnable(){  
            public void run() {  
                EmailAttachment  attachment = null;  
                if(attachPath!=null){  
                    attachment = new EmailAttachment();  
                    try {  
                        attachment.setPath(attachPath);  
                        attachment.setName(MimeUtility.encodeText(attachName));  
                        attachment.setDisposition(EmailAttachment.ATTACHMENT);  
                        attachment.setDescription("Picture of John");  
                    }catch (UnsupportedEncodingException e) {  
                        e.printStackTrace();  
                        log.info(e.getMessage());  
                    }  
                }  
                  
                HtmlEmail email = new HtmlEmail();//可以发送html类型的邮件     
                email.setHostName(mailServer);//指定要使用的邮件服务器     
                email.setAuthentication(mailName, mailPwd);//使用163的邮件服务器需提供在163已注册的用户名、密码     
                email.setCharset("UTF-8");       
                try {  
                    email.setFrom(mailName,"GMIC2012");  
                    //设置发件人     
                    email.addTo(toEmail);//设置收件人     
                    email.setSubject(mialTitle);//设置主题   
                    email.setHtmlMsg((mailContent==null||"".equals(mailContent))?"":mailContent);//可以发送html  
                    if(attachPath!=null){  
                        email.attach(attachment);  
                    }  
                    log.info("mailServer:"+Configer.get("smtpServer")+"mailTo: "+ toEmail);  
                    log.info("邮件正文："+mailContent);  
                    email.send();  
                } catch (EmailException e) {  
                    e.printStackTrace();  
                    log.info(e.getMessage());  
                }  
            }  
        });  
    }  
      
    public static void main(String[] args) throws MalformedURLException, UnsupportedEncodingException, EmailException {  
        String fileName = "Nginx配置.doc";  
        String path = URLDecoder.decode(SendMailUtil.class.getClassLoader().getResource("info"+File.separator+fileName).toString(),"utf-8").replaceAll("file:/", "");  
          
        SendMailUtil.sendEmail("测试中文",path, fileName,"68644421@qq.com", "测试正文");  
    }  
}  
{% endhighlight%}