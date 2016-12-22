---
title: "变量“&lt;变量名&gt;”在赋值前被使用 | Microsoft Docs"
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
  - "vbc42104"
  - "BC42104"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42104"
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 变量“&lt;变量名&gt;”在赋值前被使用
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

变量“\<variablename\>”在赋值前被使用。可能会在运行时导致 null 引用异常。  
  
 在将任意值赋给某个变量之前，应用程序代码中至少有一条可能的路径读取了该变量。  
  
 如果从来没有为某个变量赋过值，则该变量包含其数据类型的默认值。  对于引用数据类型，该默认值为 [Nothing](../../../visual-basic/language-reference/nothing.md)。  在某些情况下，如果读取值为 `Nothing` 的引用变量，则可能引发 <xref:System.NullReferenceException>。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的更多信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42104  
  
### 更正此错误  
  
-   检查控制流逻辑，并确保变量在控制权传递到任何读取它的语句之前具有有效的值。  
  
-   保证变量始终具有有效值的一种方法是：将该变量作为其声明的一部分加以初始化。  请参见 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md) 中的“初始化”。  
  
## 请参阅  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [变量声明](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [变量疑难解答](../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)