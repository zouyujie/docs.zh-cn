---
title: "LINQ to XML 注释 3 | Microsoft Docs"
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
ms.assetid: 54e7b9d0-07f5-488f-9065-b6e6b870f810
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 13718f509eee46853020cfe1dd27ee85437d2e6d
ms.lasthandoff: 03/13/2017


---
# <a name="linq-to-xml-annotations"></a>LINQ to XML 批注
[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中的注释可将任意类型的任意对象与 XML 树中的任何 XML 组件相关联。  
  
 若要将注释添加到 XML 组件（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XAttribute>），请调用 <xref:System.Xml.Linq.XObject.AddAnnotation%2A> 方法。 批注是按类型检索的。  
  
 请注意，批注不是 XML 信息集的一部分，不对它们进行序列化和反序列化。  
  
## <a name="methods"></a>方法  
 处理批注时可以使用以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XObject.AddAnnotation%2A>|将对象添加到 <xref:System.Xml.Linq.XObject> 的注释列表。|  
|<xref:System.Xml.Linq.XObject.Annotation%2A>|从 <xref:System.Xml.Linq.XObject> 获取指定类型的第一个注释对象。|  
|<xref:System.Xml.Linq.XObject.Annotations%2A>|为 <xref:System.Xml.Linq.XObject> 获取指定类型的注释集合。|  
|<xref:System.Xml.Linq.XObject.RemoveAnnotations%2A>|从 <xref:System.Xml.Linq.XObject> 删除指定类型的注释。|  
  
## <a name="see-also"></a>请参阅  
 [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
