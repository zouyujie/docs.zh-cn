---
title: "如何：修改 XML 文本 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML 轴 [Visual Basic], Value"
  - "XML 文本 [Visual Basic]"
  - "XML 文本 [Visual Basic], 修改"
ms.assetid: 4e864522-a37a-43a2-8236-af80277c5482
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：修改 XML 文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了修改 XML 文本的方便方式。  您可以添加或删除元素和特性，还可以用新的 XML 元素替换现有元素。  本主题提供了有关如何修改现有 XML 文本的多个示例。  
  
### 修改 XML 文本的值  
  
1.  若要修改 XML 文本的值，需要获取对 XML 文本的引用，并将 `Value` 属性设置为期望值。  
  
     下面的代码示例更新了 XML 文档中所有 \<Price\> 元素的值。  
  
     [!code-vb[VbXmlSamples2#4](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_1.vb)]  
  
     下面显示了此代码示例中的示例源 XML 和修改后的 XML。  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>47.20</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>48.25</Price>  
      </Book>  
    </Catalog>  
    ```  
  
    > [!NOTE]
    >  `Value` 属性引用集合中的第一个 XML 元素。  如果集合中有多个具有相同名称的元素，则设置 `Value` 属性仅影响集合中的第一个元素。  
  
### 向 XML 文本添加特性  
  
1.  若要向 XML 文本添加特性，需要首先获取对 XML 文本的引用。  然后可以通过添加新的 XML 特性轴属性来添加特性。  还可以使用 <xref:System.Xml.Linq.XContainer.Add%2A> 方法向 XML 文本添加新的 <xref:System.Xml.Linq.XAttribute> 对象。  下面的示例演示了这两种方法。  
  
     [!code-vb[VbXmlSamples2#5](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_2.vb)]  
  
     下面显示了此代码示例中的示例源 XML 和修改后的 XML。  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" >  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
    ```  
  
     有关 XML 特性轴属性的更多信息，请参见 [XML 特性轴属性](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)。  
  
### 向 XML 文本添加元素  
  
1.  若要向 XML 文本添加元素，需要首先获取对 XML 文本的引用。  然后可以使用 <xref:System.Xml.Linq.XContainer.Add%2A> 方法添加一个新的 <xref:System.Xml.Linq.XElement> 对象作为该元素的最后一个子元素。  可以使用 <xref:System.Xml.Linq.XContainer.AddFirst%2A> 方法添加一个新的 <xref:System.Xml.Linq.XElement> 对象作为该元素的第一个子元素。  
  
     若要在相对于其他子元素的特定位置添加一个新元素，需要首先获取对某个相邻子元素的引用。  然后可以使用 <xref:System.Xml.Linq.XNode.AddBeforeSelf%2A> 方法在该相邻子元素之前添加新的 <xref:System.Xml.Linq.XElement> 对象。  还可以使用 <xref:System.Xml.Linq.XNode.AddAfterSelf%2A> 方法在该相邻子元素之后添加新的 <xref:System.Xml.Linq.XElement> 对象。  
  
     下面的示例演示了上述每种技术的示例。  
  
     [!code-vb[VbXmlSamples2#6](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_3.vb)]  
  
     下面显示了此代码示例中的示例源 XML 和修改后的 XML。  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" >  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" >  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk000"></Book>  
      <Book id="bk331">  
        <Publisher>Microsoft Press</Publisher>  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
        <PublishDate>2005-2-14</PublishDate>  
      </Book>  
      <Book id="bk999"></Book>  
    </Catalog>  
    ```  
  
### 从 XML 文本中移除元素或特性  
  
1.  若要从 XML 文本中移除元素或特性，需要获取对该元素或特性的引用，然后调用 `Remove` 方法，如下面的示例所示。  
  
     [!code-vb[VbXmlSamples2#7](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_4.vb)]  
  
     下面显示了此代码示例中的示例源 XML 和修改后的 XML。  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk000"></Book>  
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
      <Book id="bk999"></Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" editorEmail="someone@example.com">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk000"></Book>  
      <Book id="bk331" editorEmail="someone@example.com">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book> </Catalog>  
    ```  
  
     若要从 XML 文本中移除所有元素或特性，需要获取对该 XML 文本的引用，然后调用 <xref:System.Xml.Linq.XElement.RemoveAll%2A> 方法。  
  
### 修改 XML 文本  
  
1.  若要更改 XML 元素的名称，需要首先获取对该元素的引用。  然后，可以创建一个具有新名称的新的 <xref:System.Xml.Linq.XElement> 对象，并将新的 <xref:System.Xml.Linq.XElement> 对象传递给现有 <xref:System.Xml.Linq.XElement> 对象的 <xref:System.Xml.Linq.XNode.ReplaceWith%2A> 方法。  
  
     如果要替换的元素具有必须保留的子元素，请将新的 <xref:System.Xml.Linq.XElement> 对象的值设置为现有元素的 <xref:System.Xml.Linq.XContainer.Nodes%2A> 属性。  这会将新元素的值设置为现有元素的内部 XML。  另外，还可以将新元素的值设置为现有元素的 `Value` 属性。  
  
     下面的代码示例将所有 \<Description\> 元素替换为 \<Abstract\> 元素。  通过使用 \<Description\> <xref:System.Xml.Linq.XElement> 对象的 <xref:System.Xml.Linq.XContainer.Nodes%2A> 属性，将 \<Description\> 元素的内容保留在新的 \<Abstract\> 元素中。  
  
     [!code-vb[VbXmlSamples2#8](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_5.vb)]  
  
     下面显示了此代码示例中的示例源 XML 和修改后的 XML。  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
        <Description>  
          An in-depth look at creating applications  
          with <technology>XML</technology>. For   
          <audience>beginners</audience> or   
          <audience>advanced</audience> developers.  
        </Description>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
        <Description>  
          Get the expert insights, practical code samples, and best  
          practices you need to advance your expertise with   
          <technology>Visual Basic .NET</technology>.   
          Learn how to create faster, more reliable applications  
          based on professional, pragmatic guidance by today's top  
          <audience>developers</audience>.  
        </Description>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <MSRP>44.95</MSRP>     <Abstract>  
          An in-depth look at creating applications  
          with <technology>XML</technology>. For   
          <audience>beginners</audience> or   
          <audience>advanced</audience> developers.  
        </Abstract>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <MSRP>45.95</MSRP>     <Abstract>  
          Get the expert insights, practical code samples, and best  
          practices you need to advance your expertise with   
          <technology>Visual Basic .NET</technology>.   
          Learn how to create faster, more reliable applications  
          based on professional, pragmatic guidance by today's top  
          <audience>developers</audience>.  
        </Abstract>  
      </Book>  
    </Catalog>  
    ```  
  
## 请参阅  
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [如何：从文件、字符串或流加载 XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)