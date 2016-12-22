---
title: "文档标记的分隔符（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "用于 C# 文档标记的 /** */ 分隔符"
  - "用于 C# 文档的 /// 分隔符"
  - "XML [C#], 分隔符"
ms.assetid: 9b2bdd18-4f5c-4c0b-988e-fb992e0d233e
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 文档标记的分隔符（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用 XML doc 注释需要分隔符，分隔符为编译器指示文档注释的起止位置。  XML 文档标记可以与以下几种分隔符一起使用：  
  
 `///`  
 单行分隔符。  这是显示在文档示例中并由 Visual C\# 项目模板使用的形式。  如果有后接分隔符的空白字符，则此字符将不包括在 XML 输出中。  
  
> [!NOTE]
>  Visual Studio IDE 具有一项称为“智能注释编辑”的功能，它自动插入 \<summary\> 和 \<\/summary\> 标记，并且当您在代码编辑器中键入 `///` 分隔符后将光标移动到这些标记内。  从项目属性页的 [选项、文本编辑器、C\#、格式设置](/visual-studio/ide/reference/options-text-editor-csharp-formatting) 可以访问此功能。  
  
 `/** */`  
 多行分隔符。  
  
 以下是使用 `/** */` 分隔符时要遵循的一些格式设置规则：  
  
-   对于包含 `/**`  分隔符的行，如果该行的其余部分为空白，则不将该行处理为注释。  如果 `/**`  分隔符后面的第一个字符为空白，则忽略此空白字符并处理该行的剩余部分。  否则，将 `/**` 分隔符后的整行文本处理为注释的一部分。  
  
-   对于包含 `*/`  分隔符的行，如果到 `*/` 分隔符为止仅有空白，则忽略该行。  否则，将到 `*/` 分隔符为止的那行文本处理为注释的一部分，同时必须遵循以下描述的模式匹配规则。  
  
-   对于以 `/**` 分隔符开头的行后面的那些行，编译器会在每个行的开头寻找一个常用模式。  该模式可以包含可选的空白和一个星号 \(`*`\)，后跟多个可选的空白。  如果编译器在每行的开头找到不以 `/**` 分隔符或 `*/` 分隔符开头的常见模式，则它将忽略每行的该模式。  
  
 下面的示例阐释了这些规则。  
  
-   以下注释中将被处理的唯一部分是以 `<summary>` 开头的行。  这三个标记格式产生相同的注释。  
  
    ```  
    /** <summary>text</summary> */   
  
    /**   
    <summary>text</summary>   
    */   
  
    /**   
     * <summary>text</summary>   
    */  
  
    ```  
  
-   编译器在第二行和第三行的开头标识“\*”的常见模式。  该模式不包括在输出中。  
  
    ```  
    /**   
     * <summary>   
     * text </summary>*/   
    ```  
  
-   编译器在以下注释中找不到任何常见模式，因为第三行的第二个字符没有星号。  因此，第二行和第三行中的所有文本都将被处理为注释的一部分。  
  
    ```  
    /**   
     * <summary>   
       text </summary>  
    */   
    ```  
  
-   编译器之所以在此注释中没找到任何模式有以下两个原因。  首先，星号前的空格数并不一致。  其次，第五行是以 Tab 开头的，它并不等效于空格。  因此，从第二行到第五行的所有文本都将被处理为注释的一部分。  
  
    ```  
    /**   
      * <summary>   
      * text   
     *  text2   
        *  </summary>   
    */   
    ```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)   
 [\/doc \(Process Documentation Comments\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)