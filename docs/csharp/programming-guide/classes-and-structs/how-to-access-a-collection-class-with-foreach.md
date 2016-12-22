---
title: "如何：使用 foreach 访问集合类（C# 编程指南） | Microsoft Docs"
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
  - "集合类 [C#], foreach 语句"
ms.assetid: a6b9cf5c-6c8d-4223-b12c-288949434493
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：使用 foreach 访问集合类（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

下面的代码示例演示如何编写可与 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 结合使用的非泛型集合类。  该示例定义了字符串 tokenizer 类。  
  
> [!NOTE]
>  此示例描述的是仅当您无法使用泛型集合类时才采用的推荐做法。  有关如何实现支持 <xref:System.Collections.Generic.IEnumerable%601> 的类型安全的泛型集合类，请参见[迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 在该示例中，以下代码段使用 `Tokens` 类通过“ ”和“\-”分隔符将句子“This is a sample sentence.”分成若干标记。  该代码然后使用 `foreach` 语句显示这些标记。  
  
 [!code-cs[csProgGuideCollections#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_1.cs)]  
  
## 示例  
 在内部，`Tokens` 类使用数组存储这些标记。  因为数组可实现 <xref:System.Collections.IEnumerator> 和 <xref:System.Collections.IEnumerable>，所以代码示例使用了数组的枚举方法（<xref:System.Collections.IEnumerable.GetEnumerator%2A>、<xref:System.Collections.IEnumerator.MoveNext%2A>、<xref:System.Collections.IEnumerator.Reset%2A> 和 <xref:System.Collections.IEnumerator.Current%2A>），而不是在 `Tokens` 类中定义这些方法。  方法定义包括在该示例中，以明确如何定义它们以及每个定义的内容。  
  
 [!code-cs[csProgGuideCollections#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_2.cs)]  
  
 在 C\# 中，集合类不必通过实现 <xref:System.Collections.IEnumerable> 和 <xref:System.Collections.IEnumerator> 来与 `foreach` 兼容。  如果此类具有所需的 <xref:System.Collections.IEnumerable.GetEnumerator%2A>、<xref:System.Collections.IEnumerator.MoveNext%2A>、<xref:System.Collections.IEnumerator.Reset%2A> 和 <xref:System.Collections.IEnumerator.Current%2A> 成员，则可与 `foreach` 结合使用。  省略接口有一个好处：即，您可以比 <xref:System.Object> 更为具体地定义 `Current` 的返回类型。  这会提供类型安全。  
  
 例如，可更改上述示例中的以下行。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 由于 `Current` 返回字符串，因此编译器能够检测何时在 `foreach` 语句中使用了不兼容的类型，如以下代码所示。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 省略 <xref:System.Collections.IEnumerable> 和 <xref:System.Collections.IEnumerator> 的缺点是：集合类不再与其他公共语言运行时语言的 `foreach` 语句或等效语句交互。  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)