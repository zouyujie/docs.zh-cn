---
title: "错误消息 (Visual Basic) | Microsoft Docs"
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
  - "错误信息"
  - "错误 [Visual Basic]"
  - "错误 [Visual Basic], 可捕获的"
  - "可捕获的错误"
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 错误消息 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

当您编写，编译或运行Visual Basic应用程序时，以下类型的错误可能发生:  
  
1.  设计时错误，生成，当您编写在Visual Studio的应用程序。  
  
2.  编译时错误，发生，当您生成一个应用程序在Visual Studio中或在命令提示。  
  
3.  运行时错误，生成，当您运行该应用程序在Visual Studio中或作为独立的可执行文件。  
  
 有关如何排除特定错误的信息，请参见 [为 Visual Basic 程序员提供的附加资源](../../../visual-basic/getting-started/additional-resources.md)。  
  
## 运行时错误  
 如果Visual Basic应用程序尝试执行系统无法执行的操作，则会发生运行时错误和 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 引发 `Exception` 对象。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 可以使用 `Throw` 语句生成任何数据类型的自定义错误，包括 `Exception` 对象。  应用程序可以显示所捕获的异常的错误号和消息标识该错误。  如果没有捕获到错误，则应用程序将关闭。  
  
 代码会使和检查运行时错误。  如果将产生在 `Try` 错误的代码块中，您可以找到匹配的 `Catch` 中的所有引发的错误块。  有关如何捕获错误在运行时和响应的信息它们在您的代码，请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## 编译时间错误  
 如果Visual Basic编译器在代码中遇到的问题，将产生编译时错误。  在代码编辑器中，代码行导致错误的可以方便地确定，因为波浪线下显示该行代码。  错误消息，如果您指向波浪下划线或打开 **\*\*\* 错误表 \*\*\***，还显示其他消息。  
  
 如果标识符有一条波浪下划线，并显示一条短下划线。最右侧的字符下，可以生成选件类、构造函数、方法、属性、字段或枚举生成存根。  有关更多信息，请参见[使用时生成](/visual-cpp/misc/generate-from-usage)。  
  
 通过解决从Visual Basic编译器的警告，您可能能够更快运行并具有bug较少的代码。  这些警告确定可能导致错误的代码，当应用程序运行时。  例如，编译器警告您，如果尝试调用未赋值的对象变量的成员，从函数返回，而无需设置返回值，或执行 `Try` 块并与该逻辑的错误捕获异常。  有关警告的更多信息，包括如何打开和关闭它们，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。