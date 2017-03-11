---
title: "如何：使用 LINQ 转换 XML (Visual Basic) | Microsoft Docs"
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
  - "LINQ to XML [Visual Basic], 转换 XML"
  - "XML [Visual Basic], 转换"
ms.assetid: 815687f4-0bc2-4c0b-adc6-d78744aa356f
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：使用 LINQ 转换 XML (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)使您可以轻松地从一个源读取 XML，并将其转换为新的 XML 格式。  您可以利用 LINQ 查询检索要转换的内容，或将现有文档中的内容更改为新的 XML 格式。  
  
 本主题中的示例将 XML 源文档的内容转换为可在浏览器中查看的 HTML。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 转换 XML 文档  
  
1.  在 Visual Studio 中，在**“控制台应用程序”**项目模板中创建一个新的 Visual Basic 项目。  
  
2.  双击在项目中创建的 Module1.vb 文件以修改 Visual Basic 代码。  将下面的代码添加到 `Module1` 模块的 `Sub Main` 方法。  这段代码将创建源 XML 文档作为 <xref:System.Xml.Linq.XDocument> 对象。  
  
    ```vb#  
    Dim catalog =   
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
              Get the expert insights, practical code samples,   
              and best practices you need   
              to advance your expertise with <technology>Visual   
              Basic .NET</technology>.   
              Learn how to create faster, more reliable applications  
              based on professional,   
              pragmatic guidance by today's top <audience>developers</audience>.  
            </Description>  
          </Book>  
        </Catalog>  
    ```  
  
     [如何：从文件、字符串或流加载 XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md).  
  
3.  在用于创建源 XML 文档的代码后，添加下面的代码，以便从对象检索所有 \<Book\> 元素，并将它们转换到 HTML 文档中。  \<Book\> 元素的列表是使用 LINQ 查询创建的，该查询返回 <xref:System.Xml.Linq.XElement> 对象的集合，其中包含转换后的 HTML。  使用嵌入式表达式可以将源文档的值更改为新的 XML 格式。  
  
     使用 <xref:System.Xml.Linq.XElement.Save%2A> 方法将产生的 HTML 文档写入文件。  
  
    ```vb#  
    Dim htmlOutput =   
      <html>  
        <body>  
          <%= From book In catalog.<Catalog>.<Book>   
              Select <div>  
                       <h1><%= book.<Title>.Value %></h1>  
                       <h3><%= "By " & book.<Author>.Value %></h3>  
                        <h3><%= "Price = " & book.<Price>.Value %></h3>  
                        <h2>Description</h2>  
                        <%= TransformDescription(book.<Description>(0)) %>  
                        <hr/>  
                      </div> %>  
        </body>  
      </html>  
  
    htmlOutput.Save("BookDescription.html")  
    ```  
  
4.  在 `Module1` 的 `Sub Main` 之后，添加一个新方法 \(`Sub`\)，将 \<Description\> 节点转换为指定 HTML 格式。  此方法由上一步中的代码调用，用于保留 \<Description\> 元素的格式。  
  
     此方法将 \<Description\> 元素的子元素替换为 HTML。  `ReplaceWith` 方法用于保留子元素的位置。  \<Description\> 元素的转换内容包含在 HTML 段落 \(\<p\>\) 元素中。  <xref:System.Xml.Linq.XContainer.Nodes%2A> 属性用于检索 \<Description\> 元素的转换内容。  这样确保子元素包括在转换内容中。  
  
     在 `Module1` 的 `Sub Main` 后添加以下代码。  
  
    ```vb#  
    Public Function TransformDescription(ByVal desc As XElement) As XElement  
  
      ' Replace <technology> elements with <b>.  
      Dim content = (From element In desc...<technology>).ToList()  
  
      If content.Count > 0 Then  
        For i = 0 To content.Count - 1  
          content(i).ReplaceWith(<b><%= content(i).Value %></b>)  
        Next  
      End If  
  
      ' Replace <audience> elements with <i>.  
      content = (From element In desc...<audience>).ToList()  
  
      If content.Count > 0 Then  
        For i = 0 To content.Count - 1  
          content(i).ReplaceWith(<i><%= content(i).Value %></i>)  
        Next  
      End If  
  
      ' Return the updated contents of the <Description> element.  
      Return <p><%= desc.Nodes %></p>  
    End Function  
    ```  
  
5.  保存更改。  
  
6.  按 F5 运行代码。  产生的保存的文档将与以下内容类似：  
  
    ```  
    <?xml version="1.0"?>  
    <html>  
      <body>  
        <div>  
          <h1>XML Developer's Guide</h1>  
          <h3>By Garghentini, Davide</h3>  
          <h3>Price = 44.95</h3>  
          <h2>Description</h2>  
          <p>  
            An in-depth look at creating applications  
            with <b>XML</b>. For   
            <i>beginners</i> or   
            <i>advanced</i> developers.  
          </p>  
          <hr />  
        </div>  
        <div>  
          <h1>Developing Applications with Visual Basic .NET</h1>  
          <h3>By Spencer, Phil</h3>  
          <h3>Price = 45.95</h3>  
          <h2>Description</h2>  
          <p>  
            Get the expert insights, practical code   
            samples, and best practices you need   
            to advance your expertise with <b>Visual   
            Basic .NET</b>. Learn how to create faster,  
            more reliable applications based on  
            professional, pragmatic guidance by today's   
            top <i>developers</i>.  
          </p>  
          <hr />  
        </div>  
      </body>  
    </html>  
    ```  
  
## 请参阅  
 [XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [如何：从文件、字符串或流加载 XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)