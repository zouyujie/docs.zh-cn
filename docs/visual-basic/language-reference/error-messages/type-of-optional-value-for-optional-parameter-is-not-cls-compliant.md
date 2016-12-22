---
title: "可选参数 &lt;parametername&gt; 的可选值的类型不符合 CLS | Microsoft Docs"
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
  - "BC40042"
  - "vbc40042"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40042"
ms.assetid: 1d6eae29-4ad3-4434-bde4-a53b6051adf5
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 可选参数 &lt;parametername&gt; 的可选值的类型不符合 CLS
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

一个过程标记为 `<CLSCompliant(True)>`，但声明一个[可选](../../../visual-basic/language-reference/modifiers/optional.md)参数，该参数具有不符合的类型的默认值。  
  
 一个过程要符合[语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) (CLS)，必须只使用符合 CLS 的类型。 这适用于参数的类型、返回类型及其所有本地变量的类型。 也适用于可选参数的默认值。  
  
 以下 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 数据类型不符合 CLS：  
  
-   [SByte 数据类型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong 数据类型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort 数据类型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 当将 <xref:System.CLSCompliantAttribute> 特性应用到编程元素中时，需要将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合性。 此参数没有默认值，必须为其提供一个值。  
  
 如果不将 <xref:System.CLSCompliantAttribute> 应用到元素，则它将被视为不符合规范。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC40042  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
-   如果可选参数必须具有此特定类型的默认值，请删除 <xref:System.CLSCompliantAttribute>。 该过程不符合 CLS。  
  
-   如果过程必须符合 CLS，则将此默认值的类型改为最接近的符合 CLS 的类型。 例如，如果不需要 2147483647 以上的数值范围，可以使用 `UInteger` 取代 `Integer` 。 如果确实需要更大范围，可以用 `UInteger` 代替 `Long`。  
  
-   如果在与自动化或 COM 对象对接，请记住，某些类型具有与 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 中不同的数据宽度。 例如，`int` 在其他环境中通常为 16 位。 如果接受此类组件中的一个 16 位整数，则在托管的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 代码中将其声明为 `Short` 而不是 `Integer`。  
  
## <a name="see-also"></a>另请参阅  
 [\< PAVE OVER> 编写符合 CLS 的代码](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)