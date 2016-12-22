---
title: "/codepage (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/codepage"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/codepage compiler option [C#]"
  - "codepage compiler option [C#]"
  - "-codepage compiler option [C#]"
ms.assetid: 75942989-b69a-4308-90a0-840c73d2c478
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /codepage (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此选项指定在编译期间，当所需的页不是系统当前的默认代码页时使用的代码页。  
  
## 语法  
  
```  
/codepage:id  
```  
  
## 参数  
 `id`  
 编译中用于所有源代码文件的代码页的 ID。  
  
## 备注  
 如果编译的一个或多个源代码文件没有被创建为使用计算机上的默认代码页，则可以使用 **\/codepage** 选项指定应使用哪个代码页。  **\/codepage** 适用于编译中的所有源代码文件。  
  
 如果源代码文件是用计算机中的同一有效代码页创建的，或者是用 UNICODE 或 UTF\-8 创建的，则不需要使用 **\/codepage**。  
  
 有关如何 [GetCPInfo](http://go.microsoft.com/fwlink/?LinkId=148371) 查找系统上支持哪些代码页的信息。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)