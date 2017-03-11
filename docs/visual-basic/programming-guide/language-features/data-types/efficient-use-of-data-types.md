---
title: "有效使用数据类型 (Visual Basic) | Microsoft Docs"
ms.custom: ""
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
  - "AscW 函数, 优先于 Asc 使用"
  - "ChrW 函数, 优先于 Chr 使用"
  - "数据类型 [Visual Basic], 优化"
  - "数据类型 [Visual Basic], 强类型化"
  - "数据类型 [Visual Basic], 有效使用"
  - "数据类型 [Visual Basic], 弱类型化"
  - "优化, 数据类型"
  - "性能, 数据类型效率"
  - "强类型化"
  - "类型化, strong"
ms.assetid: 28f5e4ba-ec24-4f37-b90a-e8ee822f778a
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 有效使用数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

将为未声明的变量和虽声明但无数据类型的变量分配 `Object` 数据类型。  这使得可以轻松地快速编写程序，但这样会导致程序的执行速度更慢。  
  
## 强类型  
 为所有变量指定数据类型称为“强类型”。  使用强类型有以下优点：  
  
-   它启用 IntelliSense 为您的变量支持。  这允许您在输入代码时看到变量的属性和其他成员。  
  
-   它会运用编译器类型检查。  这将捕捉到因溢出等错误而在运行时失败的语句。  这也可以在不支持方法的对象上捕捉对方法的调用。  
  
-   使代码的执行速度更快。  
  
## 最有效的数据类型  
 对于从不包含小数的变量，整型数据类型比非整型的效率高。  在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中，`Integer` 和 `UInteger` 是最有效的数值类型。  
  
 对于分数，`Double` 是最有效的数据类型，因为当前平台上的处理器以双精度形式执行浮点运算。  但是，使用 `Double` 的运算不如使用整型（如 `Integer`）的运算速度快。  
  
## 指定数据类型  
 使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 声明特定类型的变量。  同时，可以使用 [Public](../../../../visual-basic/language-reference/modifiers/public.md)、[Protected](../../../../visual-basic/language-reference/modifiers/protected.md)、[Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 或 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 关键字指定它的访问级别，如下例所示。  
  
```  
Private x As Double  
Protected s As String  
```  
  
## 字符转换  
 `AscW` 和 `ChrW` 函数以 Unicode 进行操作。  应将它们优先于 `Asc` 和 `Chr`（它们必须进行 Unicode 转换）而使用。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [数值型数据类型](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [使用 IntelliSense](/visual-studio/ide/using-intellisense)