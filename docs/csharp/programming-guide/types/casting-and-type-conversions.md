---
title: "强制转换和类型转换（C# 编程指南） | Microsoft Docs"
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
  - "强制转换 [C#]"
  - "转换 [C#], 类型"
  - "转换类型 [C#]"
  - "数据类型转换 [C#]"
  - "数值转换 [C#]"
  - "类型转换 [C#]"
ms.assetid: 568df58a-d292-4b55-93ba-601578722878
caps.latest.revision: 52
caps.handback.revision: 52
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 强制转换和类型转换（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

由于 C\# 是在编译时静态类型化的，因此变量在声明后就无法再次声明，或者无法用于存储其他类型的值，除非该类型可以转换为变量的类型。  例如，不存在从整数到任意字符串的转换。  因此，将 `i` 声明为整数后，就无法将字符串“Hello”赋予它，如下面的代码中所示。  
  
```c#  
int i;  
i = "Hello"; // Error: "Cannot implicitly convert type 'string' to 'int'"  
```  
  
 但有时可能需要将值复制到其他类型的变量或方法参数中。  例如，您可能有一个整数变量，您需要将该变量传递给参数类型化为 `double` 的方法。  或者可能需要将类变量赋给接口类型的变量。  这些类型的操作称为“类型转换”。  在 C\# 中，可以执行以下几种类型的转换：  
  
-   **隐式转换**：由于该转换是一种安全类型的转换，不会导致数据丢失，因此不需要任何特殊的语法。  例如，从较小整数类型到较大整数类型的转换以及从派生类到基类的转换都是这样的转换。  
  
-   **显式转换（强制转换）**：显式转换需要强制转换运算符。  在转换中可能丢失信息时或在出于其他原因转换可能不成功时，必须进行强制转换。典型的例子包括从数值到精度较低或范围较小的类型的转换和从基类实例到派生类的转换。  
  
-   **用户定义的转换**：可以定义一些特殊的方法来执行用户定义的转换，从而使不具有基类–派生类关系的自定义类型之间可以显式和隐式转换。  有关更多信息，请参见 [转换运算符](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)。  
  
-   **使用帮助程序类的转换**：若要在不兼容的类型之间进行转换，例如在整数与 <xref:System.DateTime?displayProperty=fullName> 对象之间转换，或者在十六进制字符串与字节数组之间转换，则可以使用 <xref:System.BitConverter?displayProperty=fullName> 类、<xref:System.Convert?displayProperty=fullName> 类和内置数值类型的 `Parse` 方法，例如 <xref:System.Int32.Parse%2A?displayProperty=fullName>。  有关更多信息，请参见[如何：将字节数组转换为 int](../Topic/How%20to:%20Convert%20a%20byte%20Array%20to%20an%20int%20\(C%23%20Programming%20Guide\).md)、[如何：将字符串转换为数字](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)和[如何：在十六进制字符串与数值类型之间转换](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)。  
  
## 隐式转换  
 对于内置数值类型，如果要存储的值无需截断或四舍五入即可适应变量，则可以进行隐式转换。  例如，[long](../../../csharp/language-reference/keywords/long.md) 类型的变量（8 字节整数）能够存储 [int](../../../csharp/language-reference/keywords/int.md)（在 32 位计算机上为 4 字节）可存储的任何值。  在下面的示例中，编译器先将右侧的值隐式转换为 `long` 类型，再将它赋给 `bigNum`。  
  
 [!CODE [csProgGuideTypes#34](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#34)]  
  
 有关所有隐式数值转换的完整列表，请参见[隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
 对于引用类型，隐式转换始终存在于从一个类转换为该类的任何一个直接或间接的基类或接口的情况。  由于派生类始终包含基类的所有成员，因此不必使用任何特殊语法。  
  
```  
Derived d = new Derived();  
Base b = d; // Always OK.  
```  
  
## 显式转换  
 但是，如果进行转换可能会导致信息丢失，则编译器会要求执行显式转换，显式转换也称为“强制转换”。  强制转换是显式通知编译器您打算进行转换且您知道可能会发生数据丢失的一种方式。  若要执行强制转换，请在要转换的值或变量前面的圆括号中指定要强制转换到的类型。  下面的程序将 [double](../../../csharp/language-reference/keywords/double.md) 强制转换为 [int](../../../csharp/language-reference/keywords/int.md)。  如不强制转换则该程序不会进行编译。  
  
 [!CODE [csProgGuideTypes#2](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#2)]  
  
 有关支持的显式数值转换的列表，请参见[显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)。  
  
 对于引用类型，如果需要从基类型转换为派生类型，则必须进行显式强制转换：  
  
```c#  
// Create a new derived type.  
Giraffe g = new Giraffe();  
  
// Implicit conversion to base type is safe.  
Animal a = g;  
  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe) a;  
```  
  
 引用类型之间的强制转换操作不会更改基础对象的运行时类型；它只更改用作对该对象的引用的值的类型。  有关更多信息，请参见 [多态性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)。  
  
## 运行时的类型转换异常  
 在某些引用类型转换中，编译器无法确定强制转换是否会有效。  正确进行编译的强制转换操作有可能在运行时失败。  如下面的示例所示，类型强制转换在运行时失败将导致引发 <xref:System.InvalidCastException>。  
  
 [!CODE [csProgGuideTypes#41](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#41)]  
  
 C\# 提供 [is](../../../csharp/language-reference/keywords/is.md) 和 [as](../../../csharp/language-reference/keywords/as.md) 运算符，使您可以在实际执行强制转换之前测试兼容性。  有关更多信息，请参见 [如何：使用 as 和 is 运算符安全地进行强制转换](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 重要章节  
 [More About Variables](http://go.microsoft.com/fwlink/?LinkId=221230) 在 [Beginning Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类型](../../../csharp/programming-guide/types/index.md)   
 [\(\) 运算符](../../../csharp/language-reference/operators/invocation-operator.md)   
 [explicit](../../../csharp/language-reference/keywords/explicit.md)   
 [implicit](../../../csharp/language-reference/keywords/implicit.md)   
 [转换运算符](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)   
 [Generalized Type Conversion](../Topic/Generalized%20Type%20Conversion.md)   
 [Exported Type Conversion](http://msdn.microsoft.com/zh-cn/1dfe55f4-07a2-4b61-aabf-a8cf65783a6b)   
 [如何：将字符串转换为数字](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)