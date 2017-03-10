---
title: "&lt;typeparam&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "typeparam"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<typeparam> C# XML 标记"
  - "typeparam C# XML 标记"
ms.assetid: 9b99d400-e911-4e55-99c6-64367c96aa4f
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# &lt;typeparam&gt;（C# 编程指南）
## 语法  
  
```  
<typeparam name="name">description</typeparam>  
```  
  
#### 参数  
 `name`  
 类型参数的名称。  将此名称用双引号括起来 \(" "\)。  
  
 `description`  
 类型参数的说明。  
  
## 备注  
 在泛型类型或方法声明的注释中应该使用 `<typeparam>` 标记描述类型参数。  为泛型类型或方法的每个类型参数添加标记。  
  
 有关更多信息，请参见 [泛型](../../../csharp/programming-guide/generics/index.md)。  
  
 `<typeparam>` 标记的文本将显示在 [Object Browser Window](http://msdn.microsoft.com/zh-cn/3c7f1673-1f0d-41b1-94ca-a3dcfcb82cda)代码注释 Web 报表的 IntelliSense 中。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#13](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/typeparam_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)