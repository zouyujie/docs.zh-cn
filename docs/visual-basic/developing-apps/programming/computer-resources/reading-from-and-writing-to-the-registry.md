---
title: "读取和写入注册表 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "My.Computer.Registry 对象, 任务"
  - "注册表, 读取"
  - "注册表, 写入"
ms.assetid: a13da106-185b-41d7-b23c-416da65e21e4
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 读取和写入注册表 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

本主题介绍与注册表相关的任务和概念性主题。  
  
 在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中编程时，可以通过 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供的函数或者通过 .NET Framework 的注册表类访问注册表。  注册表存储有关操作系统的信息，以及有关该计算机上安装的应用程序的信息。  对注册表进行操作时，如果允许对系统资源或受保护的信息进行不适当的访问，则可能会降低安全性。  
  
## 本节内容  
 [如何：创建注册表项并设置其值](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-create-a-registry-key-and-set-its-value.md)  
 描述如何使用 `My.Computer.Registry` 对象的 `CreateSubKey` 和 `SetValue` 方法创建注册表项并将其值。  
  
 [如何：从注册表项读取值](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-read-a-value-from-a-registry-key.md)  
 描述如何使用 `My.Computer.Registry` 对象的 `GetValue` 方法读取注册表项的值。  
  
 [如何：删除注册表项](../Topic/How%20to:%20Delete%20a%20Registry%20Key%20in%20Visual%20Basic.md)  
 描述如何使用 `My.Computer.Registry.CurrentUser` 属性的 `DeleteSubKey` 方法删除注册表项。  
  
 [使用 Microsoft.Win32 命名空间读取和写入注册表](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry-using-the-microsoft-win32-namespace.md)  
 描述如何使用 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 的 `Registry` 和 `RegistryKey` 类访问注册表。  
  
 [安全性与注册表](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)  
 讨论与注册表相关的安全问题。  
  
## 相关章节  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>  
 列出并说明 `My.Computer.Registry` 对象的成员。  
  
 <xref:Microsoft.Win32.Registry>  
 提供 `Registry` 类的概述和指向各个注册表项和成员的链接。