---
title: "/doc (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "FileProperties.BuildAction"
  - "/doc"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "comments, C# code"
  - "XML documentation [C#], comments in source files"
  - "doc compiler option [C#]"
  - "Visual C#, XML documentation for"
  - "-doc compiler option [C#]"
  - "/doc compiler option [C#]"
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /doc (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/doc** 选项允许在 XML 文件中放置文档注释。  
  
## 语法  
  
```  
/doc:file  
```  
  
## 参数  
 `file`  
 XML 的输出文件，由编译的源代码文件中的注释填充。  
  
## 备注  
 在源代码文件中，可处理以下内容之前的文档注释，并将其添加到 XML 文件中：  
  
-   用户定义的类型，如 [class](../../../csharp/language-reference/keywords/class.md)、[delegate](../../../csharp/language-reference/keywords/delegate.md) 或 [interface](../../../csharp/language-reference/keywords/interface.md)  
  
-   成员，如字段、[事件](../../../csharp/language-reference/keywords/event.md)、[属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)或方法  
  
 包含 Main 的源代码文件首先输出到 XML。  
  
 若要将生成的 .xml 文件用于[Intellisense](/visual-studio/ide/using-intellisense)功能，请使该 .xml 文件的文件名与要支持的程序集同名，然后确保该 .xml 文件放入与该程序集相同的目录中。  这样，在 Visual Studio 项目中引用程序集时，也可找到该 .xml 文件。  有关更多信息，请参见[提供代码注释](/visual-studio/ide/supplying-xml-code-comments)。  
  
 除非用 [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) 进行编译，否则 `file` 将包含 \<assembly\>\<\/assembly\>，以指定包含编译输出文件的程序集清单的文件名。  
  
> [!NOTE]
>  \/doc 选项适用于所有输入文件；或者，如果此选项是在“项目设置”中设置的，则适用于项目中的所有文件。  若要禁用与特定的文件或代码段的文档注释相关的警告，请使用 [\#pragma warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md)。  
  
 有关从代码中的注释生成文档的方法，请参见[建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**选项卡。  
  
3.  修改**“XML 文档文件”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)