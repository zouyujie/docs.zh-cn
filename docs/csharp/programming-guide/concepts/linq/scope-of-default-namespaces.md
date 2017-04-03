---
title: "C#1 中默认命名空间的范围 | Microsoft Docs"
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
ms.assetid: fe826236-830f-457a-9027-7ad62c909fae
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
ms.openlocfilehash: 760716dc81f5cd946ae014ed22b6c5a7df64a5dd
ms.lasthandoff: 03/13/2017

---
# <a name="scope-of-default-namespaces-in-c"></a>C 中默认命名空间的范围#
XML 树中表示的默认命名空间不在查询范围内。 如果 XML 在默认命名空间内，则仍须声明一个 <xref:System.Xml.Linq.XNamespace> 变量，并将该变量与本地名称组合在一起，生成一个限定名，在查询中使用。  
  
 查询 XML 树时遇到的一个最常见问题是，如果 XML 树具有默认命名空间，开发人员在编写查询时，有时会将 XML 视为不在命名空间内。  
  
 本主题的第一个示例集演示一种加载但是按不正确方式查询默认命名空间中的 XML 的典型方式。  
  
 第二个示例集演示必需的更正，以便可以查询命名空间中的 XML。  
  
## <a name="example"></a>示例  
 此示例演示如何在命名空间中创建 XML 和一个返回空结果集的查询。  
  
### <a name="code"></a>代码  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements("Child")  
    select el;  
Console.WriteLine("Result set follows:");  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
Console.WriteLine("End of result set");  
```  
  
### <a name="comments"></a>注释  
 此示例产生下面的结果：  
  
```  
Result set follows:  
End of result set  
```  
  
## <a name="example"></a>示例  
 本示例演示如何在命名空间中创建 XML 和一个正确编码的查询。  
  
 与上述不正确编码的示例相比，使用 C# 时的正确方法是声明和初始化一个 <xref:System.Xml.Linq.XNamespace> 对象，并在指定 <xref:System.Xml.Linq.XName> 对象时使用它。 此时，<xref:System.Xml.Linq.XElement.Elements%2A> 方法的自变量是 <xref:System.Xml.Linq.XName> 对象。  
  
### <a name="code"></a>代码  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
XNamespace aw = "http://www.adventure-works.com";  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
Console.WriteLine("Result set follows:");  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
Console.WriteLine("End of result set");  
```  
  
### <a name="comments"></a>注释  
 此示例产生下面的结果：  
  
```  
Result set follows:  
1  
2  
3  
End of result set  
```  
  
## <a name="see-also"></a>请参阅  
 [使用 XML 命名空间 (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)
