---
title: "指令 (Visual Basic) | Microsoft Docs"
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
  - "指令"
  - "指令, Visual Basic 编译器"
  - "Visual Basic 代码, 指令"
ms.assetid: 20d5fe65-490a-4c23-88c2-ee4f490ed762
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 指令 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本节中的主题记录 Visual Basic 源代码编译器指令。  
  
## 本节内容  
 [\#Const 指令](../../../visual-basic/language-reference/directives/const-directive.md)：定义编译器常量  
  
 [\#ExternalSource 指令](../../../visual-basic/language-reference/directives/externalsource-directive.md)：指示源行和源的外部文本之间的映射  
  
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)：编译选定的代码块  
  
 [\#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)：折叠并隐藏 Visual Studio 编辑器中的代码段  
  
 **\#Disable, \#Enable**：禁用和启用地区代码的特定警告。  
  
```vb  
#Disable Warning BC42356 ' suppress warning about no awaits in this method  
    Async Function TestAsync() As Task  
        Console.WriteLine("testing")  
    End Function  
#Enable Warning BC42356  
  
```  
  
 还可以禁用和启用以逗号分隔的警告代码列表。  
  
## 相关章节  
 [Visual Basic 语言参考](../../../visual-basic/language-reference/index.md)  
  
 [Visual Basic](../../../visual-basic/index.md)