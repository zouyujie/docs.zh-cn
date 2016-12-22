---
title: "/langversion (Visual Basic) | Microsoft Docs"
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
  - "/langversion 编译器选项 [Visual Basic]"
  - "langversion 编译器选项 [Visual Basic]"
  - "-langversion 编译器选项 [Visual Basic]"
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /langversion (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使编译器仅接受指定 Visual Basic 语言版本中所包含的语法。  
  
## 语法  
  
```  
/langversion:version  
```  
  
## 参数  
 `version`  
 必选。  要在编译期间使用的语言版本。  可接受的值为 `9`、`9.0`、 `10` 和 `10.0`。  
  
## 备注  
 `/langversion` 选项指定编译器接受的语法。  例如，如果指定语言版本为 9.0，则对于仅在 10.0 版及更高版本中有效的语法，编译器会生成错误。  
  
 在开发面向不同版本 .NET Framework 的应用程序时，可以使用此选项。  例如，如果面向的是 .NET Framework 3.5，则可以使用此选项以确保不使用语言版本 10.0 的语法。  
  
 只能使用命令行直接设置 `/langversion`。  有关更多信息，请参见[面向特定的 .NET Framework 版本](/visual-studio/ide/targeting-a-specific-dotnet-framework-version)。  
  
## 示例  
 下面的代码针对 Visual Basic 9.0 编译 `sample.vb`。  
  
```  
vbc /langversion:9.0 sample.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [面向特定的 .NET Framework 版本](/visual-studio/ide/targeting-a-specific-dotnet-framework-version)