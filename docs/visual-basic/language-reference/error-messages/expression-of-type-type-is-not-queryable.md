---
title: "类型 &lt;类型&gt; 的表达式不可查询 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36593"
  - "vbc36593"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36593"
ms.assetid: 6f1f5860-bf97-4885-9ebb-bc87d028095c
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 类型 &lt;类型&gt; 的表达式不可查询
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

类型 \<type\> 的表达式不可查询。请确保不缺少 LINQ 提供程序的程序集引用和\/或命名空间导入。  
  
 可查询类型是在 <xref:System.Linq>、<xref:System.Data.Linq> 和 <xref:System.Xml.Linq> 命名空间中定义的。  必须导入这些命名空间中的一个或多个以执行 LINQ 查询。  
  
 <xref:System.Linq> 命名空间使您能够使用 LINQ 查询诸如集合和数组之类的对象。  
  
 <xref:System.Data.Linq> 命名空间使您能够使用 LINQ 查询 ADO.NET 数据集和 SQL Server 数据库。  
  
 <xref:System.Xml.Linq> 命名空间使您能够使用 LINQ 查询 XML，以及使用 Visual Basic 中的 XML 功能。  
  
 **错误 ID：**BC36593  
  
### 更正此错误  
  
1.  将 <xref:System.Linq>、<xref:System.Data.Linq> 或 <xref:System.Xml.Linq> 命名空间的 `Import` 语句添加到代码文件中。  还可以使用项目设计器（**“我的项目”**）的**“引用”**页导入项目的命名空间。  
  
2.  确保标识为查询源的类型为可查询类型。  即，一个实现 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 的类型。  
  
## 请参阅  
 <xref:System.Linq>   
 <xref:System.Data.Linq>   
 <xref:System.Xml.Linq>   
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)