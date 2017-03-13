---
title: "变量疑难解答 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "疑难解答 [Visual Basic], 变量"
  - "变量 [Visual Basic], 疑难解答"
ms.assetid: 928a2dc8-e565-4ae4-8ba3-80cc0cb50090
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 变量疑难解答 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此页列出在使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的变量时可能出现的一些常见问题。  
  
## 无法访问对象的成员  
 如果你的代码尝试访问对象上的属性或方法，可能会出现两种错误结果：  
  
-   如果你声明对象变量为特定类型，然后引用不是由此类型定义的成员，则编译器可能生成错误消息。  
  
-   当分配给对象变量的对象不显示代码正尝试访问的成员时，将产生运行时 <xref:System.MemberAccessException>。 当变量为 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)，如果成员不是 `Public`，则也可能遇到这种异常。 这是因为后期绑定只允许访问 `Public` 成员。  
  
 当 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 设置类型检查 `On` 时，对象变量仅可访问声明它所用的类的方法和属性。 下面的示例阐释了这一点。  
  
 [!CODE [VbVbalrStatements#49](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrStatements#49)]  
  
 [!code-vb[VbVbalrVariables#2](../../../../visual-basic/programming-guide/language-features/variables/codesnippet/VisualBasic/troubleshooting-variables_1.vb)]  
  
 在此示例中，`p` 仅可使用 <xref:System.Object> 类的成员，这不包括 `Left` 属性。 另一方面，`q` 已声明为 <xref:System.Windows.Forms.Label> 类型，因此它可以使用 <xref:System.Windows.Forms> 命名空间中 <xref:System.Windows.Forms.Label> 类的所有方法和属性。  
  
### 正确方法  
 若要能够访问特定类的对象的所有成员，则尽可能将对象变量声明为该类的类型。 如果你不能这样做（例如如果你不知道编译时的对象类型），则必须将 `Option Strict` 设置为 `Off`，并声明变量为 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)。 这将允许将任意类型的对象分配给该变量，你应该采取措施确保当前分配的对象是可接受的类型。 你可以使用 [TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md) 做出此判断。  
  
## 其他组件不能访问你的变量  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 名称*不区分大小写*。 如果这两个名称只是字母大小写不同，编译器会将其解析为相同的名称。 例如，它认为 `ABC` 和 `abc` 指的是同一个声明的元素。  
  
 但是，公共语言运行时 \(CLR\) 使用*区分大小写*绑定。 因此，当你生成程序集或 DLL 并使其可供其他程序集使用时，则名称将不再不区分大小写。 例如，如果你用名为 `ABC` 的元素定义类，而其他程序集通过公共语言运行时使用你的类，则元素必须指的是 `ABC`。 如果你以后重新编译你的类并将元素名称更改为 `abc`，则使用你的类的其他程序集将不能再访问此元素。 因此，发布程序集的更新版本时，不应该更改公共元素的字母大小写。  
  
 有关详细信息，请参阅[公共语言运行时](../Topic/Common%20Language%20Runtime%20\(CLR\).md)。  
  
### 正确方法  
 若要允许其他组件访问你的变量，将其名称视为区分大小写。 当测试类或模块时，确保其他程序集绑定到你所希望的变量。 发布组件后，请勿对现有变量名称进行修改，包括更改大小写。  
  
## 正在使用的错误变量  
 当你有名称相同的多个变量时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将尝试解析该名称的每个引用。 如果变量具有不同的范围，编译器将解析对范围最小的声明的引用。 如果它们具有相同的范围，解析将失败，编译器将引发错误。 有关详细信息，请参阅[对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
### 正确方法  
 避免使用名称相同范围不同的变量。 如果你正在使用其他程序集或项目，尽量避免使用在那些外部组件中定义的任何名称。 如果你有名称相同的多个变量，确保限定对它的每个引用。 有关详细信息，请参阅[对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
## 请参阅  
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [如何：访问对象的成员](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [如何：确定对象变量引用的类型](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)