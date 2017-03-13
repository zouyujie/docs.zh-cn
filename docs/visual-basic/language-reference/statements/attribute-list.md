---
title: "特性列表 (Visual Basic) | Microsoft Docs"
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
  - "特性列表"
  - "特性 [Visual Basic], 应用"
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 特性列表 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定要应用于已声明的编程元素的特性。  多个特性以逗号分隔。  以下是一个特性的语法。  
  
## 语法  
  
```  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## 部件  
 `attributemodifier`  
 对于用于源文件起始处的特性，为必选项。  可以为 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md) 或 [Module](../../../visual-basic/language-reference/modifiers/module-keyword.md)。  
  
 `attributename`  
 必选。  特性名。  
  
 `attributearguments`  
 可选。  该特性的定位参数列表。  多个参数以逗号分隔。  
  
 `attributeinitializer`  
 可选。  该特性的变量或属性初始值设定项列表。  多个初始值设定项以逗号分隔。  
  
## 备注  
 可以将一个或多个特性应用于几乎任何一个编程元素（类型、过程、属性等）。  特性显示在程序集的元数据中，它们可以帮助您批注代码或指定如何使用特定的编程元素。  您可以应用 Visual Basic 和 .NET Framework 定义的特性，也可以定义您自己的特性。  
  
 有关何时使用特性的更多信息，请参见[特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)。  有关特性名称的信息，请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## 规则  
  
-   **位置。**可以将特性应用于大多数已声明的编程元素。  若要应用一个或多个特性，请在元素声明的起始处放置“属性块”。  特性列表中的每一项均指定一个您要应用的特性，以及用于该特性调用的修饰符和参数。  
  
-   **尖括号。**如果您提供了特性列表，必须将其置于尖括号内（“`<`”和“`>`”）。  
  
-   **声明的一部分。**特性必须为元素声明的一部分，而不是独立的语句。  您可以使用行继续序列 \(" `_`"\) 将声明语句扩展到多个源代码行。  
  
-   **修饰符。**在应用于源文件起始处的编程元素的每个特性中，必须使用特性修饰符（`Assembly` 或 `Module`）。  在非应用于源文件起始处的元素的特性中，不允许使用特性修饰符。  
  
-   **参数。**特性的所有定位参数必须位于任何变量或属性初始值设定项之前。  
  
## 示例  
 下面的示例将 <xref:System.Runtime.InteropServices.DllImportAttribute> 特性应用于 `Function` 过程的主干定义中。  
  
 [!code-vb[VbVbalrStatements#1](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/attribute-list_1.vb)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute> 指示该特性过程表示非托管动态链接库 \(DLL\) 中的一个入口点。  该特性提供 DLL 名称作为一个定位参数，并提供其他信息作为变量初始值设定项。  
  
## 请参阅  
 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md)   
 [Module \<keyword\>](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)