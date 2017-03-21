---
title: "使用转换运算符（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "转换运算符 [C#]"
  - "转换 [C#], 运算符"
  - "显式转换运算符 [C#]"
  - "隐式转换运算符 [C#]"
  - "运算符 [C#], 转换"
  - "用户定义的转换 [C#]"
ms.assetid: caf36e89-c6c0-4b87-9f9e-85780a45c9a4
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# 使用转换运算符（C# 编程指南）
您可以使用 `implicit` 转换运算符，这种方法更易于使用，或者使用`explicit` 转换运算符，这种方法能清楚地指示每个人阅读的代码，无论您转换为什么类型。  本主题演示转换运算符的两个类型。  
  
> [!NOTE]
>  有关简单类型转换的信息，请参见[如何：将字符串转换为数字](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)[如何：将字节数组转换为 int](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md)[如何：在十六进制字符串与数值类型之间转换](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)或<xref:System.Convert>。  
  
## 示例  
 这是显式转换运算符的一个示例。  此运算符将类型 <xref:System.Byte> 转换为称为 `Digit` 的值类型。  由于不是所有字节都可以转换为数字，因此转换是显式的，这意味着必须使用强制转换，如 `Main` 方法所示。  
  
 [!code-cs[csProgGuideStatements#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-conversion-operators_1.cs)]  
  
## 示例  
 此示例通过定义用来撤消前一个示例所执行的操作的转换运算符，来演示隐式转换运算符：它将名为 `Digit` 的值类转换为整数 <xref:System.Byte> 类型。  由于任何数字都可以转换为 <xref:System.Byte>，因此没有必要一定让用户知道进行的转换。  
  
 [!code-cs[csProgGuideStatements#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-conversion-operators_2.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [转换运算符](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)   
 [is](../../../csharp/language-reference/keywords/is.md)