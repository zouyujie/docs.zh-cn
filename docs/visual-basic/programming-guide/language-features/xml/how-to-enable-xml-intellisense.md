---
title: "如何：在 Visual Basic 中启用 XML IntelliSense | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "XML [Visual Basic], IntelliSense"
  - "XML IntelliSense [Visual Basic]"
ms.assetid: af67d0ee-a4a6-4abf-9c07-5a8cfe80d111
caps.latest.revision: 25
caps.handback.revision: 25
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中启用 XML IntelliSense
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Visual Basic 中的 XML IntelliSense 为 XML 架构中定义的元素提供文字自动完成帮助。  若要启用 Visual Basic 中的 XML IntelliSense，必须执行以下操作：  
  
1.  获取应用程序将读取或写入的 XML 文件的 XML 架构 \(XSD\) 文件。  
  
2.  将这些 XML 架构文件包括在项目中。  
  
3.  将目标命名空间导入到代码文件或项目中。  目标命名空间由 XSD 架构的 `targetNamespace` 或 `tns` 特性标识。  
  
     若要导入目标命名空间，请使用 `Imports` 语句，或者使用项目设计器的**“引用”**页为项目中的所有代码文件添加命名空间。  
  
 有关 Visual Basic 中的 XML IntelliSense 功能的更多信息，请参见 [Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)。  有关导入 XML 命名空间的更多信息，请参见 [Imports 语句（XML 命名空间）](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)或[项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
 ![链接到视频](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") 有关本主题的视频版本，请参见 [Video How to: Enable XML IntelliSense in Visual Basic](http://go.microsoft.com/fwlink/?LinkId=102466)（视频帮助主题：在 Visual Basic 中启用 XML IntelliSense）。  相关的视频演示，请参见 [How Do I Enable XML IntelliSense and Use XML Namespaces?](http://go.microsoft.com/fwlink/?LinkId=143035)（如何启用 XML IntelliSense 和使用 XML 命名空间？）。  
  
## 启用 Visual Basic 中的 XML IntelliSense  
 如果有一个 XML 文件，但没有该文件的 XSD 架构文件，则在 SP1 中，可以使用“XML 到架构向导”来创建 XSD 架构文件。  还可以在 Visual Studio XML 编辑器中使用架构推断。  
  
#### 使用“XML 到架构向导”为 XML 文件创建 XSD 架构文件（需要 SP1）  
  
1.  在项目中，单击**“项目”**菜单上的**“添加新项”**。  
  
2.  从**“数据”**或**“常用项”**模板类别中选择**“XML 到架构”**项模板。  
  
3.  为将用来存储所推断的架构集的 XSD 文件提供文件名，然后单击**“添加”**。  
  
4.  在**“从 XML 文档推断 XML 架构集”**窗口中，添加一个或多个要从中推断 XML 架构集的 XML 文档。  
  
    -   通过使用文件资源管理器中，将包含XML文档的文本文件，单击 **\*\*\* 在文件中添加 \*\*\***。  
  
    -   若要从 HTTP 地址添加 XML 文档，请单击**“从 Web 添加”**。  
  
    -   若要将 XML 文档的内容复制或键入到向导中，请单击**“键入或粘贴 XML”**。  
  
5.  在指定了要从中推断 XML 架构集的所有 XML 文档源之后，单击**“确定”**推断 XML 架构集。  架构集将保存在项目文件夹下面的一个或多个 XSD 文件中。  （对于架构中的每个 XML 命名空间都会创建一个文件。）  
  
#### 在 Visual Studio XML 编辑器中使用架构推断为 XML 文件创建 XSD 架构文件  
  
1.  在 Visual Studio XML 设计器中编辑 XML 文件。  
  
2.  当光标位于 XML 文件中的某个位置时，将显示**“XML”**菜单。  在**“XML”**菜单上，单击**“创建架构”**。  根据从 XML 文件推断出的 XSD 架构创建 XSD 文件。  
  
3.  保存 XSD 架构文件。  
  
    > [!NOTE]
    >  从本应具有相同架构的多个 XML 文档可能推断出不同的 XSD 架构。  如果其中一个 XML 文件中存在特定元素和特性，而另一个文件中不存在这些元素和特性，或者元素的包含顺序不同，则可能发生这种情况。  在使用 XSD 架构推理时，应检查推断出的 XSD 架构是否完整、准确。  
  
#### 包含 XSD 架构文件  
  
-   默认情况下，不能查看 Visual Basic 项目中的 XSD 文件。  如果 XSD 文件已经包含在项目的文件夹中，请在**“解决方案资源管理器”**中单击**“显示所有文件”**按钮。  在**“解决方案资源管理器”**中找到 XSD 文件，右击该文件，然后单击**“将文件包括在项目中”**。  
  
-   如果 XSD 文件还不是项目的组成部分，请在**“解决方案资源管理器”**中右击要存储 XSD 文件的文件夹，指向**“添加”**，然后单击**“现有项”**。  找到 XSD 文件，然后单击**“添加”**。  
  
#### 将 XML 命名空间导入到代码文件中  
  
1.  根据 XSD 架构确定目标命名空间。  
  
2.  在代码文件的开头，为目标 XML 命名空间添加 `Imports` 语句，如下面的示例所示。  
  
     [!code-vb[VbXMLSamples#1](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-enable-xml-intellisense_1.vb)]  
  
     若要导入 XML 命名空间作为默认命名空间（即应用于没有命名空间前缀的 XML 元素和特性的命名空间），请为目标默认 XML 命名空间添加 `Imports` 语句。  不要指定命名空间前缀。  下面是 `Imports` 语句的示例。  
  
     [!code-vb[VbXmlSamples#50](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-enable-xml-intellisense_2.vb)]  
  
#### 为项目中的所有文件导入 XML 命名空间  
  
1.  在代码文件中导入的 XML 命名空间仅应用于该代码文件。  若要导入应用于项目中所有代码文件的 XML 命名空间，请在**“解决方案资源管理器”**中双击**“我的项目”**，打开项目设计器。  
  
2.  在**“引用”**选项卡上的**“导入的命名空间”**框中，按照完整 XML 命名空间声明的格式，键入目标 XML 命名空间（如 `<xmlns: ns="http://sampleNamespace">`）。  如果目标 XML 命名空间未指定命名空间前缀，则该命名空间将是项目的默认 XML 命名空间。  
  
3.  单击**“添加用户导入”**。  
  
## 请参阅  
 [Imports 语句（XML 命名空间）](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)   
 [Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)