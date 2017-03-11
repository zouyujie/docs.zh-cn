---
title: "程序集 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Assembly"
  - "vb.AssemblyAttribute"
  - "Assembly"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Assembly 关键字"
  - "Assembly 修饰符"
  - "特性块, Assembly 关键字"
ms.assetid: 925e7471-3bdf-4b51-bb93-cbcfc6efc52f
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 程序集 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定源文件开始处的特性应用到整个程序集。  
  
## 备注  
 许多特性属于单个编程元素，例如类或属性。  您可以通过将特性块附加在尖括号 \(`< >`\) 内，将此类特性直接应用到声明语句。  
  
 如果一个特性不仅属于后面的元素，还属于整个程序集，则将特性块放置在源文件的开始处，并用 `Assembly` 关键字标识该特性。  如果该属性适用于当前的程序集模块，则可以使用 [Module](../../../visual-basic/language-reference/modifiers/module-keyword.md) 关键字。  
  
 也可以将一个特性应用到 AssemblyInfo.vb 文件中的一个程序集，这时您不必在主源代码文件中使用特性块。  
  
## 请参阅  
 [Module \<keyword\>](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)