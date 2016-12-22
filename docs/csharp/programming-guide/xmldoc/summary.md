---
title: "&lt;summary&gt;（C# 编程指南） | Microsoft Docs"
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
  - "<summary>"
  - "summary"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<summary> C# XML 标记"
  - "summary C# XML 标记"
ms.assetid: b4c43d92-2067-4eac-a59a-d32f5248c08b
caps.latest.revision: 17
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;summary&gt;（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## 语法  
  
```  
<summary>description</summary>  
```  
  
#### 参数  
 `description`  
 对象的摘要。  
  
## 备注  
 \<summary\> 标记应当用于描述类型或类型成员。  使用 [\<remarks\>](../../../csharp/programming-guide/xmldoc/remarks.md) 添加针对某个类型说明的补充信息。  使用 [cref 特性](../../../csharp/programming-guide/xmldoc/cref-attribute.md)可启用文档工具（如 [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061)）来创建指向代码元素的文档页内部超链接。  
  
 \<summary\> 标记的文本是唯一有关 IntelliSense 中的类型的信息源，它也显示在 [Object Browser Window](http://msdn.microsoft.com/zh-cn/3c7f1673-1f0d-41b1-94ca-a3dcfcb82cda) 中。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  若要基于编译器生成的文件创建最终文档，可以创建一个自定义工具，也可以使用 [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061) 等工具。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#12](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_1.cs)]  
  
 前面的示例生成下面的 XML 文件。  
  
```  
<?xml version="1.0"?>  
<doc>  
    <assembly>  
        <name>YourNamespace</name>  
    </assembly>  
    <members>  
        <member name="T:DotNetEvents.TestClass">  
            text for class TestClass  
        </member>  
        <member name="M:DotNetEvents.TestClass.DoWork(System.Int32)">  
            <summary>DoWork is a method in the TestClass class.  
            <para>Here's how you could make a second paragraph in a description. <see cref="M:System.Console.WriteLine(System.String)"/> for information about output statements.</para>  
            <seealso cref="M:DotNetEvents.TestClass.Main"/>  
            </summary>  
        </member>  
        <member name="M:DotNetEvents.TestClass.Main">  
            text for Main  
        </member>  
    </members>  
</doc>  
```  
  
## 示例  
 下面的示例演示如何对泛型类型进行 `cref` 引用。  
  
 [!code-cs[csProgGuideDocComments#11](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_2.cs)]  
  
 前面的示例生成下面的 XML 文件。  
  
```  
<?xml version="1.0"?>  
<doc>  
    <assembly>  
        <name>YourNamespace</name>  
    </assembly>  
    <members>  
        <member name="T:ExtensionMethodsDemo1.A">  
            <summary cref="T:ExtensionMethodsDemo1.C`1">  
            </summary>  
        </member>  
        <member name="T:ExtensionMethodsDemo1.B">  
            <summary cref="T:C`1">  
            </summary>  
        </member>  
        <member name="T:ExtensionMethodsDemo1.C`1">  
            <summary cref="T:ExtensionMethodsDemo1.A">  
            </summary>  
            <typeparam name="T"></typeparam>  
        </member>  
    </members>  
</doc>  
  
```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)