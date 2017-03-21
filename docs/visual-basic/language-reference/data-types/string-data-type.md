---
title: "String 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.String"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "" String 文本"
  - "$ 标识符类型字符"
  - "数据类型 [Visual Basic], 分配"
  - "定长字符串"
  - "定长字符串, 字符串数据类型"
  - "标识符类型字符串, $"
  - "文本, string"
  - "String 数据类型"
  - "string 关键字 [Visual Basic]"
  - "字符串"
  - "字符串 [Visual Basic], 字符"
  - "字符串 [Visual Basic], 固定长度"
  - "文本 [Visual Basic], String 数据类型"
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# String 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存无符号 16 位 \(2 字节\) 代码序列点该范围按从 0 到 65535 的值。  每个 *码位*，或者字符代码，表示单个 Unicode 字符。  字符串可以包含从 0 到大约两个对数字 2 \(^\) 31 个 Unicode 字符。  
  
## 备注  
 使用 `String` 数据类型保存多个字符，而无需数组管理开销 `Char()`，数组 `Char` 元素。  
  
 `String` 的默认值为 `Nothing` \(空引用\)。  请注意这与为空字符串 \(值 `""`\)。  
  
## Unicode 字符  
 码位的前 128 \(0\-127\) Unicode 对应于字母和符号在标准美国。  键盘。  码位的这些前 128 相同的与 ASCII 字符集定义。  码位的第二个 128 \(128\-255\) 表示特殊字符，比如基于拉丁语字母表的字母、重音、、货币符号和部分。  使用 Unicode 其余的代码对各种符号点 \(256\-65535\)。  这包括成功率文本字符、差异和数学和技术符号。  
  
 在 `String` 变量可以使用之类的方法 <xref:System.Char.IsDigit%2A> 和 <xref:System.Char.IsPunctuation%2A> 在单个字符确定其 Unicode 类别。  
  
## 布局要求  
 您必须括在引号 \(`" "`\) 中的一个 `String` 文本。  如果必须包括引号作为参数之一个字符在字符串，则使用两个连续引号 \(`""`\)。  下面的示例阐释了这一点。  
  
```  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 请注意个表示字符串中的一个引号的连续引号都是开始和结束 `String` 文本引号无关。  
  
## 字符串操作  
 一旦将字符串到 `String` 变量，该字符串是不可变 *的*，这意味着不能更改其长度或目录。  当通过任何方式时修改一个字符串， Visual Basic 创建一个新字符串并丢弃上一个。  `String` 变量并指向新字符串。  
  
 可以使用多种字符串功能，可以操作 `String` 变量的内容。  下面的示例演示 <xref:Microsoft.VisualBasic.Strings.Left%2A> 功能  
  
```  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 另一个组件创建的字符串可能填充前导或尾随空格。  如果收到这种字符串，可以使用 <xref:Microsoft.VisualBasic.Strings.Trim%2A>、 <xref:Microsoft.VisualBasic.Strings.LTrim%2A>和 <xref:Microsoft.VisualBasic.Strings.RTrim%2A> 功能来撤消这些空间。  
  
 有关字符串操作的更多信息，请 [字符串](../../../visual-basic/programming-guide/language-features/strings/index.md)参见。  
  
## 编程提示  
  
-   **负数。** 确保 `String` 保存的字符未签名，不能表示负值。  在任一情况下，您不应使用 `String` 表示数值。  
  
-   **互操作注意事项。** 如果您针对使用 .NET framework 编写的组件，例如自动或 COM 对象，请确保字符串的字符具有不同的数据宽度 \(8 位\) 在其他环境。  如果将 8 位字符的字符串参数传递给此类元素，则将其声明为，则 `Byte()`，数组 `Byte` 元素，而不是在新的 Visual Basic 代码的 `String` 。  
  
-   **键入字符。** 追加该标识符键入对所有标识符的 `$` 强制到 `String` 数据类型的字符。  `String` 没有文本类型字符。  但是，编译器将括在引号内的文本 \(`" "`\) 作为 `String`。  
  
-   **结构类型。** 相应键入 .NET framework 是 <xref:System.String?displayProperty=fullName> 类。  
  
## 请参阅  
 <xref:System.String?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Char 数据类型](../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)