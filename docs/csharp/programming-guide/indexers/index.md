---
title: "索引器（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.indexers"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 索引器"
  - "索引器 [C#]"
ms.assetid: 022cd27d-d5e0-4cfe-8b97-dc018cc3355d
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# 索引器（C# 编程指南）
索引器允许类或结构的实例就像数组一样进行索引。  索引器类似于[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)，不同之处在于它们的取值函数采用参数。  
  
 在下面的示例中，定义了一个泛型类，并为其提供了简单的 [get](../../../csharp/language-reference/keywords/get.md) 和 [set](../../../csharp/language-reference/keywords/set.md) 取值函数方法（作为分配和检索值的方法）。  `Program` 类创建了此类的一个实例，用于存储字符串。  
  
 [!code-cs[csProgGuideIndexers#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/index_1.cs)]  
  
> [!NOTE]
>  有关更多示例，请参阅[相关章节](../../../csharp/programming-guide/indexers/index.md#BKMK_RelatedSections)。  
  
## 表达式主体定义  
 直接只返回表达式结果的索引器很常见。  下面的语法快捷方式使用 `=>` 来定义这些索引器：  
  
```c#  
public Customer this[long id] => store.LookupCustomer(id);  
  
```  
  
 索引器必须为只读，并且你不能使用 `get` 取值函数关键字。  
  
## 索引器概述  
  
-   使用索引器可以用类似于数组的方式为对象建立索引。  
  
-   `get` 取值函数返回值。  `set` 取值函数分配值。  
  
-   [this](../../../csharp/language-reference/keywords/this.md) 关键字用于定义索引器。  
  
-   [value](../../../csharp/language-reference/keywords/value.md) 关键字用于定义由 `set` 索引器分配的值。  
  
-   索引器不必根据整数值进行索引；由你决定如何定义特定的查找机制。  
  
-   索引器可被重载。  
  
-   索引器可以有多个形参，例如当访问二维数组时。  
  
##  <a name="BKMK_RelatedSections"></a> 相关章节  
  
-   [使用索引器](../../../csharp/programming-guide/indexers/using-indexers.md)  
  
-   [接口中的索引器](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)  
  
-   [属性和索引器之间的比较](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)