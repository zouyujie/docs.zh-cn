---
title: "XML 文档文本 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralDocument"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "文档文本 [Visual Basic]"
  - "XML 文档文本 [Visual Basic]"
  - "XML 文档 [Visual Basic], 创建"
  - "XML 文本 [Visual Basic], 文档"
ms.assetid: f7bbee56-0911-41de-b907-96f20450137b
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# XML 文档文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用于表示 <xref:System.Xml.Linq.XDocument> 对象的文本。  
  
## 语法  
  
```  
<?xml version="1.0" [encoding="encoding"] [standalone="standalone"] ?>  
[ piCommentList ]  
rootElement  
[ piCommentList ]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`encoding`|可选。  用于声明文档使用哪种编码的文本。|  
|`standalone`|可选。  文本。  必须为“yes”或“no”。|  
|`piCommentList`|可选。  XML 处理指令和 XML 注释的列表。  采用下面的格式：<br /><br /> `piComment [` `piComment` `... ]`<br /><br /> 每个 `piComment` `` 都可以为下列内容之一：<br /><br /> -   [XML 处理指令文本](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md).<br />-   [XML 注释文本](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md).|  
|`rootElement`|必选。  文档的根元素。  格式为以下格式之一：<br /><br /> <ul><li>[XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).</li><li>形式为 `<%=` `elementExp` `%>` 的嵌入式表达式。  `elementExp` 返回下列内容之一：<br /><br /> <ul><li><xref:System.Xml.Linq.XElement> 对象。</li><li>包含一个 <xref:System.Xml.Linq.XElement> 对象以及任意数量的 <xref:System.Xml.Linq.XProcessingInstruction> 和 <xref:System.Xml.Linq.XComment> 对象的集合。</li></ul></li></ul><br /> 有关更多信息，请参见 [XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。|  
  
## 返回值  
 <xref:System.Xml.Linq.XDocument> 对象。  
  
## 备注  
 XML 文档文本由位于文本开头的 XML 声明标识。  虽然每个 XML 文档文本都必须只具有一个 XML 根元素，但是可以具有任意数量的 XML 处理指令和 XML 注释。  
  
 XML 文档文本不能出现在 XML 元素中。  
  
> [!NOTE]
>  XML 文本可以跨多个行，而无需使用行继续符。  这使您可以复制 XML 文档中的内容并将该内容直接粘贴到 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 程序中。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将 XML 文档文本转换为对 <xref:System.Xml.Linq.XDocument.%23ctor%2A> 和 <xref:System.Xml.Linq.XDeclaration.%23ctor%2A> 构造函数的调用。  
  
## 示例  
 下面的示例创建一个 XML 文档，该文档具有一个 XML 声明、一条处理指令、一条注释以及一个包含其他元素的元素。  
  
 [!code-vb[VbXMLSamples#30](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-document-literal_1.vb)]  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 <xref:System.Xml.Linq.XProcessingInstruction>   
 <xref:System.Xml.Linq.XComment>   
 <xref:System.Xml.Linq.XDocument>   
 [XML 处理指令文本](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)   
 [XML 注释文本](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)   
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)