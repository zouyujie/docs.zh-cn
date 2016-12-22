---
title: "如何：在旧式编码与 Unicode 之间转换（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "转换 [C#], 从旧版转换为 Unicode 编码"
  - "字符串 [C#], 在不同编码之间进行转换"
ms.assetid: 4eed7d8e-47ab-4a7c-8b95-9645a0ef000b
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在旧式编码与 Unicode 之间转换（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 C\# 中，内存中的所有字符串都是按 Unicode \(UTF\-16\) 编码的。  将数据从存储器移动到 `string` 对象中后，数据将自动转换为 UTF\-16。  如果数据仅包含从 0 到 127 的 ASCII 值，则此转换无需您执行任何额外的工作。  但若源文本包含扩展的 ASCII 字节值（128 到 255），则默认情况下，将根据当前代码页解释扩展字符。  若要指定应该根据其他某个代码页解释源文本，请使用 <xref:System.Text.Encoding?displayProperty=fullName> 类，如下面的示例所示。  
  
## 示例  
 下面的示例演示如何转换按 8 位 ASCII 编码的文本文件，此转换根据 Windows 代码页 737 解释源文本。  
  
 [!code-cs[csProgGuideStrings#34](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-between-legacy-encodings-and-unicode_1.cs)]  
  
## 请参阅  
 [字符串](../../../csharp/programming-guide/strings/index.md)