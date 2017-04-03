---
title: "序列化为文件、TextWriter 和 XmlWriter1 | Microsoft Docs"
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
ms.assetid: bd3ea6f7-895b-4ff4-a625-fe2bb55b1886
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
ms.openlocfilehash: f61324395e81509e5800e99b654a8c669d4397f0
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-to-files-textwriters-and-xmlwriters"></a>序列化为文件、TextWriter 和 XmlWriter
可将 XML 树序列化为 <xref:System.IO.File>、<xref:System.IO.TextWriter> 或 <xref:System.Xml.XmlWriter>。  
  
 使用 `ToString` 方法，可将任何 XML 组件（包括 <xref:System.Xml.Linq.XDocument> 和 <xref:System.Xml.Linq.XElement>）序列化为字符串。  
  
 若要在序列化为字符串时禁止格式化，可使用 <xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=fullName> 方法。  
  
 序列化为文件时，默认行为是格式化（缩进）生成的 XML 文档。 缩进时，不会保留 XML 树中无意义的空白。 若要使用格式化方式进行序列化，请使用不将 <xref:System.Xml.Linq.SaveOptions> 作为参数的以下方法的重载之一：  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 如果要选择不在 XML 树中缩进，并保留无意义空白，请使用将 <xref:System.Xml.Linq.SaveOptions> 作为参数的以下方法的重载之一：  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 有关示例，请参见相应的参考主题。  
  
## <a name="see-also"></a>请参阅  
 [序列化 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
