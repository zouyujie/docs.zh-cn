---
title: "内插字符串（C# 和 Visual Basic 引用） | Microsoft Docs"
ms.date: "2017-02-03"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: 324f267e-1c61-431a-97ed-852c1530742d
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# 内插字符串（C# 和 Visual Basic 引用）
用于构造字符串。  内插字符串表达式类似于包含表达式的模板字符串。  内插字符串表达式通过将包含的表达式替换为表达式结果的 ToString 表示形式来创建字符串。  与[复合格式设置](../Topic/Composite%20Formatting.md)相比，内插字符串在参数方面更易于理解。  下面是内插字符串的示例：  
  
```c#  
Console.WriteLine($"Name = {name}, hours = {hours:hh}")  
```  
  
 内插字符串的结构如下所示：  
  
```  
$ " <text> { <interpolation-expression> <optional-comma-field-width> <optional-colon-format> } <text> ... } "  
```  
  
 可以在可使用字符串的任何位置使用内插字符串。  当运行程序会执行带内插字符串的代码时，此代码会通过计算内插表达式来计算新的字符串。  每次执行带内插字符串的代码时，都会发生此计算。  
  
 若要在内插字符串中包含大括号（“{”或“}”），请使用两个大括号，即“{{”或“}}”。  请参阅“隐式转换”部分以获取详细信息。  
  
## 隐式转换  
 内插字符串中的隐式类型转换如下：  
  
```c#  
var s = $"hello, {name}" System.IFormattable s = $"Hello, {name}" System.FormattableString s = $"Hello, {name}"  
  
```  
  
 第一个示例生成一个 `string` 值，其中计算了所有字符串内插值。  此为最终结果，并具有 string 类型。  出现的所有双大括号（“{{”和“}}”）都转换为单大括号。  
  
 第二个示例生成一个 <xref:System.IFormattable> 变量，此变量允许使用固定上下文转换字符串。  要使数值和数据格式在不同语言中正确无误，此操作非常有用。  出现的所有双大括号（“{{”和“}}”）仍保留为双大括号，直至将字符串设置为 ToString 格式。  包含的所有内插表达式都转换为 {0}、{1} 等等。  
  
```c#  
s.ToString(null, System.Globalization.CultureInfo.InvariantCulture);  
```  
  
 第三个示例生成一个 <xref:System.FormattableString>，它允许检查由插值计算产生的对象。  例如，检查对象及其呈现为字符串的方式可能有助于你在生成查询时防止注入攻击。  借助 <xref:System.FormattableString>，只需简单操作即可生成 InvariantCulture 和 CurrentCulture 字符串结果。  在设置格式之前，出现在所有双大括号（“{{”和“}}”）保留为双括号。  包含的所有内插表达式都转换为 {0}、{1} 等等。  
  
## 示例  
  
```c#  
$"Name = {name}, hours = {hours:hh}" var s = $"hello, {name}" System.IFormattable s = $"Hello, {name}" System.FormattableString s = $"Hello, {name}" $"{person.Name, 20} is {person.Age:D3} year {(p.Age == 1 ? "" : "s")} old."  
  
```  
  
 无需在包含的内插表达式中引用引号字符，因为内插字符串表达式以 $ 开始，而且编译器会将包含的内插表达式扫描为平衡文本，直至它发现逗号、冒号或右大括号。出于相同原因，最后一个示例使用括号来使条件表达式 \(`p.Age == 1 ? "" : "s"`\) 包含在其格式规范不以冒号开头的内插表达式中。在包含的内插表达式外部（但仍在内插字符串表达式之中），可按通常方式转义引号字符。  
  
## 语法  
  
```  
expression: interpolated-string-expression interpolated-string-expression: interpolated-string-start interpolations interpolated-string-end interpolations: single-interpolation single-interpolation interpolated-string-mid interpolations single-interpolation: interpolation-start interpolation-start : regular-string-literal interpolation-start: expression expression , expression  
  
```  
  
## 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
 有关更多信息，请参见 [Visual Basic 语言参考](../../../visual-basic/language-reference/index.md)。  
  
## 请参阅  
 <xref:System.IFormattable?displayProperty=fullName>   
 <xref:System.FormattableString?displayProperty=fullName>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [Visual Basic 语言参考](../../../visual-basic/language-reference/index.md)   
 [Visual Basic 编程指南](../../../visual-basic/programming-guide/index.md)