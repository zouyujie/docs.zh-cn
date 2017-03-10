---
title: "/utf8output (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/utf8output"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "utf8output compiler option [C#]"
  - "/utf8output compiler option [C#]"
  - "-utf8output compiler option [C#]"
ms.assetid: 27ff7381-c281-45d7-b2eb-1ad644b1354e
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# /utf8output (C# Compiler Options)
**\/utf8output** 选项使用 UTF\-8 编码显示编译器输出。  
  
## 语法  
  
```  
/utf8output  
```  
  
## 备注  
 在某些国际配置中，编译器输出无法在控制台上正确显示。  在这些配置中，请使用 **\/utf8output** 并将编译器输出重定向到文件。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)