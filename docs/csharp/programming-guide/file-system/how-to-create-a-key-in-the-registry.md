---
title: "如何：在注册表中创建注册表项 (Visual C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "键, 在注册表中创建"
  - "注册表项, 创建 [C#]"
  - "注册表, 添加注册表项和值 [C#]"
ms.assetid: 8fa475b0-e01f-483a-9327-fd03488fdf5d
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在注册表中创建注册表项 (Visual C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本示例将值对“Name”和“Isabella”添加到当前用户的注册表中的注册表项“Names”之下。  
  
## 示例  
  
```  
Microsoft.Win32.RegistryKey key;  
key = Microsoft.Win32.Registry.CurrentUser.CreateSubKey("Names");  
key.SetValue("Name", "Isabella");  
key.Close();  
```  
  
## 编译代码  
  
-   复制该代码，并将其粘贴到某控制台应用程序的 `Main` 方法中。  
  
-   将 `Names` 参数替换为直接存在于注册表 HKEY\_CURRENT\_USER 节点下的项的名称。  
  
-   将 `Nam`e 参数替换为直接存在于“Names”节点下的值的名称。  
  
## 可靠编程  
 检查注册表结构以查找适合您的项的位置。  例如，您可能需要打开当前用户的 Software 项，并且用您的公司的名称创建一项。  然后将注册表值添加到您的公司的项上。  
  
 以下情况可能会导致异常：  
  
-   注册表项的名称为空。  
  
-   用户没有创建注册表项的权限。  
  
-   注册表项名称超过 255 个字符的限制。  
  
-   注册表项已关闭。  
  
-   注册表项是只读的。  
  
## .NET Framework 安全性  
 与将数据写入本地计算机 \(`Microsoft.Win32.Registry.LocalMachine`\) 相比，将数据写入用户文件夹 \(`Microsoft.Win32.Registry.CurrentUser`\) 更安全。  
  
 在您创建注册表值时，需要确定如果该值已存在则应执行的操作。  另一进程（可能是恶意进程）可能已创建了该值，并拥有对该值的访问权。  将数据放入注册表值后，其他进程就可以使用这些数据了。  若要防止出现这种情况，请使用 `Overload:Microsoft.Win32.RegistryKey.GetValue` 方法。  如果注册表项不存在，该方法将返回 null。  
  
 即使注册表项受访问控制列表 \(ACL\) 的保护，在注册表中以纯文本形式存储机密信息（例如密码）也不安全。  
  
## 请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)   
 [Read, write and delete from the registry with C\#](http://www.codeproject.com/Articles/3389/Read-write-and-delete-from-registry-with-C)