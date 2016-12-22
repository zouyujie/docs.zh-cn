---
title: "“&lt;过程签名 1&gt;”不符合 CLS，因为它重载仅在数组参数类型的数组或数组参数类型的秩方面与它不同的“&lt;过程签名 2&gt;” | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc40035"
  - "bc40035"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40035"
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “&lt;过程签名 1&gt;”不符合 CLS，因为它重载仅在数组参数类型的数组或数组参数类型的秩方面与它不同的“&lt;过程签名 2&gt;”
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

当某个过程或属性重写了另一个过程或属性，并且它们的参数列表之间的唯一差异是交错数组的嵌套级别或数组的秩时，该过程或属性被标记为 `<CLSCompliant(True)>`。  
  
 在以下声明中，第二个和第三个声明会产生此错误。  
  
 `Overloads Sub processArray(ByVal arrayParam() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam()() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam(,) As Integer)`  
  
 第二个声明将原始一维参数 `arrayParam` 更改为数组的数组。  第三个声明将 `arrayParam` 更改为一个二维数组（秩为 2）。  尽管 Visual Basic 允许重载只是在其中某项更改上不同，但此类重载操作不符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)。  
  
 将 <xref:System.CLSCompliantAttribute> 应用于编程元素时，将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合。  此参数没有默认值，您必须提供一个值。  
  
 如果没有将 <xref:System.CLSCompliantAttribute> 应用于某个元素，则认为该元素是不符合的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40035  
  
### 更正此错误  
  
-   如果需要符合 CLS，请对重载进行定义，以使它们在多个方面（而不只是在此帮助页面上所引用的这些更改方面）相互不同。  
  
-   如果需要重载只是在此帮助页面上所引用的这些更改方面有所不同，请从它们的定义中移除 <xref:System.CLSCompliantAttribute>，或将它们标记为 `<CLSCompliant(False)>`。  
  
## 请参阅  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)   
 [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md)