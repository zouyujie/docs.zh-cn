---
title: "LINQ to XML 轴概述 (Visual Basic) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 9161f151-cfa8-4408-94ba-08a9ba3a486d
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b127aa6b443e865c76831d886f110550ec785e9b
ms.lasthandoff: 03/13/2017


---
# <a name="linq-to-xml-axes-overview-visual-basic"></a>LINQ to XML 轴概述 (Visual Basic)
创建 XML 树或将 XML 文档加载到 XML 树之后，可以进行查询，从而查找元素和属性并检索它们的值。 您通过检索集合*轴方法*也称为*轴*。 一些轴是在方法<xref:System.Xml.Linq.XElement>和<xref:System.Xml.Linq.XDocument>类中返回<xref:System.Collections.Generic.IEnumerable%601>集合。</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 一些轴是在<xref:System.Xml.Linq.Extensions>类</xref:System.Xml.Linq.Extensions>中的扩展方法 实现为扩展方法的轴对集合进行操作，然后返回集合。  
  
 如中所述[XElement 类概述](http://msdn.microsoft.com/library/d35180fe-7016-4895-9bfc-ba1e3f7875ec)、<xref:System.Xml.Linq.XElement>对象表示单个元素节点。</xref:System.Xml.Linq.XElement> 元素的内容可以是复杂的（有时称为结构化内容），也可以是简单元素。 简单元素可以是空的，也可以包含值。 如果节点包含结构化内容，则可以使用各种轴方法来检索子代元素的枚举。 最常使用的轴方法是<xref:System.Xml.Linq.XContainer.Elements%2A>和<xref:System.Xml.Linq.XContainer.Descendants%2A>。</xref:System.Xml.Linq.XContainer.Descendants%2A> </xref:System.Xml.Linq.XContainer.Elements%2A>  
  
 除了返回集合的轴方法之外，还有两个方法会在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询中经常用到。 <xref:System.Xml.Linq.XContainer.Element%2A>方法返回单个<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XContainer.Element%2A> <xref:System.Xml.Linq.XElement.Attribute%2A>方法返回单个<xref:System.Xml.Linq.XAttribute>。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement.Attribute%2A>  
  
 对于很多应用来说，[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询提供了检查树、从树中提取数据以及转换树的最有效的方法。 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]实现的对象上运行的查询<xref:System.Collections.Generic.IEnumerable%601>，和[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]轴返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>集合，和<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XAttribute>集合。</xref:System.Xml.Linq.XAttribute> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.Generic.IEnumerable%601> 需要使用这些集合来执行查询。  
  
 除了检索元素和属性集合的轴方法之外，还有一些轴方法可以十分详尽地循环访问树。 例如，可以处理树的节点，而不是处理元素和属性。 节点比元素和属性有更细的粒度。 处理节点时，可以检查 XML 注释、文本节点、处理指令以及其他方面。 该功能很重要，例如对正在编写字处理器并希望将文档保存为 XML 的用户非常有用。 但是，大部分 XML 程序员主要关心的是元素、属性和它们的值。  
  
## <a name="methods-for-retrieving-a-collection-of-elements"></a>用于检索元素集合的方法  
 下面的方法的概述了<xref:System.Xml.Linq.XElement>类 （或其基类） 上调用<xref:System.Xml.Linq.XElement>要返回的元素的集合。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement>  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>此元素的上级。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>这些上级具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>的</xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>此元素的子代。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>这些子代具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>的</xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>此元素的子元素。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>子元素具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>此元素之后的元素。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>此元素之后的元素</xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>此元素之前的元素。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>此元素之前的元素的元素</xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>以及此元素及其上级。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>的元素</xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>此元素及其子代。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 重载方法返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>的元素</xref:System.Xml.Linq.XElement></xref:System.Collections.Generic.IEnumerable%601>|  
  
## <a name="method-for-retrieving-a-single-element"></a>用于检索单个元素的方法  
 下面的方法检索单个子级从<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement>  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName>|返回第一个子<xref:System.Xml.Linq.XElement>对象具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>对象</xref:System.Xml.Linq.XElement>|  
  
## <a name="method-for-retrieving-a-collection-of-attributes"></a>用于检索属性集合的方法  
 下面的方法检索属性从<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement>  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName>|返回<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XAttribute>的所有属性。</xref:System.Xml.Linq.XAttribute> </xref:System.Collections.Generic.IEnumerable%601>|  
  
## <a name="method-for-retrieving-a-single-attribute"></a>用于检索单个属性的方法  
 下面的方法检索单个属性从<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement>  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName>|返回<xref:System.Xml.Linq.XAttribute>具有指定<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XAttribute>|  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 轴 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
