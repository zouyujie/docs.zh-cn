---
title: "无法读取分隔字段，因为当 EscapeQuotes 设置为 True 时，双引号不是合法的分隔符 | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_IllegalDelimiter"
ms.assetid: ab8a0c3a-b89c-4617-9e31-7e81f5dca433
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 无法读取分隔字段，因为当 EscapeQuotes 设置为 True 时，双引号不是合法的分隔符
`TextFieldParser` 无法从文件中读取，因为引号 \("\) 以分隔符形式提供，且 `EscapeQuotes` 设置为 `True`。  
  
### 更正此错误  
  
-   将 `EscapeQuotes` 设置为 `False`。  
  
## 请参阅  
 [TextFieldParser.SetDelimiters 方法](http://msdn.microsoft.com/zh-cn/21fa40ec-5866-4d0e-9fd9-c708a190dcc9)   
 [TextFieldParser.Delimiters 属性](http://msdn.microsoft.com/zh-cn/4eb18f4d-3011-40a9-b668-be93eed0444f)   
 [如何：读取逗号分隔的文本文件](../Topic/How%20to:%20Read%20From%20Comma-Delimited%20Text%20Files%20in%20Visual%20Basic.md)   
 [TextFieldParser 对象](../../visual-basic/language-reference/objects/textfieldparser-object.md)