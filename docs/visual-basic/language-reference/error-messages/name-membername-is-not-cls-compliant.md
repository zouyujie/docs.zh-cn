---
title: "名称 &lt;成员名&gt; 不符合 CLS | Microsoft Docs"
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
  - "bc40031"
  - "vbc40031"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40031"
ms.assetid: e2b885dc-cbf9-49ff-bbbe-531657ea99f7
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 名称 &lt;成员名&gt; 不符合 CLS
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

一个程序集被标记为 `<CLSCompliant(True)>`，但它用以下划线 \(`_`\) 开头的名称公开了一个成员。  
  
 编程元素可以包含一个或多个下划线，但为了符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)，它不得以下划线开头。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
 将 <xref:System.CLSCompliantAttribute> 应用于编程元素时，将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合。  此参数没有默认值，您必须提供一个值。  
  
 如果没有将 <xref:System.CLSCompliantAttribute> 应用于某个元素，则认为该元素是不符合的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40031  
  
### 更正此错误  
  
-   如果您可以控制源代码，请更改成员名称，使它不以下划线开头。  
  
-   如果您要求成员名称保持不变，请从其定义中移除 <xref:System.CLSCompliantAttribute>，或者将它标记为 `<CLSCompliant(False)>`。  您仍可以将程序集标记为 `<CLSCompliant(True)>`。  
  
## 请参阅  
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)