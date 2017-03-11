---
title: "如何：在 Visual Basic 中从注册表项中读取值 | Microsoft Docs"
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
  - "My.Computer.Registry 对象, 示例"
  - "注册表项, 确定值是否存在其中"
  - "注册表项, 读取自"
  - "注册表, 确定值是否存在"
  - "注册表, 读取"
ms.assetid: 775d0a57-68c9-464e-8949-9a39bd29cc64
caps.latest.revision: 31
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 31
---
# 如何：在 Visual Basic 中从注册表项中读取值
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`My.Computer.Registry` 对象的 `GetValue` 方法可用于读取 windows 注册表中的值。  
  
 如果键， “software \\ MyApp”在下面的示例中，不存在，则将引发。  如果 `ValueName`， “名称”在下面的示例中，不存在， `Nothing` 返回。  
  
 `GetValue` 方法还可用于确定给定的值是否存在于特定的注册表项。  
  
 当代码从 Web 应用程序中读取注册表，在 Web 应用程序实现的身份验证和模拟取决于当前用户。  
  
### 读取注册表项的值  
  
-   使用 `GetValue` 方法，指定路径和名称\) 读取注册表项的值。  下面的示例读取 `HKEY_CURRENT_USER\Software\MyApp` 的值 `Name` 并在消息框中显示该  
  
     [!code-vb[VbResourceTasks#4](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-read-a-value-from_1.vb)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **windows 操作系统 \> 注册表**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
### 确定值是否存在于注册表项  
  
-   使用 `GetValue` 方法检索值。  下面的代码检查该值是否存在并返回消息; 如果未。  
  
     [!code-vb[VbResourceTasks#12](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-read-a-value-from_2.vb)]  
  
## 可靠编程  
 注册表到顶级 \(或根，用于存储数据的键。  例如，在中，而 HKEY\_CURRENT\_USER 用于存储为单个用户的数据时，具体使用 HKEY\_LOCAL\_MACHINE 根注册表项用于存储所有用户使用的计算机级设置。  
  
 以下情况可能会导致异常:  
  
-   注册表项的名称为 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   用户无权从注册表项 \(<xref:System.Security.SecurityException>\) 中读取。  
  
-   注册表项名称超过 255 个字符的限制 \(<xref:System.ArgumentException>\)。  
  
## .NET Framework 安全性  
 若要运行此进程，程序集需要 <xref:System.Security.Permissions.RegistryPermission> 类授予的特权级别。  如果在部分信任的上下文中运行，则该进程可能会因特权不足而引发异常权限。  同样，用户必须有创建或写入设置的正确的 ACL。  例如，具有代码访问安全性权限的本地应用程序可能没有操作系统权限。  有关更多信息，请参见 [代码访问安全性基础知识](../Topic/Code%20Access%20Security%20Basics.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 <xref:Microsoft.Win32.RegistryHive>   
 [读取和写入注册表](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)