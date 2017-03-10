---
title: "引用和 Imports 语句 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "程序集 [Visual Basic], 命名空间"
  - "程序集 [Visual Basic], 引用"
  - "Imports 语句, 引用程序集"
  - "命名空间, 程序集"
  - "引用, 程序集"
  - "引用程序集"
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 引用和 Imports 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

通过选择**“项目”**菜单中的**“添加引用”**命令，可以使外部对象能够应用于项目。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的引用可以指向程序集（与类型库类似但包含更多的信息）。  
  
## Imports 语句  
 程序集包括一个或多个命名空间。  添加对程序集的引用时，还可以将 `Imports` 语句添加到控制该程序集的命名空间在模块内的可见性的模块。  `Imports` 语句提供范围上下文，使您可以仅使用提供唯一引用所需的命名空间部分。  
  
 `Imports` 语句的语法如下：  
  
 `Imports` \[         `|` `Aliasname` \=\] `Namespace`  
  
 `Aliasname` 引用一个简称，您可以在代码内使用该简称来引用导入的命名空间。  `Namespace` 是通过各项目引用、项目内的定义或前面的 `Imports` 语句可用的命名空间。  
  
 模块可以包含任意数量的 `Imports` 语句。  如果有任何 `Option` 语句，则它们必须出现在该语句后面，但在其他任何代码之前。  
  
> [!NOTE]
>  不要将项目引用与 `Imports` 语句或 `Declare` 语句混淆。  项目引用使得外部对象（例如程序集中的对象）可用于 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 项目。  `Imports` 语句用于简化对项目引用的访问，但是不提供对这些对象的访问。  `Declare` 语句用于声明对动态链接库 \(DLL\) 里的外部过程的引用。  
  
## 在 Imports 语句中使用别名  
 使用 `Imports` 语句不再需要显式键入引用的完全限定名，从而使访问类方法变得更容易。  别名允许为命名空间的一部分分配更友好的名称。  例如，使单个文本片段以多行形式显示的回车\/换行序列就是 <xref:Microsoft.VisualBasic?displayProperty=fullName> 命名空间中 <xref:Microsoft.VisualBasic.ControlChars> 模块的一部分。  若要不使用别名而直接在程序中使用该常数，则需要键入下面的代码：  
  
 [!code-vb[VbVbalrApplication#3](../../../visual-basic/programming-guide/program-structure/codesnippet/visualbasic/references-and-the-impor_1.vb)]  
  
 在模块中，`Imports` 语句必须始终是紧接着 `Option` 语句后面的最先几行。  下面的代码片段演示如何导入命名空间并将其别名分配给 <xref:Microsoft.VisualBasic.ControlChars?displayProperty=fullName> 模块：  
  
 [!code-vb[VbVbalrApplication#4](../../../visual-basic/programming-guide/program-structure/codesnippet/visualbasic/references-and-the-impor_2.vb)]  
  
 以后对该命名空间的引用可以简短得多：  
  
 [!code-vb[VbVbalrApplication#5](../../../visual-basic/programming-guide/program-structure/codesnippet/visualbasic/references-and-the-impor_3.vb)]  
  
 如果 `Imports` 语句中没有包括别名，则在导入的命名空间内定义的元素可以不加限定地在模块内使用。  如果指定了别名，它必须用作该命名空间内所包含名称的限定符。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ControlChars>   
 <xref:Microsoft.VisualBasic>   
 [NIB How to: Add or Remove References By Using the Add Reference Dialog Box](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：使用命令行创建和使用程序集](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)