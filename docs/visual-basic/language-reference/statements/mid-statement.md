---
title: "Mid 语句 | Microsoft Docs"
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
  - "vb.MidB"
  - "vb.Mid"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Mid 语句"
  - "字符串 [Visual Basic], 替换"
  - "字符串 [Visual Basic], 子字符串"
  - "子字符串, Mid 语句"
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Mid 语句
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

用另一个字符串中的字符替换 `String` 变量中指定数量的字符。  
  
## 语法  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## 部件  
 `Target`  
 必选。  要修改的 `String` 变量的名称。  
  
 `Start`  
 必选。  `Integer` 表达式。  `Target` 的字符位置，即开始替换文本处。  `Start` 使用从一开始的索引。  
  
 `Length`  
 可选。  `Integer` 表达式。  要替换的字符数。  如果省略该参数，则使用所有 `String`。  
  
 `StringExpression`  
 必选。  替换部分 `Target` 的 `String` 表达式。  
  
## 异常  
  
|异常类型|Condition|  
|----------|---------------|  
|<xref:System.ArgumentException>|`Start` \<\= 0 或 `Length` \< 0。|  
  
## 备注  
 所替换的字符数总是小于或等于 `Target` 中的字符数。  
  
 Visual Basic 具有 <xref:Microsoft.VisualBasic.Strings.Mid%2A> 函数和 `Mid` 语句。  这些元素都对字符串中指定数量的字符进行操作，但 `Mid` 函数返回字符，而 `Mid` 语句替换字符。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.Strings.Mid%2A>。  
  
> [!NOTE]
>  Visual Basic 早期版本中的 `MidB` 语句替换字节形式（而不是字符形式）的子字符串。  它主要用于在双字节字符集 \(DBCS\) 应用程序中转换字符串。  所有 Visual Basic 字符串均采用 Unicode 的形式，不再支持 `MidB`。  
  
## 示例  
 本例使用 `Mid` 语句用一个字符串中的字符替换字符串变量中指定数量的字符。  
  
 [!code-vb[VbVbalrStrings#5](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/mid-statement_1.vb)]  
  
## 要求  
 **命名空间：** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **模块：** `Strings`  
  
 **程序集：** [!INCLUDE[vbprvbruntime](../../../visual-basic/language-reference/objects/includes/vbprvbruntime_md.md)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 [字符串](../../../visual-basic/reference/command-line-compiler/index.md)   
 [字符串介绍 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)