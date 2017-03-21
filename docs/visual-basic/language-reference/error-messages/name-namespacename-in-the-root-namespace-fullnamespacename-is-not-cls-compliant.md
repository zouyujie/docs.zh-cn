---
title: "根命名空间 &lt;完整命名空间&gt; 中的名称 &lt;命名空间名称&gt; 不符合 CLS | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40039"
  - "bc40039"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40039"
ms.assetid: c5bd5914-ae71-416a-8bed-f76f644f78be
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 根命名空间 &lt;完整命名空间&gt; 中的名称 &lt;命名空间名称&gt; 不符合 CLS
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

程序集标记为 `<CLSCompliant(True)>`，但根命名空间名称的某个元素以下划线 \(`_`\) 开头。  
  
 编程元素可以包含一个或多个下划线，但为了符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)，它不得以下划线开头。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
 将 <xref:System.CLSCompliantAttribute> 应用于编程元素时，将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合。  此参数没有默认值，您必须提供一个值。  
  
 如果没有将 <xref:System.CLSCompliantAttribute> 应用于某个元素，则认为该元素是不符合的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40039  
  
### 更正此错误  
  
-   如果需要符合 CLS，请更改根命名空间名称，以使它的任何元素都不以下划线开头。  
  
-   如果需要保持命名空间名称不变，请从程序集中移除 <xref:System.CLSCompliantAttribute>，或将其标记为 `<CLSCompliant(False)>`。  
  
## 请参阅  
 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [\/rootnamespace](../../../visual-basic/reference/command-line-compiler/rootnamespace.md)   
 [“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)