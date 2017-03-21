---
title: "“&lt;类名&gt;”不符合 CLS，因为它所实现的接口“&lt;接口名&gt;”不符合 CLS | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc40029"
  - "vbc40029"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40029"
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# “&lt;类名&gt;”不符合 CLS，因为它所实现的接口“&lt;接口名&gt;”不符合 CLS
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

当类或接口派生自标记为 `<CLSCompliant(False)>` 的类型或未标记的类型时，或者当类或接口实现这样的类型时，该类或接口被标记为 `<CLSCompliant(True)>`。  
  
 为使类或接口符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)，其整个继承层次结构必须是符合的。  这意味着它继承自的每种类型（无论是直接继承还是间接继承）都必须是符合的。  同样，如果某个类实现一个或多个接口，则这些接口在它们的整个继承层次结构中都必须符合该规范。  
  
 将 <xref:System.CLSCompliantAttribute> 应用于编程元素时，将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合。  此参数没有默认值，您必须提供一个值。  
  
 如果没有将 <xref:System.CLSCompliantAttribute> 应用于某个元素，则认为该元素是不符合的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40029  
  
### 更正此错误  
  
-   如果您要求符合 CLS，请在不同的继承层次结构或实现方案中定义此类型。  
  
-   如果您要求此类型保留在其当前的继承层次结构内或实现方案内，则从其定义中移除 <xref:System.CLSCompliantAttribute>，并将其标记为 `<CLSCompliant(False)>`。  
  
## 请参阅  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/zh-cn/4c705105-69a2-4e5e-b24e-0633bc32c7f3)