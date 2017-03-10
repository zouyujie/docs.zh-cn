---
title: "“Declare”语句中不支持“As Any” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30828"
  - "vbc30828"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30828"
ms.assetid: 7e5cf519-8b64-4ac5-8116-705fe26c846d
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# “Declare”语句中不支持“As Any”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在 Visual Basic 6.0 和更早的版本中，`Any` 数据类型用在 `Declare` 语句中，以允许使用可包含任意数据类型的参数。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 支持重载，但也因此使得 `Any` 数据类型过时。  
  
 **错误 ID：**BC30828  
  
### 更正此错误  
  
1.  声明要使用的特定类型的参数；例如：  
  
     [!code-vb[VbVbalrStatements#95](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/as-any-is-not-supported-_1.vb)]  
  
2.  如果调用的过程需要 `Void*`，请使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性指定 `As Any`。  
  
     [!code-vb[VbVbalrStatements#96](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/as-any-is-not-supported-_2.vb)]  
  
## 请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [在托管代码中创建原型](../Topic/Creating%20Prototypes%20in%20Managed%20Code.md)