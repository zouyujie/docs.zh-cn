---
title: "编译项目中的 XML 架构时发生错误 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc36810"
  - "vbc36810"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36810"
ms.assetid: 9323b5d2-ba14-4e49-91f1-9ad647162144
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 编译项目中的 XML 架构时发生错误
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在项目中编译 XML 架构时发生错误。因此 XML Intellisense 不可用。  
  
 项目所包含的 XML 架构定义 \(XSD\) 架构中有一个错误。  如果所添加的 XSD 架构 \(.xsd\) 文件与项目的现有 XSD 架构集发生冲突，则会出现此错误。  
  
 **错误 ID：**BC36810  
  
### 更正此错误  
  
-   双击**“错误列表”**窗口中的警告。  Visual Basic 将转到 XSD 文件中引起该警告的位置。  更正 XSD 架构中的错误。  
  
-   确保所有必需的 XSD 架构 \(.xsd\) 文件都包括在项目中。  可能需要单击**“项目”**菜单上的**“显示所有文件”**以在**“解决方案资源管理器”**中查看 .xsd 文件。  右击 .xsd 文件，然后单击**“包括在项目中”**以在项目中包括该文件。  
  
-   如果使用了“XML 到架构向导”，并且从同一个源推断多次架构，就会出现此错误。  在这种情况下，可以从项目中移除现有的 XSD 架构文件，添加一个新的“XML 到架构”项模板，然后为“XML 到架构向导”提供适用于项目的所有 XML 源。  
  
-   如果在 XSD 架构中未找到错误，则 XML 编译器可能没有足够的信息，因此无法提供一条详细的错误消息。  如果确保包括在项目中的 .xsd 文件的 XML 命名空间与针对 Visual Studio 中 XML 架构集标识的 XML 命名空间相匹配，则也许能够获取更加详细的错误信息。  
  
## 请参阅  
 [“错误列表”窗口](/visual-studio/ide/reference/error-list-window)   
 [Visual Basic 中的 XML IntelliSense](../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)