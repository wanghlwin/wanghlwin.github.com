---
layout: page
title: "JSP页面中使用jstl 标签"
category: javaweb
tags: [jsp,jstl]
description: 介绍jsp页面中使用jstl标签。maven引入jstl
---

# 时间长了不常用的东西老是忘记，这次小记一下，以备下次查找。

>>
## 如果是maven项目，则先在 pom.xml中添入一下配置：
	<dependency>
		<groupId>jstl</groupId>
		<artifactId>jstl</artifactId>
		<version>1.2</version>
	</dependency>

	<dependency>
		<groupId>taglibs</groupId>
		<artifactId>standard</artifactId>
		<version>1.1.2</version>
	</dependency>
## 如果是一般的web项目，则导入相应的jar包即可。之后再jsp页面头导入标签的配置：
	核心标签库：<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
	格式化标签库：<%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %> 
    函数标签库：<%@taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>

 
##	判断集合的长度：
	<c:if test="${fn:length(blackAppList) > 0 }">
		<c:forEach items="${blackAppList}" var="app">
			<li><strong>应用程序名称</strong>${app.appName }</li>
		</c:forEach>
	</c:if>
 
##	常用的遍历集合和判断标签的使用：

	<c:forEach items="${pageInfo.result }" var="result" varStatus="st">
  		<tr <c:if test='${st.index % 2 != 0 }'> class="sec_tr" </c:if>>	
			<td scope="col">
  				<fmt:formatDate value="${result.requestTime}" pattern="yyyy年MM月dd日HH点mm分ss秒" />
  			</td>
  			<td scope="col">
		    	<c:if test="${result.platform == 1 }">
		    		IOS
		    	</c:if>
		    	<c:if test="${result.platform == 2 }">
		    		Android
		    	</c:if>
		    </td>
  			<td scope="col">${result.department }</td>
		    <td scope="col">${result.username }</td>
		    <td scope="col">${result.email }</td>
		    <td scope="col">${result.policyId}</td>
		    <td scope="col">
  				<c:if test="${result.requestStatus == 0}">
  					Pending
  				</c:if>
  				<c:if test="${result.requestStatus == 1}">
  					Completed
  				</c:if>
  			</td>
  			<td scope="col">${result.registionTime }</td>
		    <td scope="col">${result.deviceId }</td>
		    <td scope="col">${result.requestComment}</td>
		    <td scope="col">${result.passcode }</td>
  		</tr>
	</c:forEach>
