---
title: "如何：折叠和隐藏代码节 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic 代码, 折叠和隐藏"
  - "Visual Basic, 代码折叠"
  - "Visual Basic, 代码隐藏"
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：折叠和隐藏代码节 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`#Region` 指令使您能够折叠和隐藏 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 文件中的代码节。  `#Region` 指令可用于指定在使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 代码编辑器时可以展开或折叠的代码块。  有选择地隐藏代码的能力使文件更易于管理和读取。  有关更多信息，请参见 [大纲显示](/visual-studio/ide/outlining)。  
  
 `#Region` 指令支持代码块语义，如 `#If...#End If`。  这意味着它们不能在一个块内开始并在另一个块内结束；开始与结束必须在同一个块内。  在函数内部不支持 `#Region` 指令。  
  
### 折叠并隐藏代码节  
  
-   将代码节放在 `#Region` 和 `#End Region` 语句之间，如下例所示：  
  
     [!code-vb[VbVbalrConditionalComp#6](../../../visual-basic/language-reference/directives/codesnippet/visualbasic/how-to-collapse-and-hide_1.vb)]  
  
     在代码文件中可多次使用 `#Region` 块；因此，用户可定义自己的过程块和类块，这些块可依次折叠。  `#Region` 块也可嵌套在其他 `#Region` 块内。  
  
    > [!NOTE]
    >  隐藏代码不会使其无法编译，且不会影响 `#If...#End If` 语句。  
  
## 请参阅  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [\#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)   
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [大纲显示](/visual-studio/ide/outlining)