---
title: "命名实参和可选实参（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "namedParameter_CSharpKeyword"
  - "cs_namedParameter"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "参数 [C#], 命名的"
  - "参数 [C#], 可选"
  - "命名参数和可选参数 [C#]"
  - "命名参数 [C#]"
  - "可选参数 [C#]"
  - "参数 [C#], 命名的"
  - "参数 [C#], 可选"
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
caps.latest.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 43
---
# 命名实参和可选实参（C# 编程指南）
[!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] 引入了命名实参和可选实参。  利用“命名实参”，您将能够为特定形参指定实参，方法是将实参与该形参的名称关联，而不是与形参在形参列表中的位置关联。  利用“可选实参”，您将能够为某些形参省略实参。  这两种技术都可与方法、索引器、构造函数和委托一起使用。  
  
 在使用命名实参和可选实参时，将按实参出现在实参列表（而不是形参列表）中的顺序计算这些实参。  
  
 命名形参和可选形参一起使用时，您将能够只为可选形参列表中的少数形参提供实参。  此功能大大方便了对 COM 接口（例如 Microsoft Office 自动化 API）的调用。  
  
## 命名实参  
 有了命名实参，您将不再需要记住或查找形参在所调用方法的形参列表中的顺序。  可以按形参名称指定每个实参的形参。  例如，可以采用标准方式调用计算身体质量指数 \(BMI\) 的函数，方法是依照该函数定义的顺序按位置发送体重和身高的实参。  
  
 `CalculateBMI(123, 64);`  
  
 如果不记得形参的顺序，但却知道其名称，您可以按任意顺序（先发送体重或先发送身高）发送实参。  
  
 `CalculateBMI(weight: 123, height: 64);`  
  
 `CalculateBMI(height: 64, weight: 123);`  
  
 命名实参还可以标识每个实参所表示的含义，从而改进代码的可读性。  
  
 命名实参可以放在位置实参后面，如此处所示。  
  
 `CalculateBMI(123, height: 64);`  
  
 但是，位置实参不能放在命名实参后面。  下面的语句会导致编译器错误。  
  
 `//CalculateBMI(weight: 123, 64);`  
  
## 示例  
 下面的代码实现本节中的示例。  
  
 [!code-cs[csProgGuideNamedAndOptional#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/namedandoptionalsnippets/program.cs#1)]  
  
## 可选参数  
 方法、构造函数、索引器或委托的定义可以指定其形参为必需还是可选。  任何调用都必须为所有必需的形参提供实参，但可以为可选的形参省略实参。  
  
 每个可选形参都具有默认值作为其定义的一部分。  如果没有为该形参发送实参，则使用默认值。  默认值必须是一个表达式的以下类型之一:  
  
-   常数表达式;  
  
-   窗体 `new ValType()`的表达式， `ValType` 是值类型，例如 [枚举](../../../csharp/language-reference/keywords/enum.md) 或 [结构](../../../csharp/programming-guide/classes-and-structs/structs.md);  
  
-   窗体 [默认 \(ValType\)](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md)的表达式， `ValType` 是值类型。  
  
 可选形参在形参列表的末尾定义，位于任何必需的形参之后。  如果调用方为一系列可选形参中的任意一个形参提供了实参，则它必须为前面的所有可选形参提供实参。  实参列表中不支持使用逗号分隔的间隔。  例如，在以下代码中，使用一个必选形参和两个可选形参定义实例方法 `ExampleMethod`。  
  
 [!code-cs[csProgGuideNamedAndOptional#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/namedandoptionalsnippets/optional.cs#15)]  
  
 下面对 `ExampleMethod` 的调用导致编译器错误，原因是为第三个形参而不是为第二个形参提供了实参。  
  
 `//anExample.ExampleMethod(3, ,4);`  
  
 但是，如果您知道第三个形参的名称，则可以使用命名实参来完成任务。  
  
 `anExample.ExampleMethod(3, optionalint: 4);`  
  
 IntelliSense 使用括号指示可选形参，如下图所示。  
  
 ![ExampleMethod 方法的 IntelliSense 快速信息。](../../../csharp/programming-guide/classes-and-structs/media/optional-parameters.png "Optional\_Parameters")  
ExampleMethod 中的可选形参  
  
> [!NOTE]
>  还可以通过使用 .NET <xref:System.Runtime.InteropServices.OptionalAttribute> 类来声明可选形参。  `OptionalAttribute` 形参不需要默认值。  
  
## 示例  
 在下面的示例中，`ExampleClass` 的构造函数具有一个形参，该形参是可选的。  实例方法 `ExampleMethod` 具有一个必需的形参：`required`，以及两个可选形参：`optionalstr` 和 `optionalint`。  `Main` 中的代码演示了可用于调用构造函数和方法的不同方式。  
  
 [!code-cs[csProgGuideNamedAndOptional#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/namedandoptionalsnippets/optional.cs#2)]  
  
## COM 接口  
 命名实参和可选实参，以及对动态对象的支持和其他增强功能大大提高了与 COM API（例如 Office 自动化 API）的互操作性。  
  
 例如，Microsoft Office Excel 的 [Range](http://go.microsoft.com/fwlink/?LinkId=148196) 接口中的 [AutoFormat](http://go.microsoft.com/fwlink/?LinkId=148201) 方法具有七个形参，这七个形参都是可选的。  这些形参如下图所示。  
  
 ![AutoFormat 方法的 IntelliSense 快速信息。](../../../csharp/programming-guide/classes-and-structs/media/autoformat-parameters.png "AutoFormat\_Parameters")  
AutoFormat 形参  
  
 在 C\# 3.0 和早期版本中，每个形参都需要一个实参，如以下示例所示。  
  
 [!code-cs[csProgGuideNamedAndOptional#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/namedandoptionalsnippets/namedandoptcom.cs#3)]  
  
 但是，可以通过使用 C\# 4.0 中引入的命名实参和可选实参来大大简化对 `AutoFormat` 的调用。  如果不希望更改形参的默认值，则可以通过使用命名实参和可选实参来为可选形参省略实参。  在下面的调用中，仅为七个形参中的其中一个指定了值。  
  
 [!code-cs[csProgGuideNamedAndOptional#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/namedandoptionalsnippets/namedandoptcom.cs#13)]  
  
 有关更多信息和示例，请参见[如何：在 Office 编程中使用命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)和[如何：通过使用 Visual C\# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)。  
  
## 重载决策  
 使用命名实参和可选实参将在以下方面对重载决策产生影响：  
  
-   如果方法、索引器或构造函数的各个形参均为可选，或者按名称或位置与调用语句中的单个实参对应，并且该实参可转换为形参的类型，则该方法、索引器或构造函数是执行的候选项。  
  
-   如果找到多个候选项，则会将首选转换的重载决策规则应用于显式指定的实参。  将忽略可选形参已省略的实参。  
  
-   如果两个候选项不相上下，则会将没有可选形参的候选项作为首选项，对于这些可选形参，已在调用中为其省略了实参。  这是具有较少形参的候选项的重载决策中一般首选项的结果。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [如何：在 Office 编程中使用命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)   
 [使用索引器](../../../csharp/programming-guide/indexers/using-indexers.md)