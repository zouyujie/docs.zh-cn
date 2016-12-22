---
title: "程序结构和代码约定 (Visual Basic) | Microsoft Docs"
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
  - "编码约定"
  - "Visual Basic 代码, 编码约定"
  - "编码约定, Visual Basic"
  - "程序, 结构"
  - "程序结构"
  - "命名约定, Visual Basic"
  - "最佳实践, 编码约定"
  - "约定, Visual Basic 编码"
  - "Visual Basic 代码"
  - "编程, Visual Basic 编码约定"
ms.assetid: dd9be76f-6944-4e78-ad72-0b6084a3fc13
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 程序结构和代码约定 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本节介绍典型的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序结构，提供简单的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序“Hello, World”并且讨论 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 代码约定。  代码约定是这样一些建议，它们所针对的不是程序的逻辑，而是其物理结构和外观。  遵循这些约定能使代码更易于阅读、理解和维护。  代码约定可以包含以下内容（当然也可以包含其他内容）：  
  
-   标记和注释代码的标准化格式。  
  
-   代码间隔、格式和缩进的原则。  
  
-   对象、变量和过程的命名约定。  
  
 下面的主题叙述了为 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序建议的一系列编程原则，以及一些好的用法示例。  
  
## 本节内容  
 [Visual Basic 程序的结构](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 概述组成 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序的元素。  
  
 [Visual Basic 中的 Main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)  
 讨论作为起始点的过程以及对应用程序的总体控制。  
  
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)  
 讨论如何引用其他程序集中的对象。  
  
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)  
 描述命名空间在程序集中组织对象的方式。  
  
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)  
 包括命名过程、常数、变量、参数和对象的通用原则。  
  
 [Visual Basic 编码约定](../../../visual-basic/programming-guide/program-structure/coding-conventions.md)  
 回顾在开发此文档中的示例时所采用的原则。  
  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 描述如何有选择性地编译特定代码块并同时控制编译器忽略其他代码块。  
  
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)  
 介绍如何将长语句分成多行以及如何将短语句合并为一行。  
  
 [如何：折叠和隐藏代码节](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)  
 演示如何在 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 代码编辑器中折叠和隐藏代码段。  
  
 [如何：标记语句](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)  
 介绍如何标记要标识的代码行，便于与 `On Error Goto` 之类的语句一起使用。  
  
 [代码中的特殊字符](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)  
 介绍使用非数字字符和非字母字符的方式和场所。  
  
 [代码中的注释](../../../visual-basic/programming-guide/program-structure/comments-in-code.md)  
 讨论如何将描述性注释添加到代码中。  
  
 [代码中用作元素名称的关键字](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)  
 描述如何使用方括号 \(`[]`\) 分隔也是 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 关键字的变量名。  
  
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)  
 描述引用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序的元素的各种方法。  
  
 [Visual Basic 限制](../../../visual-basic/programming-guide/program-structure/limitations.md)  
 讨论如何在 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中消除已知的编码限制。  
  
## 相关章节  
 [版式和代码约定](../../../visual-basic/language-reference/typographic-and-code-conventions.md)  
 提供用于 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 的标准编码约定。  
  
 [编写代码](/visual-studio/ide/writing-code-in-the-code-and-text-editor)  
 描述有助于您编写和管理代码的功能。