---
title: "名称“&lt;名称&gt;”未声明 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30451"
  - "vbc30451"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30451"
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 名称“&lt;名称&gt;”未声明
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

语句引用某个编程元素，但编译器无法找到具有该确切名称的元素。  
  
 **错误 ID：**BC30451  
  
### 更正此错误  
  
1.  检查提及的语句中的名称的拼写。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 是不区分大小写的，但是拼写中的任何其他变化都会被视为完全不同的名称。  请注意，下划线 \(`_`\) 是名称的一部分，因此也是拼写的一部分。  
  
2.  检查对象和对象的成员之间是否具有成员访问运算符 \(`.`\)。  例如，如果具有名为 `TextBox1` 的 <xref:System.Windows.Forms.TextBox> 控件，若要访问它的 <xref:System.Windows.Forms.TextBoxBase.Text%2A> 属性，您应该键入 `TextBox1.Text`。  而如果您键入的是 `TextBox1Text`，就会创建不同的名称。  
  
3.  如果拼写是正确的，任何对象成员访问的语法也是正确的，请验证是否声明了该元素。  有关更多信息，请参见 [已声明的元素](../../../visual-basic/programming-guide/language-features/declared-elements/index.md)。  
  
4.  如果已声明该编程元素，请检查它是否在范围内。  如果引用语句在声明该编程元素的区域外，您可能需要限定该元素名称。  有关更多信息，请参见 [Visual Basic 中的范围](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)。  
  
## 请参阅  
 [声明和常量摘要](../../../visual-basic/language-reference/keywords/declarations-and-constants-summary.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)