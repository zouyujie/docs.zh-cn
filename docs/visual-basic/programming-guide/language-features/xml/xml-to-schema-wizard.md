---
title: "XML 到架构向导 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlToSchemaWizard"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "IntelliSense [Visual Basic], XML"
  - "XML [Visual Basic], IntelliSense"
  - "XML IntelliSense [Visual Basic]"
  - "XML 架构, 创建"
ms.assetid: 98c495ba-8f37-4517-a0db-aa738611ab76
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML 到架构向导 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用“XML 到架构向导”可以创建从一个或多个 XML 文档推断的 XML 架构集并将该架构集包括在项目中。  可以使用以下形式的 XML 文档的任意组合：文本文件、HTTP Internet 地址中的 XML 或者键入或粘贴到“XML 到架构向导”中的 XML。  
  
 XML 架构用于为 Visual Basic 中的 XML 属性提供 IntelliSense。  有关更多信息，请参见[XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)和 [Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)。  
  
> [!NOTE]
>  在运行“XML 到架构向导”之前，建议您从项目中移除以前由该向导生成的所有现有的 XSD 文件。  如果您推断一个与现有的架构集相匹配的 XML 架构，则可能会发生冲突，而且 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将无法为 XML 属性提供 IntelliSense。  
  
 “XML 到架构向导”使用 <xref:System.Xml.Schema.XmlSchemaInference> 类为所提供的 XML 创建架构。  因此，可以为架构集创建多个架构文件。  对于所提供的 XML 中的每个 XML 命名空间，都会创建一个可扩展架构定义 \(XSD\) 文件。  有关更多信息，请参见 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法。  
  
 若要访问“XML 到架构向导”，请单击**“项目”**菜单上的**“添加新项”**，并从**“数据”**或**“常用项”**模板组中添加一个**“XML 到架构”**模板。  在包括了要从中推断 XML 架构集的所有 XML 文档源之后，单击**“确定”**创建所推断的架构集。  
  
 **源类型**  
 此列显示 XML 文档源的类型：**“文件”**、**“URL”**或**“XML”**。  
  
 **XML 文档位置**  
 此列显示 XML 文档的路径。  对于所键入或粘贴的 XML 文档，将显示 XML 文档的内容。  
  
 **从文件添加**  
 通过使用文件资源管理器中，单击此按钮将XML文件。  
  
 **从 Web 添加**  
 单击此按钮将提供 XML 文档的 HTTP 地址。  
  
 **键入或粘贴 XML**  
 单击此按钮可在该对话框中键入或粘贴 XML 文档。  
  
## 请参阅  
 <xref:System.Xml.Schema.XmlSchemaInference>   
 [Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)