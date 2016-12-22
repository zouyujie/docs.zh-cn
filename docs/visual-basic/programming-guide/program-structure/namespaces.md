---
title: "Visual Basic 中的命名空间 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.global"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "程序集 [Visual Basic], 命名空间"
  - "名称冲突"
  - "Global 关键字 [Visual Basic]"
  - "命名空间污染"
  - "名称, 避免冲突"
  - "命名冲突, 命名空间"
  - "命名空间, 程序集"
  - "Visual Basic 代码, 命名空间"
  - "完全限定名"
  - "命名约定, 命名冲突"
  - "命名空间"
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic 中的命名空间
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

命名空间组织程序集中定义的对象。 程序集可以包含多个命名空间，命名空间又可以包含其他命名空间。 使用大组对象（比如类库）时，命名空间可以避免多义性和简化引用。  
  
 例如，[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 在 <xref:System.Windows.Forms?displayProperty=fullName> 命名空间中定义 <xref:System.Windows.Forms.ListBox> 类。 以下代码段演示如何使用此类的完全限定名称声明变量：  
  
 [!CODE [VbVbalrApplication#6](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#6)]  
  
## 避免名称冲突  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 命名空间解决有时被称为*命名空间污染*的问题，即类库开发人员会受到另一个库中使用的相似名称的妨碍。 这些冲突及其现有组件有时被称为*名称冲突*。  
  
 例如，如果创建一个名为 `ListBox`的新类，你可以在项目中不加限定地使用它。 但是，如果想要在同一项目中使用 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]<xref:System.Windows.Forms.ListBox> 类，则必须使用完全限定引用，以使引用唯一。 如果引用不唯一，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会产生一个错误，指出名称不明确。 下面的代码示例演示如何声明这些对象：  
  
 [!CODE [VbVbalrApplication#7](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#7)]  
  
 下图显示两个命名空间层次结构，它们都包含一个名为 `ListBox` 的对象。  
  
 ![命名空间层次结构](../../../visual-basic/programming-guide/program-structure/media/vanamespacehierarchy.png "vaNamespaceHierarchy")  
  
 默认情况下，使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 创建的所有可执行文件都包含与项目具有相同名称的命名空间。 例如，如果在一个名为 `ListBoxProject` 的项目中定义对象，则可执行文件 ListBoxProject.exe 包含一个名为 `ListBoxProject` 的命名空间。  
  
 多个程序集可以使用相同的命名空间。[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会将它们视为多个名称的单个组。 例如，你可以为名为 `Assemb1` 的程序集中名为 `SomeNameSpace` 的命名空间定义多个类，并为名为 `Assemb2` 的程序集中相同的命名空间定义其他类。  
  
## 完全限定名  
 完全限定名是以在其中定义对象的命名空间的名称为前缀的对象引用。 如果创建对类的引用（通过选择“项目”菜单中的“添加引用”），然后为代码中的对象使用完全限定名，则可以使用在其他项目中定义的对象。 以下代码段演示如何为来自另一个项目命名空间的对象使用完全限定名：  
  
 [!CODE [VbVbalrApplication#8](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#8)]  
  
 完全限定名避免命名冲突，因为它们可以使编译器确定哪些对象正在被使用。 但是，名称本身可能会变得冗长繁杂。 为避免这一问题，可以使用 `Imports` 语句来定义*别名* \- 可用于代替完全限定名的缩略名。 例如，以下代码示例为两个完全限定名创建别名，并使用这些别名来定义两个对象。  
  
 [!CODE [VbVbalrApplication#9](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#9)]  
  
 [!CODE [VbVbalrApplication#10](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#10)]  
  
 如果不带别名使用 `Imports` 语句，可以使用命名空间中的所有名称而无需限定，只要这些名称唯一。 如果项目包含同名的项的命名空间使用的 `Imports` 语句，则使用时必须完全限定该名称。 例如，假设项目包含以下两个 `Imports` 语句：  
  
 [!CODE [VbVbalrApplication#11](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#11)]  
  
 如果尝试使用 `Class1` 而不对其完全限定，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会产生错误消息，指出名称 `Class1` 不明确。  
  
## 命名空间级别语句  
 在命名空间中，可以定义项，如模块、接口、类、委托、枚举、结构和其他命名空间。 无法在命名空间级别定义属性、过程、变量和事件等项。 这些项必须在模块、结构或类等容器内部进行声明。  
  
## 完全限定名中的全局关键字  
 如果定义了命名空间的嵌套层次结构，该层次结构内的代码可能会被阻止访问 .NET Framework 的 <xref:System?displayProperty=fullName> 命名空间。 下面的示例阐释了 `SpecialSpace.System` 命名空间阻止访问 <xref:System?displayProperty=fullName> 的层次结构。  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As System.Int32  
                Dim n As System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 结果是，Visual Basic 编译器无法成功地解析对 <xref:System.Int32?displayProperty=fullName> 的引用，因为 `SpecialSpace.System` 没有定义 `Int32`。 可以使用 `Global` 关键字在.NET Framework 类库的最外层级别上启动限定链。 这将允许你指定类库中的 <xref:System?displayProperty=fullName> 命名空间或任何其他命名空间。 下面的示例阐释了这一点。  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As Global.System.Int32  
                Dim n As Global.System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 可以使用 `Global` 访问其他根级别的命名空间，如 <xref:Microsoft.VisualBasic?displayProperty=fullName> 和与项目相关联的任何命名空间。  
  
## 命名空间语句中的全局关键字  
 还可以使用 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md) 中的 `Global`关键字。 这将允许你定义项目根命名空间之外的命名空间。  
  
 项目中的所有命名空间均基于项目的根命名空间。  Visual Studio 针对项目中的所有代码，将项目名称指定为默认根命名空间。 例如，如果项目命名为 `ConsoleApplication1`，则其编程元素属于命名空间 `ConsoleApplication1`。 如果声明 `Namespace Magnetosphere`，项目中对 `Magnetosphere` 的引用将访问 `ConsoleApplication1.Magnetosphere`。  
  
 以下示例使用 `Global` 关键字来为项目声明根命名空间之外的命名空间。  
  
 [!CODE [VbVbalrApplication#22](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#22)]  
  
 在命名空间声明中，`Global` 不能嵌套于另一个命名空间中。  
  
 可以使用 [“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic) 查看和修改项目的“根命名空间”。  对于新项目，“根命名空间”默认为该项目的名称。 若要使 `Global` 成为顶级命名空间，可以清除“根命名空间”条目，以便此框为空。 清除“根命名空间”移除了命名空间声明中需要的 `Global` 关键字。  
  
 如果 `Namespace` 语句声明一个名称，而该名称也是.NET Framework 中的命名空间，则如果 `Global` 关键字未在完全限定名中使用，.NET Framework 命名空间会变得不可用。 在不使用 `Global` 关键字的情况下，若要启用对该 .NET Framework 命名空间的访问，可以将 `Global` 关键字包括到 `Namespace` 语句中。  
  
 以下示例在 `System.Text` 命名空间声明中具有 `Global` 关键字。  
  
 如果命名空间声明中不存在 `Global` 关键字，若不指定 `Global.System.Text.StringBuilder`将无法访问<xref:System.Text.StringBuilder>。 对于名为 `ConsoleApplication1` 的项目，如果未使用 `Global` 关键字，对 `System.Text` 的引用会访问 `ConsoleApplication1.System.Text`。  
  
 [!CODE [VbVbalrApplication#21](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrApplication#21)]  
  
## 请参阅  
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms?displayProperty=fullName>   
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：使用命令行创建和使用程序集](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [在 Office 解决方案中编写代码](/office-dev/office-dev/writing-code-in-office-solutions)