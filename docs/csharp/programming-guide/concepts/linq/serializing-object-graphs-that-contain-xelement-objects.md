---
title: "序列化包含 XElement 对象的对象图 (C#) | Microsoft Docs"
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
ms.assetid: fcbc3951-3cc4-4d0f-9259-e97549ed68f0
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
ms.openlocfilehash: 752092f7455fa0a10efcaa41166b66ff1f87b16e
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-object-graphs-that-contain-xelement-objects-c"></a>序列化包含 XElement 对象的对象图 (C#)
本主题介绍序列化对象图功能，其中对象图包含对类型为 <xref:System.Xml.Linq.XElement> 的对象的引用。 为了帮助实现此类型的序列化，<xref:System.Xml.Linq.XElement> 实现了 <xref:System.Xml.Serialization.IXmlSerializable> 接口。  
  
 请注意，只有 <xref:System.Xml.Linq.XElement> 类才实现序列化。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[如何：使用 XmlSerializer 进行序列化 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)|演示如何使用 <xref:System.Xml.Serialization.XmlSerializer> 进行序列化。|  
|[如何：使用 DataContractSerializer 进行序列化 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-serialize-using-datacontractserializer.md)|演示如何使用 <xref:System.Runtime.Serialization.DataContractSerializer> 进行序列化。|  
  
## <a name="see-also"></a>请参阅  
 [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
