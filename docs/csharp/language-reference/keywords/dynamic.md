---
title: "dynamic（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "dynamic_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "dynamic [C#]"
  - "dynamic 关键字 [C#]"
ms.assetid: 9e797102-cc83-4964-bf58-afe4f54d16bc
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# dynamic（C# 参考）
在通过 `dynamic` 类型实现的操作中，该类型的作用是绕过编译时类型检查，  改为在运行时解析这些操作。  `dynamic` 类型简化了对 COM API（例如 Office Automation API）、动态 API（例如 IronPython 库）和 HTML 文档对象模型 \(DOM\) 的访问。  
  
 在大多数情况下，`dynamic` 类型与 `object` 类型的行为是一样的。  但是，不会用编译器对包含 `dynamic` 类型表达式的操作进行解析或类型检查。  编译器将有关该操作信息打包在一起，并且该信息以后用于计算运行时操作。  在此过程中，类型 `dynamic` 的变量会编译到类型 `object` 的变量中。  因此，类型 `dynamic` 只在编译时存在，在运行时则不存在。  
  
 以下示例将类型为 `dynamic` 的变量与类型为 `object` 的变量对比。  若要在编译时验证每个变量的类型，请将鼠标指针放在 `WriteLine` 语句中的 `dyn` 或 `obj` 上。  IntelliSense 显示了 `dyn` 的**“动态”**和 `obj` 的**“对象”**。  
  
 [!code-cs[csrefKeywordsTypes#21](../../../csharp/language-reference/keywords/codesnippet/csharp/dynamic_1.cs)]  
  
 `WriteLine` 语句显示 `dyn` 和 `obj` 的运行时类型。  此时，两者具有相同的整数类型。  将生成以下输出：  
  
 `System.Int32`  
  
 `System.Int32`  
  
 若要查看 `dyn` 和 `obj` 之间的差异，请在前面示例的声明和 `WriteLine` 语句之间添加下列两行之间。  
  
```c#  
dyn = dyn + 3;  
obj = obj + 3;  
  
```  
  
 为尝试添加表达式 `obj + 3` 中的整数和对象报告编译器错误。  但是，不会报告 `dyn + 3` 错误。  编译时不会检查包含 `dyn` 的表达式，原因是 `dyn` 的类型为 `dynamic`。  
  
## 上下文  
 `dynamic` 关键字可以直接出现或作为构造类型的组件在下列情况中出现：  
  
-   在声明中，作为属性、字段、索引器、参数、返回值或类型约束的类型。  下面的类定义在几个不同的声明中使用 `dynamic`。  
  
     [!code-cs[csrefKeywordsTypes#22](../../../csharp/language-reference/keywords/codesnippet/csharp/dynamic_2.cs)]  
  
-   在显式类型转换中，作为转换的目标类型。  
  
     [!code-cs[csrefKeywordsTypes#23](../../../csharp/language-reference/keywords/codesnippet/csharp/dynamic_3.cs)]  
  
-   在以类型充当值（如 `is` 运算符或 `as` 运算符右侧）或者作为 `typeof` 的参数成为构造类型的一部分的任何上下文中。  例如，可以在下列表达式中使用 `dynamic`。  
  
     [!code-cs[csrefKeywordsTypes#24](../../../csharp/language-reference/keywords/codesnippet/csharp/dynamic_4.cs)]  
  
## 示例  
 下面的示例以多个声明使用 `dynamic`。  `Main` 也用运行时类型检查对比编译时类型检查。  
  
 [!code-cs[csrefKeywordsTypes#25](../../../csharp/language-reference/keywords/codesnippet/csharp/dynamic_5.cs)]  
  
 有关更多信息和示例，请参见[使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)。  
  
## 请参阅  
 <xref:System.Dynamic.ExpandoObject?displayProperty=fullName>   
 <xref:System.Dynamic.DynamicObject?displayProperty=fullName>   
 [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [对象](../../../csharp/language-reference/keywords/object.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [as](../../../csharp/language-reference/keywords/as.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [如何：使用 as 和 is 运算符安全地进行强制转换](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md)   
 [演练：创建和使用动态对象](../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)