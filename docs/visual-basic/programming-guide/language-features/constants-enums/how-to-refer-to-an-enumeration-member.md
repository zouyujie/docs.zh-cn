---
title: "如何：引用枚举成员 (Visual Basic) | Microsoft Docs"
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
  - "常量, 枚举的"
  - "枚举成员"
  - "枚举 [Visual Basic], 引用"
  - "values, 关联常量值和名称"
ms.assetid: bbb5c3cc-7cdb-4814-8d6a-a6d91546ed1e
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：引用枚举成员 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

枚举提供一种使用成组的相关常数以及将常数值与名称相关联的方便途径。  例如，可以为一组与一周中的七天相对应的整数常数声明一个枚举，然后在代码中使用这七天的名称而不是它们的整数值。  
  
 可以避免在 `Imports` 语句中使用完全限定名。  有关更多信息，请参见[枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)。  
  
### 引用枚举成员  
  
-   用枚举限定成员名称。  例如，下面的示例将 `FirstDayOfWeek` 枚举的 `Saturday` 成员分配给变量 `DayValue`。  
  
     [!code-vb[VbEnumsTask#19](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/how-to-refer-to-an-enumeration-member_1.vb)]  
  
## 请参阅  
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [如何：在 Visual Basic 中循环访问枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [如何：确定与枚举值关联的字符串](../Topic/How%20to:%20Determine%20the%20String%20Associated%20with%20an%20Enumeration%20Value%20\(Visual%20Basic\).md)   
 [何时使用枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)