---
title: "安全性与注册表 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "注册表, 安全性问题"
  - "安全 [Visual Basic], 注册表"
ms.assetid: 9980aff7-2f69-492b-8f66-29a9a76d3df5
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 安全性与注册表 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本页讨论在注册表中存储数据的安全问题。  
  
## 权限  
 在注册表中以纯文本形式存储机密信息（例如密码）是不安全的，即使注册表项受 ACL（访问控制列表）保护。  
  
 对注册表进行操作时，如果允许对系统资源或受保护的信息进行不适当的访问，则可能会降低安全性。  要使用这些属性，您必须拥有控制注册表变量访问权限的 <xref:System.Security.Permissions.RegistryPermissionAccess> 枚举的读写权限。  任何以完全信任方式运行的代码（在默认安全策略下，指任何安装在用户的本地硬盘上的代码）都具有访问注册表的必要权限。  有关更多信息，请参见 <xref:System.Security.Permissions.RegistryPermission> 类。  
  
 注册表变量不应存储在没有 <xref:System.Security.Permissions.RegistryPermission> 的代码也能访问的内存位置。  同样，在授予权限时，应授予完成任务所需的最小权限。  
  
 注册表权限访问值由 <xref:System.Security.Permissions.RegistryPermissionAccess> 枚举定义。  下表详细描述了它的成员。  
  
|值|对注册表变量的访问权限|  
|-------|-----------------|  
|`AllAccess`|创建、读取和写入|  
|`Create`|Create|  
|`NoAccess`|没有访问权|  
|`Read`|Read|  
|`Write`|Write|  
  
## 检查注册表项中的值  
 在您创建注册表值时，需要确定如果该值已存在则应执行的操作。  另一进程（可能是恶意进程）可能已创建了该值，并拥有对该值的访问权。  将数据放入注册表值后，其他进程就可以使用这些数据了。  若要防止出现这种情况，请使用 `GetValue` 方法。  它在注册表项已经不存在时返回 `Nothing`。  
  
> [!IMPORTANT]
>  从 Web 应用程序中读取注册表时，当前用户的身份取决于 Web 应用程序中实现的身份验证和模拟。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 [读取和写入注册表](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)