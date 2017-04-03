---
title: "查询 XDocument 与查询 XElement (C#) | Microsoft Docs"
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
ms.assetid: 46221ff5-62ee-4de8-93ba-66465facb5c1
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9a3da563618ad3dbc9797f252ab51588a43ce8e6
ms.lasthandoff: 03/13/2017


---
# <a name="querying-an-xdocument-vs-querying-an-xelement-c"></a>查询 XDocument 与查询 XElement (C#)
通过 <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName> 加载文档时，你会注意到，要编写的查询与通过 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName> 加载文档时稍有不同。  
  
## <a name="comparison-of-xdocumentload-and-xelementload"></a>XDocument.Load 与 XElement.Load 的比较  
 通过 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName> 将 XML 文档加载到 <xref:System.Xml.Linq.XElement> 中时，位于 XML 树根部的 <xref:System.Xml.Linq.XElement> 包含所加载文档的根元素。 然而，通过 <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName> 将同一个 XML 文档加载到 <xref:System.Xml.Linq.XDocument> 中时，树根部为 <xref:System.Xml.Linq.XDocument> 节点，所加载文档的根元素为 <xref:System.Xml.Linq.XDocument> 所允许的一个子 <xref:System.Xml.Linq.XElement> 节点。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 轴相对于根节点进行操作。  
  
 第一个示例使用 <xref:System.Xml.Linq.XElement.Load%2A> 加载 XML 树。 然后它查询树根部的子元素。  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XElement.Load");  
Console.WriteLine("----");  
XElement doc = XElement.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 此示例将按预期产生以下输出：  
  
```  
Querying tree loaded with XElement.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
 下面的示例与上一个示例基本相同，不同之处在于 XML 树是加载到 <xref:System.Xml.Linq.XDocument>，而不是加载到 <xref:System.Xml.Linq.XElement>。  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 该示例产生下面的输出：  
  
```  
Querying tree loaded with XDocument.Load  
----  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
</Root>  
```  
  
 请注意，同样的查询返回一个 `Root` 节点，而不是返回三个子节点。  
  
 处理这一问题的一种方法是在访问轴方法之前使用 <xref:System.Xml.Linq.XDocument.Root%2A> 属性，如下所示：  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Root.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 此查询现在的执行方式与根部位于 <xref:System.Xml.Linq.XElement> 中的树中的查询相同。 此示例产生以下输出：  
  
```  
Querying tree loaded with XDocument.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
## <a name="see-also"></a>请参阅  
 [基本查询 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
