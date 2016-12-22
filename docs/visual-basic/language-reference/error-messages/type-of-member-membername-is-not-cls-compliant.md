---
title: "成员“&lt;成员名&gt;”的类型不符合 CLS | Microsoft Docs"
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
  - "bc40025"
  - "vbc40025"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40025"
ms.assetid: adbd34bb-43d2-4266-90e7-cd1afaf49b4e
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 成员“&lt;成员名&gt;”的类型不符合 CLS
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

为此成员指定的数据类型不是 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\) 的组成部分。  在您的组件中，这不是错误，因为 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 和 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 支持此数据类型。  但是，另一个在严格符合 CLS 的代码中编写的组件可能不支持此数据类型。  此类组件可能无法与您的组件成功进行交互。  
  
 以下 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 数据类型不符合 CLS：  
  
-   [SByte 数据类型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [Ulong 数据类型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [Ushort 数据类型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的更多信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40025  
  
### 更正此错误  
  
-   如果您的组件只与其他 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 组件交互，或者不与任何其他组件交互，您无需更改任何内容。  
  
-   如果要与并非针对 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 编写的组件交互，您可能能够通过反射或依据文档确定它是否支持此数据类型。  如果支持，您无需更改任何内容。  
  
-   如果要与不支持此数据类型的组件交互，您必须将其替换为最接近的符合 CLS 的类型。  例如，如果不需要 2,147,483,647 以上的数值范围，您可以使用 `Integer` 替换 `UInteger`。  如果您确实需要扩展的范围，可以将 `UInteger` 替换为 `Long`。  
  
-   如果您针对的是自动化对象或 COM 对象，请记住，某些类型具有与 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 中不同的数据宽度。  例如，`uint` 在其他环境中通常为 16 位。  如果要将某个 16 位参数传递给此类组件，请在托管 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 代码中将其声明为 `UShort`（而不是 `UInteger`）。  
  
## 请参阅  
 [反射](../Topic/Reflection%20in%20the%20.NET%20Framework.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)