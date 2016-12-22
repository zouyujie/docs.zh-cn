---
title: "#Region 指令 | Microsoft Docs"
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
  - "vb.Region"
  - "vb.#Region"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "#region 指令"
  - "#Region 关键字"
  - "region 指令 (#region)"
  - "Visual Basic 编译器, 编译器指令"
ms.assetid: 90a6a104-3cbf-47d0-bdc4-b585d0921b87
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# #Region 指令
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

折叠并隐藏 Visual Basic 文件中的代码段。  
  
## 语法  
  
```  
  
        #Region "identifier_string"  
#End Region  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`identifier_string`|必需。  当区域处于折叠状态时充当区域标题的字符串。  默认情况下，区域处于折叠状态。|  
|`#End Region`|终止 `#Region` 块。|  
  
## 备注  
 使用 `#Region` 指令指定使用 Visual Studio 代码编辑器的大纲显示功能时要展开或折叠的代码块。  你可以将区域放置（或*“嵌套”*）到其他区域中，以将类似区域组合在一起。  
  
## 示例  
 此示例使用 `#Region` 指令。  
  
 [!code-vb[VbVbalrConditionalComp#4](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/region-directive_1.vb)]  
  
## 请参阅  
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [大纲显示](/visual-studio/ide/outlining)   
 [如何：折叠和隐藏代码节](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)