---
title: "设置数值结果表的格式（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "格式设置 [C#]"
  - "数值格式 [C#]"
  - "String.Format 方法"
  - "Console.Write 方法"
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 设置数值结果表的格式（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

通过使用 <xref:System.String.Format%2A?displayProperty=fullName> 方法，或者通过 <xref:System.Console.Write%2A?displayProperty=fullName> 或 <xref:System.Console.WriteLine%2A?displayProperty=fullName> 方法（这两个方法会调用 `String.Format`），可以设置数值结果的格式。  通过使用格式字符串指定格式。  下表包含受支持的标准格式字符串。  格式字符串采用以下形式：`Axx`，其中 `A` 是格式说明符，`xx` 是精度说明符。  格式说明符控制应用于数值的格式类型，而精度说明符则控制格式化输出的有效位数或小数位数。  精度说明符的值介于 0 到 99。  
  
 有关标准和自定义格式字符串的更多信息，请参见 [格式化类型](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)。  有关 `String.Format` 方法的更多信息，请参见 <xref:System.String.Format%2A?displayProperty=fullName>。  
  
|格式说明符|描述|示例|Output|  
|-----------|--------|--------|------------|  
|C 或 c|货币|Console.Write\("{0:C}", 2.5\);<br /><br /> Console.Write\("{0:C}", \-2.5\);|$2.50<br /><br /> \($2.50\)|  
|D 或 d|Decimal|Console.Write\("{0:D5}", 25\);|00025|  
|E 或 e|科学型|Console.Write\("{0:E}", 250000\);|2.500000E\+005|  
|F 或 f|定点|Console.Write\("{0:F2}", 25\);<br /><br /> Console.Write\("{0:F0}", 25\);|25.00<br /><br /> 25|  
|G 或 g|常规|Console.Write\("{0:G}", 2.5\);|2.5|  
|N 或 n|数字|Console.Write\("{0:N}", 2500000\);|2,500,000.00|  
|X 或 x|十六进制|Console.Write\("{0:X}", 250\);<br /><br /> Console.Write\("{0:X}", 0xffff\);|FA<br /><br /> FFFF|  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [标准数字格式字符串](../Topic/Standard%20Numeric%20Format%20Strings.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [string](../../../csharp/language-reference/keywords/string.md)