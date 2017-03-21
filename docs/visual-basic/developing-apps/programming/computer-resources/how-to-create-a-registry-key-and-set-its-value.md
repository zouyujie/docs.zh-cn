---
title: "如何：在 Visual Basic 中创建注册表项并设置其值 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "RegistryKey.CreateSubKey"
  - "RegistryKey.SetValue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "示例 [Visual Basic], 注册表"
  - "注册表项, 创建"
  - "注册表项, 设置值"
  - "注册表, 添加项"
  - "注册表, 添加值"
ms.assetid: d3e40f74-c283-480c-ab18-e5e9052cd814
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# 如何：在 Visual Basic 中创建注册表项并设置其值
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`My.Computer.Registry` 对象的 `CreateSubKey` 方法可用于创建注册表项。  
  
## 程序  
  
#### 创建注册表项  
  
-   使用 `CreateSubKey` 方法，指定在其下放置注册表配置单元以及注册表项的名称。  该参数`Subkey`不区分大小写。  此示例创建注册表项 `MyTestKey` 在 HKEY\_CURRENT\_USER 下。  
  
     [!code-vb[VbResourceTasks#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_1.vb)]  
  
#### 创建注册表项并在注册表项中设置值  
  
1.  使用 `CreateSubkey` 方法，指定在其下放置注册表配置单元以及注册表项的名称。  此示例创建注册表项 `MyTestKey` 在 HKEY\_CURRENT\_USER 下。  
  
     [!code-vb[VbResourceTasks#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_1.vb)]  
  
2.  设置与 `SetValue` 方案的值。  此示例将字符串值。 “  ” MyTestKeyValue “设置为 " this is a test value”。  
  
     [!code-vb[VbResourceTasks#14](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_2.vb)]  
  
## 示例  
 此示例创建注册表项 `MyTestKey` 在 HKEY\_CURRENT\_USER 下然后将字符串值 `MyTestKeyValue` 到 `This is a test value`。  
  
 [!code-vb[VbResourceTasks#15](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_3.vb)]  
  
## 可靠编程  
 检查注册表结构查找适合您的项的位置。  例如，您可能需要打开当前用户的 HKEY\_CURRENT\_USER \\ software 项，然后用您的公司名称创建一项。  然后将注册表值添加到您的公司的键。  
  
 当从 Web 应用程序中读取注册表，当前用户取决于 Web 应用程序中实现的身份验证和模拟。  
  
 它与将数据写入用户文件夹 \(<xref:Microsoft.Win32.Registry.CurrentUser>\) 而不是写入本地计算机 \(<xref:Microsoft.Win32.Registry.LocalMachine>\)。  
  
 当您创建注册表值时，需要确定解决方法，如果该值已存在。  另一进程， \(可能是恶意一个，可能已创建了该值和可以访问它。  将数据放入注册表值时，数据对其他可用进程。  若要防止这一问题，请使用 <xref:Microsoft.Win32.RegistryKey.GetValue%2A> 方法。  ，如果此键已不存在，则返回 `Nothing` 。  
  
 它是不安全的存储机密信息，例如密码，在注册表中以纯文本形式，因此，即使注册表项受 ACL \(访问控制列表\) 保护。  
  
 以下情况可能会导致异常:  
  
-   注册表项的名称为 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   用户没有创建注册表项的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   注册表项名称超过 255 个字符的限制 \(<xref:System.ArgumentException>\)。  
  
-   注册表项已关闭 \(<xref:System.IO.IOException>\)。  
  
-   注册表项是只读的 \(<xref:System.UnauthorizedAccessException>\)。  
  
## .NET Framework 安全性  
 若要运行此进程，程序集需要 <xref:System.Security.Permissions.RegistryPermission> 类授予的特权级别。  如果在部分信任的上下文中运行，则该进程可能会因特权不足而引发异常权限。  同样，用户必须有创建或写入设置的正确的 ACL。  例如，具有代码访问安全性权限的本地应用程序可能没有操作系统权限。  有关更多信息，请参见 [代码访问安全性基础知识](../Topic/Code%20Access%20Security%20Basics.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy.CurrentUser%2A>   
 <xref:Microsoft.Win32.RegistryKey.CreateSubKey%2A>   
 [读取和写入注册表](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)   
 [代码访问安全性基础知识](../Topic/Code%20Access%20Security%20Basics.md)