---
title: "未定义类型“&lt;类型名&gt;” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30002"
  - "bc30002"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30002"
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 未定义类型“&lt;类型名&gt;”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

该语句引用了未定义的类型。  可以在声明语句（如 `Enum`、`Structure`、`Class` 或 `Interface`）中定义类型。  
  
 **错误 ID：**BC30002  
  
### 更正此错误  
  
-   确保类型定义和类型引用的拼写相同。  
  
-   确保引用可以访问对应的类型定义。  例如，如果类型在另一个模块中且已声明为 `Private`，则请将该类型定义移到引用模块中或将其声明为 `Public`。  
  
-   确保在您的项目中未重新定义类型的命名空间。  如果进行了重新定义，请使用 `Global` 关键字对该类型名称进行完全限定。  例如，如果项目定义了一个名为 `System` 的命名空间，则不能对 <xref:System.Object?displayProperty=fullName> 类型进行访问，除非用 `Global` 关键字对其进行了完全限定：`Global.System.Object`。  
  
-   如果类型已经定义，但定义它时所在的对象库或类型库未在 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中注册，则请单击**“项目”**菜单上的**“添加引用”**，然后选择适当的对象库或类型库。  
  
-   确保类型位于一个属于目标 .NET Framework 配置文件的一部分的程序集中。  有关更多信息，请参见 [.NET Framework 目标错误疑难解答](/visual-studio/msbuild/troubleshooting-dotnet-framework-targeting-errors)。  
  
## 请参阅  
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)