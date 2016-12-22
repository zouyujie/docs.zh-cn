---
title: "string（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "string"
  - "string_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "strings [C#], 参考"
  - "@ 字符串文本"
  - "字符串文本 [C#]"
  - "string 关键字 [C#]"
ms.assetid: 3037e558-fb22-494d-bca1-a15ade11b11a
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# string（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`string` 类型表示一个字符序列（零个或更多 Unicode 字符）。  `string` 是 .NET Framework 中 <xref:System.String> 的别名。  
  
 尽管 `string` 是引用类型，但定义相等运算符（`==` 和 `!=`）是为了比较 `string` 对象（而不是引用）的值。  这使得对字符串相等性的测试更为直观。  例如：  
  
```c#  
  
      string a = "hello";  
string b = "h";  
// Append to contents of 'b'  
b += "ello";  
Console.WriteLine(a == b);  
Console.WriteLine((object)a == (object)b);  
```  
  
 这将先显示“True”，然后显示“False”，因为字符串的内容是相同的，但是 `a` 和 `b` 引用的不是同一个字符串实例。  
  
 \+ 运算符用于连接字符串：  
  
```c#  
  
string a = "good " + "morning";  
```  
  
 这将创建一个包含“good morning”的字符串对象。  
  
 字符串是不可变的，即：字符串对象在创建后，尽管从语法上看您似乎可以更改其内容，但事实上并不可行。  例如，编写此代码时，编译器实际上会创建一个新字符串对象来保存新的字符序列，且新对象将赋给 b。  然后字符串“h”将适宜于垃圾回收。  
  
```c#  
  
      string b = "h";  
b += "ello";  
```  
  
 \[\] 运算符可以用于对 `string` 的各个字符的只读访问。  
  
```c#  
  
      string str = "test";  
char x = str[2];  // x = 's';  
```  
  
 字符串为 `string` 类型并可写成两种形式，即用引号引起来和用 @ 引起来。  用引号引起来的字符串括在双引号 \("\) 内：  
  
```c#  
"good morning"  // a string literal  
```  
  
 字符串文本可包含任何字符。  包括转义序列。  下面的示例使用转义序列 `\\` 来表示反斜杠，使用 `\u0066` 来表示字母 f，使用 `\n` 来表示换行符。  
  
```  
  
      string a = "\\\u0066\n";  
Console.WriteLine(a);  
```  
  
> [!NOTE]
>  转义码 `\u``dddd`（其中 `dddd` 是一个四位数）表示 Unicode 字符 U\+`dddd`。  此外还识别 8 位 Unicode 转义码： `\Udddddddd`。  
  
 原义字符串以 @ 开头并且也用双引号引起来。  例如：  
  
```c#  
@"good morning"  // a string literal  
```  
  
 原义字符串的优势在于*不* 处理转义序列，因此很容易写入，例如完全限定的文件名就是原义字符串：  
  
```c#  
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"  
```  
  
 若要在一个用 @ 引起来的字符串中包括一个双引号，请使用两对双引号：  
  
```c#  
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.  
```  
  
 @ 符号的另一种用法是使用作为 C\# 关键字的被引用的 \([\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)\) 标识符。  
  
 有关 C\# 中字符串的更多信息，请参见[字符串](../../../csharp/programming-guide/strings/index.md)。  
  
## 示例  
 [!code-cs[csrefKeywordsTypes#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/string_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [针对使用字符串的最佳做法](../Topic/Best%20Practices%20for%20Using%20Strings%20in%20the%20.NET%20Framework.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [基本字符串操作](../Topic/Basic%20String%20Operations%20in%20the%20.NET%20Framework.md)   
 [创建新字符串](../Topic/Creating%20New%20Strings%20in%20the%20.NET%20Framework.md)   
 [设置数值结果表的格式](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)