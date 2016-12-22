---
title: "如果将 EscapeQuote 设置为 True，则双引号不是分隔字段的有效注释标记 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_InvalidComment"
dev_langs: 
  - "VB"
ms.assetid: 636d4b81-00ba-4cfd-98f7-4d57036f494d
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如果将 EscapeQuote 设置为 True，则双引号不是分隔字段的有效注释标记
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

已提供了一个引号作为 `TextFieldParser` 的分隔符，但 `EscapeQuotes` 已设置为 `True`。  
  
### 更正此错误  
  
-   将 `EscapeQuotes` 设置为 `False`。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.SetDelimiters%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.Delimiters%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser>   
 [如何：读取逗号分隔的文本文件](../Topic/How%20to:%20Read%20From%20Comma-Delimited%20Text%20Files%20in%20Visual%20Basic.md)