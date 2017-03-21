---
title: "装箱和取消装箱（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.boxing"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 装箱"
  - "C# 语言, 取消装箱"
  - "取消装箱 [C#]"
  - "装箱 [C#]"
ms.assetid: 8da9bbf4-bce9-4b08-b2e5-f64c11c56514
caps.latest.revision: 34
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 34
---
# 装箱和取消装箱（C# 编程指南）
装箱是将[值类型](../../../csharp/language-reference/keywords/value-types.md)转换为 `object` 类型或由此值类型实现的任何接口类型的过程。  当 CLR 对值类型进行装箱时，会将该值包装到 System.Object 内部，再将后者存储在托管堆上。  取消装箱将从对象中提取值类型。  装箱是隐式的；取消装箱是显式的。  装箱和取消装箱的概念是类型系统 C\# 统一视图的基础，其中任一类型的值都被视为一个对象。  
  
 在下面的示例中，将整型变量 `i` 进行了装箱并分配给对象 `o`。  
  
 [!code-cs[csProgGuideTypes#14](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_1.cs)]  
  
 然后，可以将对象 `o`  取消装箱并分配给整型变量 `i`：  
  
 [!code-cs[csProgGuideTypes#15](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_2.cs)]  
  
 以下示例演示如何在 C\# 中使用装箱。  
  
 [!code-cs[csProgGuideTypes#47](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_3.cs)]  
  
## 性能  
 相对于简单的赋值而言，装箱和取消装箱过程需要进行大量的计算。  对值类型进行装箱时，必须分配并构造一个新对象。  取消装箱所需的强制转换也需要进行大量的计算，只是程度较轻。  有关更多信息，请参见[性能](../Topic/.NET%20Performance%20Tips.md)。  
  
## 装箱  
 装箱用于在垃圾回收堆中存储值类型。  装箱是[值类型](../../../csharp/language-reference/keywords/value-types.md)到 `object` 类型或到此值类型所实现的任何接口类型的隐式转换。  对值类型装箱会在堆中分配一个对象实例，并将该值复制到新的对象中。  
  
 请看以下值类型变量的声明：  
  
 [!code-cs[csProgGuideTypes#17](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_4.cs)]  
  
 以下语句对变量 `i` 隐式应用了装箱操作：  
  
 [!code-cs[csProgGuideTypes#18](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_5.cs)]  
  
 此语句的结果是在堆栈上创建对象引用 `o`，而在堆上则引用 `int` 类型的值。  该值是赋给变量 `i` 的值类型值的一个副本。  下图说明了两个变量 `i` 和 `o` 之间的差异。  
  
 ![BoxingConversion 图](../../../csharp/programming-guide/types/media/vcboxingconversion.gif "vcBoxingConversion")  
装箱转换  
  
 还可以像下面的示例一样执行显式装箱，但显式装箱从来不是必需的：  
  
 [!code-cs[csProgGuideTypes#19](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_6.cs)]  
  
## 说明  
 此示例使用装箱将整型变量 `i` 转换为对象 `o`。  这样一来，存储在变量 `i` 中的值就从 `123` 更改为 `456`。  该示例表明原始值类型和装箱的对象使用不同的内存位置，因此能够存储不同的值。  
  
## 示例  
 [!code-cs[csProgGuideTypes#16](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_7.cs)]  
  
## 取消装箱  
 取消装箱是从 `object` 类型到[值类型](../../../csharp/language-reference/keywords/value-types.md)或从接口类型到实现该接口的值类型的显式转换。  取消装箱操作包括：  
  
-   检查对象实例，以确保它是给定值类型的装箱值。  
  
-   将该值从实例复制到值类型变量中。  
  
 下面的语句演示装箱和取消装箱两种操作：  
  
 [!code-cs[csProgGuideTypes#21](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_8.cs)]  
  
 下图演示上述语句的结果。  
  
 ![图：取消装箱转换](../../../csharp/programming-guide/types/media/vcunboxingconversion.gif "vcUnBoxingConversion")  
取消装箱转换  
  
 要在运行时成功取消装箱值类型，被取消装箱的项必须是对一个对象的引用，该对象是先前通过装箱该值类型的实例创建的。  尝试取消装箱 `null` 会导致 <xref:System.NullReferenceException>。  尝试取消装箱对不兼容值类型的引用会导致 <xref:System.InvalidCastException>。  
  
## 示例  
 下面的示例演示无效的取消装箱及引发的 `InvalidCastException`。  使用 `try` 和 `catch`，在发生错误时显示错误信息。  
  
 [!code-cs[csProgGuideTypes#20](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_9.cs)]  
  
 此程序输出：  
  
 `Specified cast is not valid.  Error: Incorrect unboxing.`  
  
 如果将下列语句：  
  
```  
int j = (short) o;  
```  
  
 更改为：  
  
```  
int j = (int) o;  
```  
  
 将执行转换，并将得到以下输出：  
  
 `Unboxing OK.`  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 相关章节  
 更多相关信息：  
  
-   [引用类型](../../../csharp/language-reference/keywords/reference-types.md)  
  
-   [值类型](../../../csharp/language-reference/keywords/value-types.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)