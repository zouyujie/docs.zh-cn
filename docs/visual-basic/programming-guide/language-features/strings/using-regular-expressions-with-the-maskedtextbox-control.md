---
title: "在 MaskedTextBox 控件中使用正则表达式 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "字符串 [Visual Basic], 屏蔽编辑"
  - "字符串 [Visual Basic], 正则表达式"
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 在 MaskedTextBox 控件中使用正则表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

此示例演示如何转换简单的正则表达式，以便与 <xref:System.Windows.Forms.MaskedTextBox> 控件一起使用。  
  
## 掩码语言的说明  
 标准的 <xref:System.Windows.Forms.MaskedTextBox> 掩码语言基于 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 6.0 中的 `Masked Edit` 控件使用的掩码语言，从该平台迁移的用户应该熟悉这一语言。  
  
 <xref:System.Windows.Forms.MaskedTextBox> 控件的 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 属性指定要使用的输入掩码。  掩码必须是由下表中的一个或多个掩码元素组成的字符串。  
  
|掩码元素|说明|正则表达式元素|  
|----------|--------|-------------|  
|0|0 到 9 之间的任何一个数字。  必选项。|\\d|  
|9|数字或空格。  可选项。|\[ \\d\]?|  
|\#|数字或空格。  可选项。  如果此位置在掩码中保留为空，它将显示为空格。  允许使用加号 \(\+\) 和减号 \(\-\)。|\[ \\d\+\-\]?|  
|L|ASCII 字母。  必选项。|\[a\-zA\-Z\]|  
|?|ASCII 字母。  可选项。|\[a\-zA\-Z\]?|  
|&|字符。  必选项。|\[\\p{Ll}\\p{Lu}\\p{Lt}\\p{Lm}\\p{Lo}\]|  
|C|字符。  可选项。|\[\\p{Ll}\\p{Lu}\\p{Lt}\\p{Lm}\\p{Lo}\]?|  
|A|字母数字。  可选项。|\\W|  
|.|相应于区域性的小数点占位符。|不可用。|  
|,|相应于区域性的千分位占位符。|不可用。|  
|:|相应于区域性的时间分隔符。|不可用。|  
|\/|相应于区域性的日期分隔符。|不可用。|  
|$|相应于区域性的货币符号。|不可用。|  
|\<|将后续所有字符都转换为小写。|不可用。|  
|\>|将后面的所有字符转换为大写。|不可用。|  
|&#124;|停止前面的大写转换或小写转换。|不可用。|  
|\\|对掩码字符进行转义，将其转变为原义字符。"  “\\\\”是反斜杠的转义序列。|\\|  
|所有其他字符。|原义字符。  所有非掩码元素将在 <xref:System.Windows.Forms.MaskedTextBox> 中以原样显示。|所有其他字符。|  
  
 默认情况下，小数点 \(.\)、千分位 \(,\)、时间 \(:\)、日期 \(\/\) 和货币 \($\) 符号按应用程序的区域性定义显示。  可使用 <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A> 属性强制它们显示为其他区域性的符号。  
  
## 正则表达式和掩码  
 虽然正则表达式和掩码都可以用来验证用户输入，但它们并不完全相同。  与掩码相比，正则表达式可以表达更复杂的模式，但掩码可以更简洁地采用与区域相关的格式来表达相同的信息。  
  
 下表将四个正则表达式与它们的等效掩码进行比较。  
  
|正则表达式|掩码|注释|  
|-----------|--------|--------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|掩码中的 `/` 字符是逻辑日期分隔符，它按应用程序的当前区域性设置向用户显示相应的日期分隔符。|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|美国格式的日期（日, 月份缩写, 年），其中的 3 个字母为首字母大写、后两个字母小写的月份缩写形式。|  
|`(\(\d{3}\)-)?  \d{3}-d{4}`|`(999)-000-0000`|美国电话号码，区号为可选项。  如果用户不想输入可选字符，则可输入空格，也可以将鼠标指针直接放在掩码中由第一个 0 表示的位置。|  
|`$\d{6}.00`|`$999,999.00`|货币值的范围从 0 到 999999。  货币字符、千位字符和十进制字符在运行时会被替换为区域特定的等效内容。|  
  
## 请参阅  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>   
 <xref:System.Windows.Forms.MaskedTextBox>   
 [验证字符串 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)   
 [MaskedTextBox 控件](../Topic/MaskedTextBox%20Control%20\(Windows%20Forms\).md)