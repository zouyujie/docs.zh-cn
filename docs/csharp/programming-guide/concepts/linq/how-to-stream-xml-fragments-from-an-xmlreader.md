---
title: "如何：从 XmlReader 流式处理 XML 片段 (C#) | Microsoft Docs"
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
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
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
ms.openlocfilehash: 4bb11e120a123b701e45916b983032797c0ea8b6
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-c"></a>如何：从 XmlReader 流式处理 XML 片段 (C#)
如果必须处理很大的 XML 文件，将整个 XML 树加载到内存可能不可行。 本主题演示如何使用 <xref:System.Xml.XmlReader> 对片段进行流式处理。  
  
 使用 <xref:System.Xml.XmlReader> 读取 <xref:System.Xml.Linq.XElement> 对象的最有效方法之一是编写自己的自定义轴方法。 轴方法通常返回集合（如 <xref:System.Xml.Linq.XElement> 的 <xref:System.Collections.Generic.IEnumerable%601>），如本主题中的示例所示。 在自定义轴方法中，在通过调用 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 方法创建 XML 片段后，可以使用 `yield return` 返回该集合。 这可为您的自定义轴方法提供延迟执行语义。  
  
 从 <xref:System.Xml.XmlReader> 对象创建 XML 树，<xref:System.Xml.XmlReader> 必须定位在元素上。 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 方法在读取该元素的结束标记之前不会返回。  
  
 如果要创建部分树，则可以实例化 <xref:System.Xml.XmlReader>，将读取器定位在要转换为 <xref:System.Xml.Linq.XElement> 树的节点上，然后创建 <xref:System.Xml.Linq.XElement> 对象。  
  
 [如何：通过对标头信息的访问流式处理 XML 片段 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md) 主题包含有关如何流式处理更复杂的文档的信息和示例。  
  
 [如何：执行大型 XML 文档的流式转换 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-perform-streaming-transform-of-large-xml-documents.md) 主题包含如何使用 LINQ to XML 在保持小内存需求量的同时转换极大 XML 文档的示例。  
  
## <a name="example"></a>示例  
 本示例创建一个自定义轴方法。 可以通过使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询来查询该方法。 自定义轴方法 `StreamRootChildDoc` 是一个专门设计的方法，用于读取具有重复 `Child` 元素的文档。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 该示例产生下面的输出：  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 在本示例中，源文档非常小。 但是即使有数百万个 `Child` 元素，本示例也仍具有很小的内存需求量。  
  
## <a name="see-also"></a>请参阅  
 [分析 XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)
