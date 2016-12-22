---
title: "Option Compare 语句 | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Compare"
  - "vb.OptionCompare"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "二进制比较"
  - "二进制比较, Option Compare 语句"
  - "Binary 关键字, Option Compare 语句"
  - "区分大小写, Option Compare 语句"
  - "Compare 关键字"
  - "Option Compare 语句"
  - "字符串比较 [Visual Basic], Option Compare 语句"
  - "字符串比较 [Visual Basic], 对数据进行排序"
  - "字符串 [Visual Basic], 比较"
  - "字符串 [Visual Basic], 从函数中返回"
  - "文本 [Visual Basic], 比较"
  - "Text 关键字, Option Compare 语句"
ms.assetid: 54e8eeeb-3b0d-4fb9-acce-fbfbd5975f6e
caps.latest.revision: 37
caps.handback.revision: 37
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Option Compare 语句
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

声明比较字符串数据时要使用的默认比较方法。  
  
## 语法  
  
```  
Option Compare { Binary | Text }  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`Binary`|可选。  字符串比较中的结果基于派生自字符的内部二进制表示形式排序顺序。<br /><br /> 这种比较类型在字符串包含不能解释为文本的字符时尤其有用。  在这种情况下，你不想因为字母顺序的等效性（如，不区分大小写）而使比较出现偏差。|  
|`Text`|可选。  字符串比较中的结果基于由系统的区域设置确定的不区分大小写的文本排序顺序。<br /><br /> 如果字符串包含所有文本字符且你想在比较它们时考虑到母顺序等效性（如，不区分大小写和紧密相关的字母），则这种比较类型非常有用。  例如，你可能认定 `A` 等于 `a`，`Ä` 和 `ä` 出现在 `B` 和 `b` 之前。|  
  
## 备注  
 使用时，`Option Compare` 语句必须在文件中任何其他源代码语句之前。  
  
 `Option Compare` 语句指定字符串比较方法（`Binary` 或 `Text`）。  默认的文本比较方法是 `Binary`。  
  
 `Binary` 比较会对每个字符串中每个字符的数字 Unicode 值进行比较。  `Text` 比较会基于当前区域性中的词汇意义对每个 Unicode 字符进行比较。  
  
 在 Microsoft Windows 中，排序顺序取决于代码页。  有关详细信息，请参阅 [代码页](/visual-cpp/c-runtime-library/code-pages)。  
  
 在下例中，使用 `Option Compare Binary` 对英语\/欧洲代码页 \(ANSI 1252\) 中的字符进行排序，由此产生典型的二进制排序顺序。  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 使用 `Option Compare Text` 对同一代码页中的相同字符进行排序时，会产生以下文本排序顺序。  
  
 `(A=a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
## 当 Option Compare 语句不存在时  
 如果源代码不包括 `Option Compare` 语句，则使用 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 上的“Option Compare”设置。  如果使用命令行编译器，则使用 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) 编译器指定的设置。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
#### 若要在 IDE 中设置 Option Compare  
  
1.  在“解决方案资源管理器”中，选择项目。  在“项目”菜单上，单击“属性”。  有关详细信息，请参阅 [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/zh-cn/983f3c18-832f-4666-afec-74b716ff3e0e)。  
  
2.  单击“编译”选项卡。  
  
3.  设置“Option Compare”框中的值。  
  
 创建新项目时，将“编译”选项卡上的“Option Compare”设置设置为“选项”对话框中的“Option Compare”设置。  若要更改此设置，请在“工具”菜单上，单击“选项”。  在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”。  “VB 默认值”中的初始默认设置为“二进制”。  
  
#### 若要设置命令行上的 Option Compare  
  
-   包括 **vbc** 命令中的 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) 编译器选项。  
  
## 示例  
 下例使用 `Option Compare` 语句将二进制比较设置为默认字符串比较方法。  若要使用此代码，请取消 `Option Compare Binary` 语句的注释，并将其置于源文件顶部。  
  
 [!code-vb[VbVbalrStatements#45](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_1.vb)]  
  
## 示例  
 下例使用 `Option Compare` 语句将不区分大小写的文本排序顺序设置为默认字符串比较方法。  若要使用此代码，请取消 `Option Compare Text` 语句的注释，并将其置于源文件顶部。  
  
 [!code-vb[VbVbalrStatements#46](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_2.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.InStrRev%2A>   
 <xref:Microsoft.VisualBasic.Strings.Replace%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [比较运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [比较运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Like 运算符](../../../visual-basic/language-reference/operators/like-operator.md)   
 [字符串函数](../../../visual-basic/language-reference/functions/string-functions.md)   
 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)