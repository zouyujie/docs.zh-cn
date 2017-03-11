---
title: "&lt;param&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "param"
  - "<param>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<param> C# XML 标记"
  - "param C# XML 标记"
ms.assetid: 46d329b1-5b84-4537-9e17-73ca97313e4e
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# &lt;param&gt;（C# 编程指南）
## 语法  
  
```  
<param name="name">description</param>  
```  
  
#### 参数  
 `name`  
 方法参数名。  将此名称用双引号括起来 \(" "\)。  
  
 `description`  
 参数说明。  
  
## 备注  
 \<param\> 标记应当用于方法声明的注释中，以描述方法的一个参数。  如要记录多个参数，请使用多个 \<param\> 标记。  
  
 有关 \<param\> 标记的文本将显示在 IntelliSense、对象浏览器和代码注释 Web 报表中。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#1](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/param_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)