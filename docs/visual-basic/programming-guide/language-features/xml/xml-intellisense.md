---
title: "Visual Basic 中的 XML IntelliSense | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "IntelliSense [Visual Basic], XML"
  - "Visual Basic 代码, XML"
  - "XML [Visual Basic], IntelliSense"
  - "XML IntelliSense [Visual Basic]"
ms.assetid: 59506ce9-d64e-417e-90fc-e9fe19f0a8fa
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic 中的 XML IntelliSense
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Visual Basic 代码编辑器包含用于 XML 的 IntelliSense 功能，该功能为 XML 架构中定义的元素提供文字自动完成帮助。  如果在项目中包括一个 XML 架构定义 \(XSD\) 文件，并使用 `Imports` 语句导入架构的目标命名空间，则代码编辑器将在 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XDocument> 对象的 IntelliSense 有效成员变量列表中包括 XSD 架构中的元素。  下图演示 <xref:System.Xml.Linq.XElement> 对象的 IntelliSense 成员列表。  
  
 ![Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/media/xml_intellisense.png "XML\_Intellisense")  
XML IntelliSense  
  
## 在 Visual Basic 中启用 XML IntelliSense  
 若要在 Visual Basic 中启用 XML IntelliSense，必须在 Visual Basic 项目中包括一个 XSD 架构文件。  您还必须使用 `Imports` 语句将 XSD 架构的目标命名空间导入到代码文件中。  或者，可以使用 Visual Basic 项目设计器的**“引用”**页将目标命名空间添加到项目级命名空间列表。  有关示例，请参见[如何：在 Visual Basic 中启用 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)。  有关更多信息，请参见[Imports 语句（XML 命名空间）](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)和[项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)。  
  
 请注意，默认情况下，不能查看 Visual Basic 项目中的 XSD 架构文件。  必须单击**“显示所有文件”**按钮才能选择要包括在项目中的 XSD 文件。  
  
### 生成架构文件（架构推断）  
 您可以使用 Visual Studio XML 工具推断 XSD 架构，以此为现有 XML 文件创建 XSD 架构。  
  
-   从 SP1 开始，可以使用“XML 到架构向导”创建从一个或多个 XML 文档推断的 XML 架构集并将该架构集包括在项目中。  可以使用以下形式的 XML 文档的任意组合：文本文件、HTTP Internet 地址中的 XML 或者键入或粘贴到“XML 到架构向导”中的 XML。  若要访问“XML 到架构向导”，请单击**“项目”**菜单上的**“添加新项”**，并从**“数据”**或**“常用项”**模板组中添加一个**“XML 到架构”**模板。  在包括了要从中推断 XML 架构集的所有 XML 文档源之后，单击**“确定”**创建所推断的架构集。  有关更多信息，请参见 [XML 到架构向导](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md)。  
  
-   还可以使用 Visual Studio XML 编辑器从 XML 文件推断 XSD 架构集。  若要使用 XML 编辑器创建 XML 架构，请在 Visual Studio XML 设计器中打开 XML 文件，然后单击**“XML”**菜单中的**“创建架构”**。  创建 XSD 架构集之后，可以将所创建的架构集保存到一个或 XSD 文件中，并在项目中包括这些文件。  有关更多信息，请参见[如何：在 Visual Basic 中启用 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)。  
  
 请注意，可能从多个应具有相同架构的 XML 文档推断出不同的 XSD 架构集。  如果其中一个 XML 文件中存在特定元素和特性，而另一个文件中不存在这些元素和特性，或者元素的包含顺序不同，则可能发生这种情况。  在使用 XSD 架构推断时，应检查推断出的 XSD 架构集是否完整和准确。  
  
## 成员列表  
 在键入句点 \(.\) 以分隔 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象的实例（或者 `IEnumerable(Of XElement)` 或 `IEnumerable(Of XDocument)` 的实例）之后，Visual Basic IntelliSense 会显示可能的对象成员的列表。  初始列表包括三个表示 XML 轴属性的选项，如下面的列表所示。  
  
|||  
|-|-|  
|选项|说明|  
|**\< \>**|选择此选项可显示可能的子元素的列表。  有关更多信息，请参见 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)和 <xref:System.Xml.Linq.XContainer.Elements%2A> 方法。|  
|**@**|选择此选项可显示可能的特性的列表。  有关更多信息，请参见 [XML 轴属性](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)。此选项仅对 <xref:System.Xml.Linq.XElement> 类型的对象可用。|  
|**…\< \>**|选择此选项可显示可能的子代元素的列表。  有关更多信息，请参见[如何：访问 XML 后代元素](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md) 和 <xref:System.Xml.Linq.XContainer.Elements%2A> 方法。|  
  
 选择或开始键入列表中的任一 XML 选项。  成员列表随后将显示 XML 架构中特定于所选选项的可能的成员。  如果导入的 XML 命名空间与特定 XML 命名空间前缀相关联，则成员列表中包括可能的 XML 命名空间前缀的列表。  
  
 例如，考虑下面的 XSD 架构。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema attributeFormDefault="unqualified"   
           elementFormDefault="qualified"   
           targetNamespace="http://SamplePurchaseOrder"   
           xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="PurchaseOrders">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="PurchaseOrder">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="Address" />  
              <xs:element name="Items" />  
              <xs:element name="Comment" />  
            </xs:sequence>  
            <xs:attribute name="PurchaseOrderNumber" type="xs:unsignedShort" use="required" />  
            <xs:attribute name="OrderDate" type="xs:string" use="required" />  
          </xs:complexType>  
        </xs:element>  
      </xs:sequence>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 该 XSD 架构的有效 XML 类似于下面的内容。  
  
```  
<?xml version="1.0"?>  
<PurchaseOrders xmlns="http://SamplePurchaseOrder">  
  <PurchaseOrder PurchaseOrderNumber="12345" OrderDate="2000-1-1">  
    <Address />  
    <Items />  
    <Comment />  
  </PurchaseOrder>  
</PurchaseOrders>  
```  
  
 如果您在项目中包括此 XSD 架构文件，并将目标命名空间从 XSD 架构导入到代码文件或项目中，则在您键入 Visual Basic 代码时，Visual Basic IntelliSense 将显示架构中的成员。  如果 XSD 架构的目标命名空间作为默认命名空间导入，并且您键入下面的内容，则 IntelliSense 将显示 `PurchaseOrder` XML 元素可能具有的子元素的列表。  
  
```  
Dim po = <PurchaseOrder />  
po.<  
```  
  
 该列表由 Address、Comment 和 Items 元素组成。  
  
### IntelliSense 列表项的确定性级别  
 无法准确确定要用于 IntelliSense 的 XSD 类型。  因此，XML IntelliSense 通常会显示可能成员的扩展列表。  为了帮助您从 IntelliSense 成员列表中选择项，在显示项时带有指示，表明 XML IntelliSense 对特定成员具有的确定性级别。  
  
 有时，XML IntelliSense 可以识别 XSD 架构中的特定类型。  在这些情况下，它将以高确定性级别显示该 XSD 类型可能具有的子元素、特性或子代元素。  使用选中标记来标识这些项。  
  
 但是，XML IntelliSense 有时无法识别 XSD 架构中的特定类型。  在这些情况下，它将以低确定性级别显示项目的 XSD 架构中可能具有的子元素、特性或子代元素的扩展列表。  使用问号来标识这些项。  
  
## 请参阅  
 [如何：在 Visual Basic 中启用 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)   
 [XML 到架构向导](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md)   
 [Imports 语句（XML 命名空间）](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 特性轴属性](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)   
 [XML 后代轴属性](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)   
 [项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)