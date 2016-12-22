---
title: "错误类型 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "错误 [Visual Basic], 逻辑"
  - "错误 [Visual Basic], 语法"
  - "错误 [Visual Basic], 类型"
  - "异常, 类型"
  - "逻辑错误, Visual Basic"
  - "运行时错误, 错误类型"
  - "语法错误, Visual Basic"
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 错误类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中，错误（也称为“异常”）分为三类：语法错误、运行时错误和逻辑错误。  
  
## 语法错误  
 “语法错误”是编写代码时出现的错误。  当您在**“代码编辑器”**窗口中键入代码时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会对其进行检查并在您出现错误（如拼错单词或者不正确地使用语言元素）时提醒您。  语法错误是最普通类型的错误。  这类错误一发生，就可以在代码环境中很容易地修复它们。  
  
> [!NOTE]
>  `Option Explicit` 语句是避免语法错误的一种方式。  它强制您事先声明所有将用于应用程序的变量。  因此，当那些变量用于代码时，任何版式错误都将被立即捕获并修复。  
  
## 运行时错误  
 “*运行时错误”*是仅在编译并运行代码后出现的错误，  其中包括可能看上去正确（因为代码中没有语法错误）但不会执行的代码。  例如，可能正确地写了一行打开某个文件的代码。  但是，如果该文件损坏，应用程序将无法执行 `Open` 函数，它会停止运行。  通过重写有错误的代码，然后重新编译并重新运行该代码，可以修复大多数运行时错误。  
  
## 逻辑错误  
 “*逻辑错误”*是只要使用应用程序就会出现的错误。  通常，当响应用户操作时，最不希望出现这样的结果。  例如，错误键入的键或其他外部影响可能会导致应用程序在所需的参数内停止运行，或完全停止运行。  逻辑错误通常是最难修复的类型，因为它们发生的位置一般都不明确。  
  
## 请参阅  
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [调试器基础知识](/visual-studio/debugger/debugger-basics)