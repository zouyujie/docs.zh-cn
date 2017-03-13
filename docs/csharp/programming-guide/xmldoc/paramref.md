---
title: "&lt;paramref&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "paramref"
  - "<paramref>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<paramref> C# XML 标记"
  - "paramref C# XML 标记"
ms.assetid: 756c24c1-f591-40e8-a838-559761539b0b
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# &lt;paramref&gt;（C# 编程指南）
## 语法  
  
```  
<paramref name="name"/>  
```  
  
#### 参数  
 `name`  
 要引用的参数名。  将此名称用双引号括起来 \(" "\)。  
  
## 备注  
 \<paramref\> 标记提供了指示代码注释中的某个单词（例如在 \<summary\> 或 \<remarks\> 块中）引用某个参数的方式。  可以处理 XML 文件来以不同的方式格式化此单词，比如将其设置为粗体或斜体。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#7](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/paramref_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)