---
title: "“Extension”特性只能应用于“Module”、“Sub”或“Function”声明。 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc36550"
  - "vbc36550"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36550"
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “Extension”特性只能应用于“Module”、“Sub”或“Function”声明。
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 Visual Basic 中扩展数据类型的唯一方式是在标准模块内定义一个扩展方法。  扩展方法可以是 `Sub` 过程或 `Function` 过程。  所有扩展方法都必须使用 <xref:System.Runtime.CompilerServices?displayProperty=fullName> 命名空间中的扩展特性 `<Extension()>` 进行标记。  还可以根据需要以相同的方式标记包含扩展方法的模块。  扩展特性的其他使用方式均无效。  
  
 **错误 ID：**BC36550  
  
### 更正此错误  
  
-   移除扩展特性。  
  
-   将扩展重新设计为在封闭模块中定义的方法。  
  
## 示例  
 下面的示例为 `String` 数据类型定义了 `Print` 方法。  
  
```  
Imports StringUtility  
Imports System.Runtime.CompilerServices  
Namespace StringUtility  
    <Extension()>   
    Module StringExtensions  
        <Extension()>   
        Public Sub Print (ByVal str As String)  
            Console.WriteLine(str)  
        End Sub  
    End Module  
End Namespace  
  
```  
  
## 请参阅  
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)