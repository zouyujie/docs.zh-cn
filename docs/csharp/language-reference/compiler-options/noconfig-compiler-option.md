---
title: "/noconfig (C# Compiler Options) | Microsoft Docs"
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
  - "/noconfig"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/noconfig compiler option [C#]"
  - "csc.rsp"
  - "-noconfig compiler option [C#]"
  - "noconfig compiler option [C#]"
ms.assetid: cd26967e-e494-4c8c-b5c9-af13b2f78b2e
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /noconfig (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/noconfig** 选项通知编译器不要使用 csc.rsp 文件进行编译，该文件与 csc.exe 文件位于同一目录中，并从该目录中加载。  
  
## 语法  
  
```  
/noconfig  
```  
  
## 备注  
 csc.rsp 文件引用 .NET Framework 附带的所有程序集。  Visual Studio .NET 开发环境包括的实际引用具体取决于项目类型。  
  
 可以修改 csc.rsp 文件并指定其他编译器选项，而这些选项是那些应该包括在使用 csc.exe 的来自命令行的每次编译中的选项（**\/noconfig** 选项除外）。  
  
 编译器会保留上次传递给 **csc** 命令的选项。  因此，命令行上的任何选项都会重写 csc.rsp 文件中同一选项的设置。  
  
 如果不希望编译器查找并使用 csc.rsp 文件中的设置，请指定 **\/noconfig**。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)