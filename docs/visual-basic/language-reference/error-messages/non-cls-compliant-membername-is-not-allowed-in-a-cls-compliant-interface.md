---
title: "在符合 CLS 的接口中不允许出现不符合 CLS 的 &lt;成员名称&gt; | Microsoft Docs"
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
  - "bc40033"
  - "vbc40033"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40033"
ms.assetid: 060c4b08-798e-40f1-94cf-c05c524f1b8a
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 在符合 CLS 的接口中不允许出现不符合 CLS 的 &lt;成员名称&gt;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

当接口本身被标记为 `<CLSCompliant(False)>` 或不标记时，接口中的属性、过程或事件会被标记为 `<CLSCompliant(True)>`。  
  
 要使接口符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)，那么接口的所有成员都必须是符合的。  
  
 将 <xref:System.CLSCompliantAttribute> 应用于编程元素时，将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合。  此参数没有默认值，您必须提供一个值。  
  
 如果没有将 <xref:System.CLSCompliantAttribute> 应用于某个元素，则认为该元素是不符合的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40033  
  
### 更正此错误  
  
-   如果您要求符合 CLS，并且可以对接口源代码进行控制，则将该接口标记为 `<CLSCompliant(True)>`（前提是它的所有成员都是符合的）。  
  
-   如果您要求符合 CLS，但不可以对接口源代码进行控制，或者如果其不具备符合的条件，则在其他接口中定义此成员。  
  
-   如果您要求此成员保留在其当前的接口中，请从它的定义中移除 <xref:System.CLSCompliantAttribute>，或将其标记为 `<CLSCompliant(False)>`。  
  
## 请参阅  
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)