---
title: "使用索引器（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "索引器 [C#], 关于索引器"
ms.assetid: df70e1a2-3ce3-4aba-ad80-4b2f3538699f
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# 使用索引器（C# 编程指南）
索引器在语法上方便您创建客户端应用程序可将其作为数组访问的[类](../../../csharp/language-reference/keywords/class.md)、[结构](../../../csharp/language-reference/keywords/struct.md)或[接口](../../../csharp/language-reference/keywords/interface.md)。  索引器经常是在主要用于封装内部集合或数组的类型中实现的。  例如，假定具有一个名为 TempRecord 的类，此类表示在 24 小时内的 10 个不同时间记录的华氏度。  此类包含一个表示温度的 float 类型的名为“temps”的数组和表示记录温度的日期的 <xref:System.DateTime>。  通过在此类中实现一个索引器，客户端可以通过 `float temp = tr[4]` 而不是 `float temp = tr.temps[4]` 语法访问 TempRecord 实例中的温度。  索引器表示法不仅简化了客户端应用程序的语法，还使其他开发人员能够更加直观地理解类及其用途。  
  
 要声明类或结构上的索引器，请使用 [this](../../../csharp/language-reference/keywords/this.md) 关键字，如下例所示：  
  
```  
public int this[int index]    // Indexer declaration  
{  
    // get and set accessors  
}  
  
```  
  
## 备注  
 索引器类型及其参数类型必须至少如同索引器本身一样是可访问的。  有关可访问级别的更多信息，请参见[访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)。  
  
 有关如何对接口使用索引器的更多信息，请参见[接口索引器](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)。  
  
 索引器的签名由其形参的数量和类型组成。  它不包括索引器类型或形参名。  如果在同一类中声明一个以上的索引器，则它们必须具有不同的签名。  
  
 索引器值不属于变量；因此，不能将索引器值作为 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数进行传递。  
  
 要为索引器提供一个其他语言可以使用的名字，请使用声明中的 `name` 特性。  例如：  
  
```  
[System.Runtime.CompilerServices.IndexerName("TheItem")]  
public int this [int index]   // Indexer declaration  
{  
}  
```  
  
 此索引器将具有名称 `TheItem`。  不提供名称特性将生成 `Item` 默认名称。  
  
## 示例 1  
  
### 说明  
 下面的示例说明如何声明私有数组字段、`temps` 和索引器。  使用索引器可直接访问实例 `tempRecord[i]`。  另一种使用索引器的方法是将数组声明为 [public](../../../csharp/language-reference/keywords/public.md) 成员并直接访问它的成员 `tempRecord.temps[i]`。  
  
 请注意，当计算索引器的访问时（例如，在 `Console.Write` 语句中），将调用 [get](../../../csharp/language-reference/keywords/get.md) 访问器。  因此，如果 `get` 访问器不存在，将发生编译时错误。  
  
### 代码  
 [!code-cs[csProgGuideIndexers#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-indexers_1.cs)]  
  
## 使用其他值进行索引  
 C\# 并不将索引类型限制为整数。  例如，对索引器使用字符串可能是有用的。  通过搜索集合内的字符串并返回相应的值，可以实现此类索引器。  由于访问器可被重载，字符串和整数版本可以共存。  
  
## 示例 2  
  
### 说明  
 在此例中，声明了存储星期几的类。  声明了一个 `get` 访问器，它接受字符串（天名称），并返回相应的整数。  例如，星期日将返回 0，星期一将返回 1，等等。  
  
### 代码  
 [!code-cs[csProgGuideIndexers#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-indexers_2.cs)]  
  
## 可靠编程  
 提高索引器的安全性和可靠性有两种主要的方法：  
  
-   确保结合某一类型的错误处理策略，以处理万一客户端代码传入无效索引值的情况。  在本主题前面的第一个示例中，TempRecord 类提供了 Length 属性，使客户端代码能够在将输入传递给索引器之前对其进行验证。  也可以将错误处理代码放入索引器自身内部。  确保为用户记录在索引器的访问器中引发的任何异常。  
  
-   应当为 `get` 和 [set](../../../csharp/language-reference/keywords/set.md) 访问器的可访问性设置尽可能多的限制。  这一点对 `set` 访问器尤为重要。  有关更多信息，请参见 [限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)