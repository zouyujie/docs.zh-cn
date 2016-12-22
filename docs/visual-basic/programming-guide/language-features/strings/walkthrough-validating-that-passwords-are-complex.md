---
title: "演练：验证密码是否复杂 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "String 数据类型, 验证"
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 演练：验证密码是否复杂 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

此方法将检查某些强密码特性，并使用有关检查密码失败的信息更新字符串参数。  
  
 可在安全的系统中使用密码来向用户授权。  但是，密码必须难于被未授权用户猜测出来。  攻击者可以使用一种“字典攻击”程序，该程序将遍历一本字典（或不同语言的多本字典）中的所有单词，并测试是否有任何单词就是用户的密码。  诸如“Yankees”或“Mustang”等弱密码可被很快猜测出来。  诸如“?You'L1N3vaFiNdMeyeP@sSWerd\!”等强密码被猜测出来的可能性要小很多。  密码保护系统应确保用户选择强密码。  
  
 强密码很复杂（包含大写、小写、数字和特殊字符的组合），并且不是单词。  此示例演示如何验证复杂性。  
  
## 示例  
  
### 代码  
 [!CODE [VbVbcnRegEx#1](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnRegEx#1)]  
  
## 编译代码  
 通过传递包含该密码的字符串来调用此方法。  
  
 此示例需要：  
  
-   对 <xref:System.Text.RegularExpressions> 命名空间中的成员的访问权限。  如果代码中的成员名称没有完全限定，则需要添加一条 `Imports` 语句。  有关更多信息，请参见 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
## 安全性  
 如果要在网络中转移密码，您需要使用安全的方法来传输数据。  有关更多信息，请参见 [ASP.NET Web Application Security](../Topic/ASP.NET%20Web%20Application%20Security.md)。  
  
 通过添加额外的复杂性检查，您可以改进 `ValidatePassword` 函数的准确性：  
  
-   依据用户的名称、用户标识符和应用程序定义的字典来比较密码及其子字符串。  此外，在执行比较时，将看起来类似的字符视为相同字符。  例如，将字母“l”和“e”视为与数字“1”和“3”相同的字符。  
  
-   如果只有一个大写字符，请确保它不是密码的第一个字符。  
  
-   确保密码的最后两个字符是字母字符。  
  
-   不允许这样的密码：其中的所有符号都是通过键盘最上面的一排键输入的。  
  
## 请参阅  
 <xref:System.Text.RegularExpressions.Regex>   
 [ASP.NET Web Application Security](../Topic/ASP.NET%20Web%20Application%20Security.md)