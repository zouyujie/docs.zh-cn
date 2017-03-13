---
title: "&lt;include&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "include"
  - "<include>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<include> C# XML 标记"
  - "include C# XML 标记"
ms.assetid: a8a70302-6196-4643-bd09-ef33f411f18f
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# &lt;include&gt;（C# 编程指南）
## 语法  
  
```  
<include file='filename' path='tagpath[@name="id"]' />  
```  
  
#### 参数  
 `filename`  
 包含文档的 XML 文件的名称。  该文件名可用路径加以限定。  将 `filename` 括在单引号 \(' '\) 中。  
  
 `tagpath`  
 `filename` 中指向标记 `name` 的标记路径。  将此路径括在单引号中 \(' '\)。  
  
 `name`  
 注释前边的标记中的名称说明符；`name` 具有一个 `id`。  
  
 `id`  
 位于注释之前的标记的 ID。  将此 ID 括在双引号中 \(" "\)。  
  
## 备注  
 \<include\> 标记使您得以引用描述源代码中类型和成员的另一文件中的注释。  这是除了将文档注释直接置于源代码文件中之外的另一种可选方法。  通过将文档放在单独文件中，您可以独立于源代码将源控件应用至文档。  其中一人可以签出源代码文件，而其他人则可以签出文档文件。  
  
 \<include\> 标记使用 XML XPath 语法。  有关自定义 \<include\> 使用的方法，请参见 XPath 文档。  
  
## 示例  
 以下是一个多文件示例。  第一个文件使用 \<include\>，如下所列：  
  
 [!code-cs[csProgGuideDocComments#5](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/include_1.cs)]  
  
 第二个文件 xml\_include\_tag.doc 包含下列文档注释：  
  
```  
<MyDocs>  
  
<MyMembers name="test">  
<summary>  
The summary for this type.  
</summary>  
</MyMembers>  
  
<MyMembers name="test2">  
<summary>  
The summary for this other type.  
</summary>  
</MyMembers>  
  
</MyDocs>  
```  
  
## 程序输出  
 以下输出在使用命令行 `/doc:DocFileName.xml.` 编译 Test 和 Test2 类时生成。在 Visual Studio 中，可以在项目设计器的“生成”窗格中指定 XML 文档注释选项。  C\# 编译器找到 \<inclue\> 标记时，将在 xml\_include\_tag.doc 中搜索文档注释，而不是在当前源文件中搜索。  然后，编译器生成 DocFileName.xml，这是由文档工具（如 [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061)）使用以生成最终文档的文件。  
  
```  
<?xml version="1.0"?>   
<doc>   
    <assembly>   
        <name>xml_include_tag</name>   
    </assembly>   
    <members>   
        <member name="T:Test">   
            <summary>   
The summary for this type.   
</summary>   
        </member>   
        <member name="T:Test2">   
            <summary>   
The summary for this other type.   
</summary>   
        </member>   
    </members>   
</doc>   
```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)