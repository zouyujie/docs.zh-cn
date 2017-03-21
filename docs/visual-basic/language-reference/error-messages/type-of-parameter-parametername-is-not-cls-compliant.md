---
title: "参数“&lt;参数名&gt;”的类型不符合 CLS | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40028"
  - "bc40028"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40028"
ms.assetid: dfa1f6f9-bb88-44ad-b85f-149144363d41
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 参数“&lt;参数名&gt;”的类型不符合 CLS
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

一个过程被标记为 `<CLSCompliant(True)>`，但用标记为 `<CLSCompliant(False)>` 的类型、未标记的类型或不具资格的类型（因为它是不符合的类型）声明了参数。  
  
 为使过程符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)，它必须只使用符合 CLS 的类型。  这一点适用于参数类型、返回类型及其所有局部变量的类型。  
  
 以下 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 数据类型不符合 CLS：  
  
-   [SByte 数据类型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [Ulong 数据类型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [Ushort 数据类型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 将 <xref:System.CLSCompliantAttribute> 应用于编程元素时，将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合。  此参数没有默认值，您必须提供一个值。  
  
 如果没有将 <xref:System.CLSCompliantAttribute> 应用于某个元素，则认为该元素是不符合的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40028  
  
### 更正此错误  
  
-   如果该过程必须采用此特定类型的参数，则移除 <xref:System.CLSCompliantAttribute>。  该过程无法符合 CLS。  
  
-   如果该过程必须符合 CLS，则将此参数的类型更改为最接近的符合 CLS 的类型。  例如，如果不需要 2,147,483,647 以上的数值范围，您可以使用 `Integer` 替换 `UInteger`。  如果您确实需要扩展的范围，可以将 `UInteger` 替换为 `Long`。  
  
-   如果您针对的是自动化对象或 COM 对象，请记住，某些类型具有与 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 中不同的数据宽度。  例如，`int` 在其他环境中经常是 16 位。  如果您接受来自此类组件中的 16 位整数，则在您所管理的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 代码中将其声明为 `Short` 而不是 `Integer`。  
  
## 请参阅  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)