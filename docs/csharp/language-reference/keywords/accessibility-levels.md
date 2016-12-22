---
title: "可访问性级别（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "访问修饰符 [C#], 可访问性级别"
  - "可访问性级别"
ms.assetid: dc083921-0073-413e-8936-a613e8bb7df4
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 可访问性级别（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用访问修饰符 [public](../../../csharp/language-reference/keywords/public.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 [private](../../../csharp/language-reference/keywords/private.md) 可以为成员指定以下声明的访问级别之一。  
  
|声明的可访问性|含义|  
|-------------|--------|  
|`public`|访问不受限制。|  
|`protected`|访问仅限于包含类或从包含类派生的类型。|  
|`internal`|访问仅限于当前程序集。|  
|`protected` `internal`|访问仅限于从包含类派生的当前程序集或类型。|  
|`private`|访问仅限于包含类型。|  
  
 一个成员或类型只能有一个访问修饰符，但使用 `protected` `internal` 组合时除外。  
  
 命名空间上不允许使用访问修饰符。  命名空间没有访问限制。  
  
 根据出现成员声明的上下文，只允许某些声明的可访问性。  如果在成员声明中未指定访问修饰符，则使用默认的可访问性。  
  
 不嵌套在其他类型中的顶级类型的可访问性只能是 `internal` 或 `public`。  这些类型的默认可访问性是 `internal`。  
  
 嵌套类型是其他类型的成员，它们可以具有下表所示的声明的可访问性。  
  
|属于|默认的成员可访问性|该成员允许的声明的可访问性|  
|--------|---------------|-------------------|  
|`enum`|`public`|无|  
|`class`|`private`|`public`<br /><br /> `protected`<br /><br /> `internal`<br /><br /> `private`<br /><br /> `protected` `internal`|  
|`interface`|`public`|无|  
|`struct`|`private`|`public`<br /><br /> `internal`<br /><br /> `private`|  
  
 嵌套类型的可访问性取决于它的[可访问域](../../../csharp/language-reference/keywords/accessibility-domain.md)，该域是由已声明的成员可访问性和直接包含类型的可访问域这二者共同确定的。  但是，嵌套类型的可访问域不能超出包含类型的可访问域。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [可访问域](../../../csharp/language-reference/keywords/accessibility-domain.md)   
 [对使用可访问性级别的限制](../../../csharp/language-reference/keywords/restrictions-on-using-accessibility-levels.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)