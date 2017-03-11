---
title: "建议的文档注释标记（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "XML [C#]，标记"
  - "XML 文档 [C#]，标记"
ms.assetid: 6e98f7a9-38f4-4d74-b644-1ff1b23320fd
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# 建议的文档注释标记（C# 编程指南）
C\# 编译器处理代码中的文档注释，将它们设置为 XML 文件格式，其文件名在 **\/doc** 命令行选项中指定。  若要创建基于编译器生成的文件的最终文档，您可以创建自定义工具，也可以使用诸如等工具 [约定](http://shfb.codeplex.com/)。  
  
 在代码构造（如类型和类型成员）上处理标记。  
  
> [!NOTE]
>  文档注释不能应用于命名空间。  
  
 编译器将处理任何为有效 XML 的标记。  下列标记提供了用户文档中常用的功能。  
  
## 标记  
  
||||  
|-|-|-|  
|[\<c\>](../../../csharp/programming-guide/xmldoc/code-inline.md)|[\<para\>](../../../csharp/programming-guide/xmldoc/para.md)|[\<see\>](../../../csharp/programming-guide/xmldoc/see.md)\*|  
|[\<code\>](../../../csharp/programming-guide/xmldoc/code.md)|[\<param\>](../../../csharp/programming-guide/xmldoc/param.md)\*|[\<seealso\>](../../../csharp/programming-guide/xmldoc/seealso.md)\*|  
|[\<example\>](../../../csharp/programming-guide/xmldoc/example.md)|[\<paramref\>](../../../csharp/programming-guide/xmldoc/paramref.md)|[\<summary\>](../../../csharp/programming-guide/xmldoc/summary.md)|  
|[\<exception\>](../../../csharp/programming-guide/xmldoc/exception.md)\*|[\<permission\>](../../../csharp/programming-guide/xmldoc/permission.md)\*|[\<typeparam\>](../../../csharp/programming-guide/xmldoc/typeparam.md)\*|  
|[\<include\>](../../../csharp/programming-guide/xmldoc/include.md)\*|[\<remarks\>](../../../csharp/programming-guide/xmldoc/remarks.md)|[\<typeparamref\>](../../../csharp/programming-guide/xmldoc/typeparamref.md)|  
|[\<list\>](../../../csharp/programming-guide/xmldoc/list.md)|[\<returns\>](../../../csharp/programming-guide/xmldoc/returns.md)|[\<value\>](../../../csharp/programming-guide/xmldoc/value.md)|  
  
 （\* 表示编译器验证语法。）  
  
 如果想要尖括号出现在文档注释文本中，使用 `<` 和 `>`。如下面示例所示。  
  
```xml  
/// <summary cref="C < T >">  
/// </summary>  
```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [\/doc \(Process Documentation Comments\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)