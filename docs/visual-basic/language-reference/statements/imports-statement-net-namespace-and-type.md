---
title: "Imports 语句（.NET 命名空间和类型） | Microsoft Docs"
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
  - "vb.Imports"
  - "imports"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "别名 [Visual Basic], import"
  - "别名 [Visual Basic], Imports 语句"
  - "容器元素 [Visual Basic]"
  - "已声明元素名称 [Visual Basic], 限定"
  - "已声明元素 [Visual Basic], 容器元素"
  - "导入别名 [Visual Basic]"
  - "导入 [Visual Basic]"
  - "Imports 语句 [Visual Basic]"
  - "Imports 语句 [Visual Basic], 语法"
  - "命名空间 [Visual Basic], 导入"
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
caps.latest.revision: 40
caps.handback.revision: 40
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Imports 语句（.NET 命名空间和类型）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使类型名称引用，而无需命名空间限定。  
  
## 语法  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`aliasname`|选项。  代码可以引用 `namespace` 而不是完全限定字符串的 *导入别名* 或名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`namespace`|必需。  导入的命名空间的完全限定名。  可以是命名空间字符串嵌套到所有层。|  
|`element`|选项。  在命名空间声明的编程元素的名称。  可以是任何容器元素。|  
  
## 备注  
 `Imports` 语句允许在将直接引用的特定空间中包含的类型。  
  
 可以提供一个命名空间名称或嵌套的命名空间字符串。  ，如下面的示例所示，为每个嵌套的命名空间从下一个较高级别命名空间分隔。`.`句点 \(\) 之前。  
  
 `Imports System.Collections.Generic`  
  
 每个源文件可以包含任意数量的 `Imports` 语句。  这些必须跟随任何选项声明，如 `Option Strict` 语句，并且，它们必须在任何编程元素声明，如 `Module` 或 `Class` 语句。  
  
 仅可以 `Imports` 在文件级。  这意味着导入的声明上下文必须是源文件，并且不能是命名空间，类，结构，模块，接口，程序，或者块。  
  
 请注意 `Imports` 语句由其他项目和程序集不使元素可供您的项目。  导入不能取代引用。  它只撤消需要限定到您的项目还可用的名称。  有关更多信息，请参见中的 “导入包含元素” [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
> [!NOTE]
>  通过使用， [项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)您可以定义隐式 `Imports` 语句。  有关更多信息，请参见 [如何：添加或移除导入的命名空间 \(Visual Basic\)](../Topic/How%20to:%20Add%20or%20Remove%20Imported%20Namespaces%20\(Visual%20Basic\).md)。  
  
## 导入别名  
 *导入别名* 定义命名空间或类型的别名。  导入别名很有用，当您需要使用在一个或多个命名空间声明同名的项时。  有关更多信息和示例，请参见中的 “限定元素名称” [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
 不应声明成员在具有名称的模块级别和 `aliasname`相同。  否则， Visual Basic 编译器为个声明的成员仅使用 `aliasname` 和不再将其识别为导入别名。  
  
 虽然对于声明导入别名使用的语法是类似有关导入 XML 命名空间前缀使用，结果是不同的。  导入别名用作表达式在代码中，，而 XML 命名空间前缀在 XML 文本或 XML 轴属性只能用作标题为限定的元素或特性名称。  
  
### 元素名称  
 如果提供 `element`，它必须表示 *容器元素*，即，可以包含其他组件的编程元素。  容器元素包括类、结构、模块、接口和枚举。  
  
 可用元素的大小使 `Imports` 语句取决于是否指定 `element`。  如果指定 `namespace`、该命名空间中的任何一个命名的容器元素的成员和成员该命名空间中，可没有限定。  如果指定 `namespace` 和 `element`，因此，只有该元素的成员可用的没有限定。  
  
## 示例  
 使用 <xref:System.IO.DirectoryInfo> 类，下面的示例返回位于 C:\\ 目录中的所有文件夹。  
  
 代码没有 `Imports` 语句在文件的顶部。  因此， `DirectoryInfo`、 <xref:System.Text.StringBuilder>和 <xref:Microsoft.VisualBasic.ControlChars.CrLf> 引用都完全限定的命名空间。  
  
 [!code-vb[VbVbalrStatements#152](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_1.vb)]  
  
## 示例  
 下面的示例包含引用的命名空间的 `Imports` 语句。  因此，类型无需完全限定的命名空间。  
  
 [!code-vb[VbVbalrStatements#153](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_2.vb)]  
  
 [!code-vb[VbVbalrStatements#154](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_3.vb)]  
  
## 示例  
 下面的示例创建包含引用的命名空间的别名的 `Imports` 语句。  类型未用别名。  
  
 [!code-vb[VbVbalrStatements#155](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_4.vb)]  
  
 [!code-vb[VbVbalrStatements#156](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_5.vb)]  
  
## 示例  
 下面的示例包括创建引用类型的别名的 `Imports` 语句。  别名用于指定类型。  
  
 [!code-vb[VbVbalrStatements#157](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_6.vb)]  
  
 [!code-vb[VbVbalrStatements#158](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_7.vb)]  
  
## 请参阅  
 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)