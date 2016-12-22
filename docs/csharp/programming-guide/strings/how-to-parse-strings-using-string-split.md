---
title: "如何：使用 String.Split 分析字符串（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "拆分字符串 [C#]"
  - "Split 方法 [C#]"
  - "字符串 [C#], 拆分"
  - "分析字符串"
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：使用 String.Split 分析字符串（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

以下代码示例说明如何使用 <xref:System.String.Split%2A?displayProperty=fullName> 方法分析字符串。 作为输入，<xref:System.String.Split%2A> 采用一个指示哪些字符分隔目标字符串的兴趣子字符串的字符数组。  函数返回子字符串数组。  
  
 此示例使用空格、逗号、句点、冒号和制表符，所有内容均在包含这些分隔字符的数组中传递到 <xref:System.String.Split%2A>。  目标字符串句子中每个单词均单独从所得字符串数组中显示。  
  
## 示例  
 [!code-cs[csProgGuideStrings#16](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-parse-strings-using-string-split_1.cs)]  
  
## 示例  
 默认情况下，当两个分隔字符连续出现在目标字符串时 String.Split 返回空字符串。  你可以传递可选 StringSplitOptions.RemoveEmptyEntries 参数来排除输出中的任何空字符串。  
  
 String.Split 可采用字符串数组（充当用于分析目标字符串的分隔符的字符序列，而非单个字符）。  
  
```c#  
class TestStringSplit { static void Main() { char[] separatingChars = { "<<", "..." }; string text = "one<<two......three<four"; System.Console.WriteLine("Original text: '{0}'", text); string[] words = text.Split(separatingChars, System.StringSplitOptions.RemoveEmptyEntries ); System.Console.WriteLine("{0} substrings in text:", words.Length); foreach (string s in words) { System.Console.WriteLine(s); } // Keep the console window open in debug mode. System.Console.WriteLine("Press any key to exit."); System.Console.ReadKey(); } } /* Output: Original text: 'one<<two......three<four' 3 words in text: one two three<four */  
  
```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [.NET Framework 正则表达式](../Topic/.NET%20Framework%20Regular%20Expressions.md)