---
title: "XML 文档注释（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.xml"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, XML 代码注释"
  - "C# 源代码文件"
  - "注释 [C#], XML"
  - "文档注释 [C#]"
  - "XML [C#], 代码注释"
  - "XML 文档注释 [C#]"
ms.assetid: 803b7f7b-7428-4725-b5db-9a6cff273199
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# XML 文档注释（C# 编程指南）
在 Visual C\# 中，你可以通过以下方式为代码创建文档：将特殊注释字段中的 XML 元素包含在源代码中注释引用的代码块的前面，例如：  
  
```  
/// <summary>  
///  This class performs an important function.  
/// </summary>  
public class MyClass{}  
```  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 选项进行编译时，编译器将在源代码中搜索所有 XML 标记，并创建一个 XML 文档文件。  若要基于编译器生成的文件创建最终文档，你可以创建一个自定义工具，也可以使用 [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061) 等工具。  
  
 若要引用 XML 元素（例如，你的函数将处理你要在 XML 文档注释中描述的特定 XML 元素），你可使用标准引用机制（`<` 和 `>`）。若要引用代码引用 \(`cref`\) 元素中的通用标识符，则可使用转义字符（例如，`cref=”List<T>”`）或大括号 \(`cref=”List{T}”`\)。作为特例，编译器会将大括号解析为尖括号以在引用通用标识符时使作者能够更轻松地进行文档注释。  
  
> [!NOTE]
>  XML 文档注释不是元数据；它们不包括在编译的程序集中，因此无法通过反射对其进行访问。  
  
## 本节内容  
  
-   [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)  
  
-   [处理 XML 文件](../../../csharp/programming-guide/xmldoc/processing-the-xml-file.md)  
  
-   [文档标记分隔符](../../../csharp/programming-guide/xmldoc/delimiters-for-documentation-tags.md)  
  
-   [如何：使用 XML 文档功能](../../../csharp/programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md)  
  
## 相关章节  
 有关详细信息，请参阅：  
  
-   [\/doc（处理文档注释）](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)