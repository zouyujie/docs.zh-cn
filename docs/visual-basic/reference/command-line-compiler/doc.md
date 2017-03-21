---
title: "/doc | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/doc 编译器选项 [Visual Basic]"
  - "doc 编译器选项 [Visual Basic]"
  - "-doc 编译器选项 [Visual Basic]"
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /doc
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将文档注释处理到一个 XML 文件中。  
  
## 语法  
  
```  
/doc[+ | -]  
' -or-  
/doc:file  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`+`  &#124; `-`|可选。  指定“\+”或只指定 `/doc`，让编译器生成文档信息，并将这些信息放入一个 XML 文件中。  指定 `-`  相当于不指定 `/doc`，不会创建任何文档信息。|  
|`file`|如果使用了 `/doc:`，则是必选项。  指定输出的 XML 文件，文件将包括被编译的源代码文件中的注释。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。|  
  
## 备注  
 `/doc` 选项控制编译器是否生成包含文档注释的 XML 文件。  如果您使用 `/doc:``file` 语法，则由 `file` 参数指定 XML 文件的名称。  如果使用 `/doc` 或 `/doc+`，编译器则根据该编译器正创建的可执行文件或库使用一个 XML 文件名。  如果使用 `/doc-` 或不指定 `/doc` 选项，则编译器不创建 XML 文件。  
  
 在源代码文件中，文档注释可以位于下面的定义之前：  
  
-   用户定义类型，例如[类](../../../visual-basic/language-reference/statements/class-statement.md)或[接口](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   成员，例如字段、[事件](../../../visual-basic/language-reference/statements/event-statement.md)、[属性](../../../visual-basic/language-reference/statements/property-statement.md)、[函数](../../../visual-basic/language-reference/statements/function-statement.md)或[子例程](../../../visual-basic/language-reference/statements/sub-statement.md)。  
  
 若要使用以 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] [IntelliSense](/visual-studio/ide/using-intellisense) 功能生成的 XML 文件，让 XML 文件的文件名与您要支持的程序集相同。  确保 XML 文件与程序集位于同一个目录中，从而在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 项目中引用程序集时，也可以找到 .xml 文件。  要让 IntelliSense 对项目中的代码或被一个项目引用的多个项目中的代码有效，XML 文档文件不是必选项。  
  
 如果不用 `/target:module` 编译，则 XML 文件包含标记 `<assembly></assembly>`。  这些标记为编译的输出文件指定包含程序集清单的文件名。  
  
 有关根据代码中的注释生成文档的方法，请参见 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/doc|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  设置**“生成 XML 文档文件”**框中的值。|  
  
## 示例  
 有关示例，请参见 [使用 XML 将代码文档化](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [使用 XML 将代码文档化](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)