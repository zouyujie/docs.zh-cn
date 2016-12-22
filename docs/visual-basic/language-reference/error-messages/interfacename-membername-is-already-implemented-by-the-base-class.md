---
title: "“&lt;interfacename&gt;.&lt;membername&gt;”已由基类“&lt;baseclassname&gt;”实现。假定重新实现 &lt;type&gt; | Microsoft Docs"
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
  - "vbc42015"
  - "bc42015"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42015"
ms.assetid: 658c070a-113e-4bd8-b294-12c243191160
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “&lt;interfacename&gt;.&lt;membername&gt;”已由基类“&lt;baseclassname&gt;”实现。假定重新实现 &lt;type&gt;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

派生类中的属性、过程或事件使用了指定某个接口成员的 `Implements` 子句，该成员已在基类中实现。  
  
 派生类可重新实现由其基类实现的接口成员。  这与重写基类实现不同。  有关更多信息，请参见 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md)。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42015  
  
### 更正此错误  
  
-   如果打算重新实现接口成员，您无需采取任何措施。  除非您使用 `MyBase` 关键字来访问基类实现，否则派生类中的代码将访问重新实现的成员。  
  
-   如果不想重新实现接口成员，则从属性、过程或事件声明中移除 `Implements` 子句。  
  
## 请参阅  
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)