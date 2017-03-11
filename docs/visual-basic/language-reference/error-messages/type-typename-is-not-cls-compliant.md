---
title: "类型 &lt;类型名&gt; 不符合 CLS | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc40041"
  - "vbc40041"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40041"
ms.assetid: 634132c2-5646-44aa-98c6-f773e2e63882
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 类型 &lt;类型名&gt; 不符合 CLS
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使用不符合 CLS 的数据类型声明了变量、属性或函数返回值。  
  
 要使应用程序符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)，它必须只能使用符合 CLS 的类型。  
  
 以下 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 数据类型不符合 CLS：  
  
-   [SByte 数据类型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [Ulong 数据类型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [Ushort 数据类型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 **错误 ID：**BC40041  
  
### 更正此错误  
  
-   如果应用程序需要符合 CLS，请将此元素的数据类型更改为最接近的符合 CLS 的类型。  例如，如果不需要 2,147,483,647 以上的数值范围，您可以使用 `Integer` 替换 `UInteger`。  如果您确实需要扩展的范围，可以将 `UInteger` 替换为 `Long`。  
  
-   如果应用程序不需要符合 CLS，则无需更改任何内容。  但是，您应知道它是不符合的。  
  
## 请参阅  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)