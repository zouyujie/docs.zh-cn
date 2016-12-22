---
title: "从 0 开始与从 1 开始的字符串访问 (Visual Basic) | Microsoft Docs"
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
  - "字符串 [Visual Basic], 索引"
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 从 0 开始与从 1 开始的字符串访问 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

本主题比较 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 和 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 如何提供对字符串中的字符。  [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 根据函数始终提供对字符的从零开始的访问，字符串，而 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供从零开始和从一开始的访问，。  
  
## 从一开始  
 有关从一开始的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 函数的示例，请看 `Mid` 功能。  它采用从位置 1. 开始标记字符位置该子字符串开始，的参数。  [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.String.Substring%2A?displayProperty=fullName> 方法从位置 0 开始采用一个字符的索引将中子字符串开头的字符串为; 否则为。  因此，因此，如果您有一个字符串 “ABCDE”，各个字符编号 1,2,3,4,5 用于 `Mid` 使用函数，但是， 0,1,2,3,4 用于 <xref:System.String.Substring%2A?displayProperty=fullName> 方法。  
  
## 从零开始  
 有关从零开始的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 函数的示例，请看 `Split` 功能。  该函数拆分字符串并返回包含子字符串的数组。  [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.String.Split%2A?displayProperty=fullName> 方法也拆分字符串并返回包含子字符串的数组。  由于 `Split` 功能和 <xref:System.String.Split%2A> 方法返回 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 数组，它们必须是从零开始的。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:System.String.Substring%2A>   
 <xref:System.String.Split%2A>   
 [字符串介绍 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)