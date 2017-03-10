---
title: "如何：使用 as 和 is 运算符安全地进行强制转换（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "as 运算符 [C#]"
  - "强制转换运算符 [C#], as 和 is 运算符"
  - "is 运算符 [C#]"
ms.assetid: c1176cea-1426-4a44-8570-3eadafa58863
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# 如何：使用 as 和 is 运算符安全地进行强制转换（C# 编程指南）
由于对象是多态的，因此基类类型的变量可以保存派生类型。  若要访问派生类型的方法，需要将值强制转换回该派生类型。  不过，在这些情况下，如果只尝试进行简单的强制转换，会导致引发 <xref:System.InvalidCastException> 的风险。  这就是 C\# 提供 [is](../../../csharp/language-reference/keywords/is.md) 和 [as](../../../csharp/language-reference/keywords/as.md) 运算符的原因。  您可以使用这两个运算符来测试强制转换是否会成功，而没有引发异常的风险。  通常，`as` 运算符更高效一些，因为如果可以成功进行强制转换，它会实际返回强制转换值。  而 `is` 运算符只返回一个布尔值。  因此，如果只想确定对象的类型，而无需对它进行实际强制转换，则可以使用 is 运算符。  
  
## 示例  
 下面的示例演示如何使用 `is` 和 `as` 运算符从一个引用类型强制转换为另一个引用类型，而没有引发异常的风险。  此示例还演示如何对 `as` 运算符使用可以为 null 值的类型。  
  
 [!code-cs[csProgGuideTypes#40](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/how-to-safely-cast-by-us_1.cs)]  
  
## 请参阅  
 [类型](../../../csharp/programming-guide/types/index.md)   
 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)