---
title: "如何：在 Visual Basic 中删除注册表项 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.DeleteSetting"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "示例 [Visual Basic], 注册表"
  - "GetAllSettings 函数"
  - "GetSetting 函数"
  - "注册表项, 删除"
  - "注册表, 删除键"
  - "注册表, 删除值"
ms.assetid: ab9aca0e-42b0-4ff7-8ff9-845a4bfdf9f2
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# 如何：在 Visual Basic 中删除注册表项
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%29> 和 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%2CSystem.Boolean%29> 方法可用于删除注册表项。  
  
## 程序  
  
#### 删除注册表项  
  
-   使用 `DeleteSubKey` 方法删除注册表项。  此示例删除 CurrentUser 配置单元中的 software\/testapp 项。  可以更改此在代码为相应的字符串或者根据用户提供的信息。  
  
     [!code-vb[VbResourceTasks#19](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-delete-a-registry_1.vb)]  
  
## 可靠编程  
 ，如果该键\/值对不存在， `DeleteSubKey` 方法返回空字符串。  
  
 以下情况可能会导致异常:  
  
-   注册表项的名称为 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   用户无权删除注册表项 \(<xref:System.Security.SecurityException>\)。  
  
-   注册表项名称超过 255 个字符的限制 \(<xref:System.ArgumentException>\)。  
  
-   注册表项是只读的 \(<xref:System.UnauthorizedAccessException>\)。  
  
## .NET Framework 安全性  
 注册表调用失败，如果未授予足够的运行时 \(<xref:System.Security.Permissions.RegistryPermission>\)，或者用户没有正确的访问权限 \(由 ACL\) 创建或写入设置。  例如，具有代码访问安全性权限的本地应用程序可能没有操作系统权限。  
  
## 请参阅  
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey>   
 [安全性与注册表](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)   
 [读取和写入注册表](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)