---
title: "字符串（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 字符串"
  - "字符串 [C#]"
ms.assetid: 21580405-cb25-4541-89d5-037846a38b07
caps.latest.revision: 41
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 41
---
# 字符串（C# 编程指南）
字符串是 <xref:System.String> 类型的对象，它的值是文本。  在内部，文本被存储为 <xref:System.Char> 对象的顺序只读集合。  C\# 字符串末尾没有以 null 结尾的字符；因此 C\# 字符串可以包含任意数目的嵌入式 null 字符（“\\0”）。  字符串的 <xref:System.String.Length%2A> 属性代表它包含的 `Char` 对象的数量，而不是 Unicode 字符的数量。  若要访问字符串中的各个 Unicode 码位，请使用 <xref:System.Globalization.StringInfo> 对象。  
  
## 字符串与System.String  
 在 C\# 中，`string` 关键字是 <xref:System.String> 的别名。  因此，`String` 与 `string` 等效，您可以根据自己的喜好选择命名约定。  `String` 类提供了很多用于安全地创建、操作和比较字符串的方法。  此外，C\# 语言还重载某些运算符来简化常见的字符串操作。  有关关键字的更多信息，请参见[string](../../../csharp/language-reference/keywords/string.md)。  有关类型及其方法的更多信息，请参见 <xref:System.String>。  
  
## 声明和初始化字符串  
 可以通过各种方式来声明和初始化字符串，如下面的示例所示：  
  
 [!code-cs[csProgGuideStrings#1](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_1.cs)]  
  
 注意，除了在使用字符数组初始化字符串时以外，不要使用 [new](../../../csharp/language-reference/keywords/new-operator.md) 运算符创建字符串对象。  
  
 使用 <xref:System.String.Empty> 常量值初始化字符串可新建字符串长度为零的 <xref:System.String> 对象。  零长度字符串的字符串表示形式为 ""。  使用 <xref:System.String.Empty> 值（而不是 [null](../../../csharp/language-reference/keywords/null.md)）初始化字符串可以降低发生 <xref:System.NullReferenceException> 的可能性。  请在尝试访问字符串之前使用静态 <xref:System.String.IsNullOrEmpty%28System.String%29> 方法验证字符串的值。  
  
## 字符串对象的不可变性  
 字符串对象是不可变的：即它们创建之后就无法更改。  所有看似修改字符串的 <xref:System.String> 方法和 C\# 运算符实际上都以新字符串对象的形式返回结果。  在下面的示例中，当连接 `s1` 和 `s2` 的内容以形成一个字符串时，不会修改两个原始字符串。  `+=` 运算符会创建一个包含组合内容的新字符串。  这个新对象赋给变量 `s1`，而最初赋给 `s1` 的对象由于没有其他任何变量包含对它的引用而释放，用于垃圾回收。  
  
 [!code-cs[csProgGuideStrings#2](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_2.cs)]  
  
 由于“修改”字符串实际上是创建新字符串，因此创建对字符串的引用时必须谨慎。  如果创建了对字符串的引用，然后“修改”原始字符串，则该引用指向的仍是原始对象，而不是修改字符串时创建的新对象。  下面的代码说明了这种行为：  
  
 [!code-cs[csProgGuideStrings#25](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_3.cs)]  
  
 有关如何创建基于修改（例如搜索和替换原始字符串的操作）的新字符串的更多信息，请参见[如何：修改字符串内容](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)。  
  
## 正则字符串和原义字符串  
 如果必须嵌入 C\# 提供的转义符，则应使用正则字符串，如下面的示例所示：  
  
 [!code-cs[csProgGuideStrings#3](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_4.cs)]  
  
 如果字符串文本包含反斜杠字符（例如在文件路径中），为方便起见和提高可读性，应使用原义字符串。  由于原义字符串保留换行符作为字符串文本的一部分，因此可用于初始化多行字符串。  在原义字符串中嵌入引号时请使用双引号。  下面的示例演示原义字符串的一些常见用途：  
  
 [!code-cs[csProgGuideStrings#4](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_5.cs)]  
  
## 字符串转义序列  
  
|转义序列|字符名称|Unicode 编码|  
|----------|----------|----------------|  
|\\'|单引号|0x0027|  
|\\"|双引号|0x0022|  
|\\\\|反斜杠|0x005C|  
|\\0|Null|0x0000|  
|\\a|警报|0x0007|  
|\\b|Backspace|0x0008|  
|\\f|换页|0x000C|  
|\\n|换行|0x000A|  
|\\r|回车|0x000D|  
|\\t|水平制表符|0x0009|  
|\\U|代理项对的 Unicode 转义序列。|\\Unnnnnnnn|  
|\\u|Unicode 转义序列|\\u0041 \= "A"|  
|\\v|垂直制表符|0x000B|  
|\\x|Unicode 转义序列类似于“\\u”，只是长度可变。|\\x0041 \= "A"|  
  
> [!NOTE]
>  编译时，原义字符串转换为所有转义序列均保持不变的普通字符串。  因而，如果在调试器监视窗口中查看原义字符串，则看到的将是编译器添加的转义字符，而不是源代码中的原义版本。  例如，原义字符串 @"C:\\files.txt" 在监视窗口中将显示为 "C:\\\\files.txt"。  
  
## 格式字符串  
 格式字符串是内容可以在运行时动态确定的一种字符串。  采用以下方式创建格式字符串：使用静态 <xref:System.String.Format%2A> 方法并在大括号中嵌入占位符，这些占位符将在运行时替换为其他值。  下面的示例使用格式字符串输出循环中每个迭代的结果：  
  
 [!code-cs[csProgGuideStrings#26](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_6.cs)]  
  
 <xref:System.Console.WriteLine%2A> 方法的一个重载将格式字符串用作参数。  因此，可以只嵌入格式字符串，而无需显式调用该方法。  但若使用 <xref:System.Diagnostics.Trace.WriteLine%2A> 方法在 Visual Studio**“输出”**窗口中显示调试输出，则必须显式调用 <xref:System.String.Format%2A> 方法，因为 <xref:System.Diagnostics.Trace.WriteLine%2A> 只接受字符串，而不接受格式字符串。  有关格式字符串的更多信息，请参见[格式化类型](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)。  
  
## 子字符串  
 子字符串是包含在字符串中的任意字符序列。  使用 <xref:System.String.Substring%2A> 方法可以基于原始字符串的一部分创建新字符串。  可以使用 <xref:System.String.IndexOf%2A> 方法搜索子字符串的一个或多个匹配项。  使用 <xref:System.String.Replace%2A> 方法可将指定子字符串的所有匹配项替换为一个新字符串。  与 <xref:System.String.Substring%2A> 方法一样，<xref:System.String.Replace%2A> 实际上返回的也是新字符串，而不修改原始字符串。  有关更多信息，请参见[如何：使用字符串方法搜索字符串](../../../csharp/programming-guide/strings/how-to-search-strings-using-string-methods.md)和[如何：修改字符串内容](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)。  
  
 [!code-cs[csProgGuideStrings#7](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_7.cs)]  
  
## 访问各个字符  
 可以使用带索引值的数组表示法获取对各个字符的只读访问，如下面的示例所示：  
  
 [!code-cs[csProgGuideStrings#9](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_8.cs)]  
  
 如果 <xref:System.String> 方法不提供修改字符串中的各个字符所必须具有的功能，则您可以使用 <xref:System.Text.StringBuilder> 对象“就地”修改各个字符，然后使用 <xref:System.Text.StringBuilder> 方法创建一个新字符串来存储结果。  在下面的示例中，假设您必须以特定方式修改原始字符串，然后存储结果以备将来使用：  
  
 [!code-cs[csProgGuideStrings#8](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_9.cs)]  
  
## Null 字符串和空字符串  
 空字符串是不包含字符的 <xref:System.String?displayProperty=fullName> 对象的实例。  在各种编程方案中经常会使用空字符串表示空白文本字段。  可以对空字符串调用方法，因为它们是有效的 <xref:System.String?displayProperty=fullName> 对象。  空字符串可按如下方式初始化：  
  
```  
string s = String.Empty;  
```  
  
 相反，null 字符串并不引用 <xref:System.String?displayProperty=fullName> 对象的实例，任何对 null 字符串调用方法的尝试都会生成 <xref:System.NullReferenceException>。  但是，可以在串联和比较操作中将 null 字符串与其他字符串一起使用。  下面的示例阐释了引用 null 字符串导致引发异常的情形以及并不导致引发异常的情形：  
  
 [!code-cs[csProgGuideStrings#27](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_10.cs)]  
  
## 使用 StringBuilder 快速创建字符串  
 .NET 中的字符串操作已高度优化，大多数情况下不会显著影响性能。  但在某些应用场景中，例如在执行好几百甚至好几千次的紧凑循环中，字符串操作会影响性能。  <xref:System.Text.StringBuilder> 类创建了一个字符串缓冲区，用于在程序执行大量字符串操作时提供更好的性能。  <xref:System.Text.StringBuilder> 字符串还使您能够重新分配个别字符（内置字符串数据类型所不支持的字符）。  例如，此代码在不创建新字符串的情况下更改了一个字符串的内容：  
  
 [!code-cs[csProgGuideStrings#20](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_11.cs)]  
  
 在本示例中，<xref:System.Text.StringBuilder> 对象用于从一组数值类型中创建字符串：  
  
 [!code-cs[csProgGuideStrings#15](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_12.cs)]  
  
## 字符串、扩展方法和 LINQ  
 由于 <xref:System.String> 类型实现 <xref:System.Collections.Generic.IEnumerable%601>，因此可以对字符串使用 <xref:System.Linq.Enumerable> 类中定义的扩展方法。  对于 <xref:System.String> 类型，为了避免视觉上的混乱，从 IntelliSense 中排除了这些方法，但这些方法仍然可用。  此外，还可以对字符串使用 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询表达式。  有关更多信息，请参见 [LINQ and Strings](../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)。  
  
## 相关主题  
  
|主题|说明|  
|--------|--------|  
|[如何：修改字符串内容](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)|提供一个代码示例来演示如何修改字符串的内容。|  
|[如何：串联多个字符串](../../../csharp/programming-guide/strings/how-to-concatenate-multiple-strings.md)|阐释如何使用 `+` 运算符和 `Stringbuilder` 类在编译时和运行时将字符串联接在一起。|  
|[如何：比较字符串](../../../csharp/programming-guide/strings/how-to-compare-strings.md)|演示如何执行字符串的序号比较。|  
|[如何：使用 String.Split 分析字符串 ](../../../csharp/programming-guide/strings/how-to-parse-strings-using-string-split.md)|包含一个代码示例，该示例演示如何使用 `String.Split` 方法来分析字符串。|  
|[如何：使用字符串方法搜索字符串](../../../csharp/programming-guide/strings/how-to-search-strings-using-string-methods.md)|解释如何使用特定方法来搜索字符串。|  
|[如何：使用正则表达式搜索字符串](../../../csharp/programming-guide/strings/how-to-search-strings-using-regular-expressions.md)|解释如何使用正则表达式来搜索字符串。|  
|[如何：确定字符串是否表示数值](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)|演示如何安全地分析字符串以了解其是否具有有效数值。|  
|[如何：将字符串转换为 DateTime](../../../csharp/programming-guide/strings/how-to-convert-a-string-to-a-datetime.md)|演示如何将诸如“01\/24\/2008”这样的字符串转换为 <xref:System.DateTime?displayProperty=fullName> 对象。|  
|[基本字符串操作](../Topic/Basic%20String%20Operations%20in%20the%20.NET%20Framework.md)|提供一些指向主题的链接，这些主题使用 <xref:System.String?displayProperty=fullName> 和 <xref:System.Text.StringBuilder?displayProperty=fullName> 方法来执行基本字符串操作。|  
|[分析字符串](../Topic/Parsing%20Strings%20in%20the%20.NET%20Framework.md)|介绍如何将字符或空格插入到字符串中。|  
|[比较字符串](../Topic/Comparing%20Strings%20in%20the%20.NET%20Framework.md)|包含有关如何比较字符串的信息，并且提供使用 C\# 和 Visual Basic 编写的示例。|  
|[使用 StringBuilder 类](../Topic/Using%20the%20StringBuilder%20Class%20in%20the%20.NET%20Framework.md)|描述如何使用 <xref:System.Text.StringBuilder> 类创建和修改动态字符串对象。|  
|[LINQ and Strings](../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)|提供有关如何使用 LINQ 查询来执行各种字符串操作的信息。|  
|[C\# 编程指南](../../../csharp/programming-guide/index.md)|提供指向解释 C\# 中编程构造的主题的链接。|  
  
## 重要章节  
 [More About Variables](http://go.microsoft.com/fwlink/?LinkId=221230) 在 [Beginning Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)