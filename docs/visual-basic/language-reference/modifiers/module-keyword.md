---
title: "Module &lt;关键字&gt; (Visual Basic) | Microsoft Docs"
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
  - "vb.ModuleAttribute"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "特性块, Module 关键字"
  - "Module 关键字"
  - "Module 修饰符"
ms.assetid: d971b940-05ab-4d56-8485-e3b8a661906b
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Module &lt;关键字&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定位于源文件开头的特性将应用于当前程序集模块。  
  
## 备注  
 许多特性属于单个编程元素，例如类或属性。  您可以通过将特性块附加在尖括号 \(`< >`\) 内，将此类特性直接应用到声明语句。  
  
 如果特性不仅属于下面的元素，而且属于当前程序集模块，则可以将特性块放在源文件的开头，并使用 `Module` 关键字标识该特性。  如果它应用于整个程序集，则可以使用 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md) 关键字。  
  
 `Module` 修饰符与 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md) 不同。  
  
## 请参阅  
 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md)   
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)