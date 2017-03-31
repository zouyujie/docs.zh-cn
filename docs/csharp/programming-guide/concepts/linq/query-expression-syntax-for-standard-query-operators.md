---
title: "标准查询运算符的查询表达式语法 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: e1e17ef2-68ff-4c26-b6e2-015668227fa5
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 115f97eec99d5f22a659532ccf4ed7b20a089014
ms.lasthandoff: 03/13/2017

---
# <a name="query-expression-syntax-for-standard-query-operators-c"></a>标准查询运算符的查询表达式语法 (C#)
某些使用更频繁的标准查询运算符具有专用的 C# 语言关键字语法，使用这些语法可以在查询表达式**中调用这些运算符。 查询表达式是比基于方法**的等效项更具可读性的另一种查询表示形式。 查询表达式子句在编译时被转换为对查询方法的调用。  
  
## <a name="query-expression-syntax-table"></a>查询表达式语法表  
 下表列出包含等效查询表达式子句的标准查询运算符。  
  
|方法|C# 查询表达式语法|  
|------------|---------------------------------|  
|<xref:System.Linq.Enumerable.Cast%2A>|使用显式类型化范围变量，例如：<br /><br /> `from int i in numbers`<br /><br /> （有关详细信息，请参阅 [from 子句](../../../../csharp/language-reference/keywords/from-clause.md)。）|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`group … by`<br /><br /> - 或 -<br /><br /> `group … by … into …`<br /><br /> （有关详细信息，请参阅 [group 子句](../../../../csharp/language-reference/keywords/group-clause.md)。）|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`join … in … on … equals … into …`<br /><br /> （有关详细信息，请参阅 [join 子句](../../../../csharp/language-reference/keywords/join-clause.md)。）|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`join … in … on … equals …`<br /><br /> （有关详细信息，请参阅 [join 子句](../../../../csharp/language-reference/keywords/join-clause.md)。）|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby … descending`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
|<xref:System.Linq.Enumerable.Select%2A>|`select`<br /><br /> （有关详细信息，请参阅 [let 子句](../../../../csharp/language-reference/keywords/select-clause.md)。）|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|多个 `from` 子句。<br /><br /> （有关详细信息，请参阅 [from 子句](../../../../csharp/language-reference/keywords/from-clause.md)。）|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, …`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, … descending`<br /><br /> （有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。）|  
|<xref:System.Linq.Enumerable.Where%2A>|`where`<br /><br /> （有关详细信息，请参阅 [where 子句](../../../../csharp/language-reference/keywords/where-clause.md)。）|  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable>   
 [标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [标准查询运算符按执行方式的分类 (C#)](../../../../csharp/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)
