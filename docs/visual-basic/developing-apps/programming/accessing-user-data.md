---
title: "访问用户数据 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据 [Visual Basic], 访问用户数据"
  - "域名, 检索"
  - "示例 [Visual Basic], 访问用户数据"
  - "登录名称"
  - "My.User 对象, 任务"
  - "用户数据, 访问"
  - "用户数据, 域"
  - "用户名, 检索"
ms.assetid: 32492a15-ee59-4a63-a1f1-9b24cc13140a
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 访问用户数据 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本节包含涉及 `My.User` 对象以及可以使用该对象完成的任务的主题。  
  
 `My.User` 对象通过返回实现 <xref:System.Security.Principal.IPrincipal> 接口的对象提供对有关已登录用户的信息的访问。  
  
## 任务  
  
|若要|请参见|  
|--------|---------|  
|获取用户的登录名称|<xref:Microsoft.VisualBasic.ApplicationServices.User.Name%2A>|  
|获取用户的域名（如果应用程序使用 Windows 身份验证）|<xref:Microsoft.VisualBasic.ApplicationServices.User.CurrentPrincipal>|  
|确定用户的角色|<xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A>|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.User>