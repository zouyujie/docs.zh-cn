---
title: "&lt;exception&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "exception"
  - "<exception>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<exception> C# XML 标记"
  - "exception C# XML 标记"
ms.assetid: dd73aac5-3c74-4fcf-9498-f11bff3a2f3c
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# &lt;exception&gt;（C# 编程指南）
## 语法  
  
```  
<exception cref="member">description</exception>  
```  
  
#### 参数  
 cref \= "`member`"  
 对可从当前编译环境中获取的异常的引用。  编译器检查到给定异常存在后，将 `member` 转换为输出 XML 中的规范化元素名称。  `member` 必须位于双引号 \(" "\) 中。  
  
 有关如何创建对泛型类型的 cref 引用的更多信息，请参见 [\<see\>](../../../csharp/programming-guide/xmldoc/see.md)。  
  
 `description`  
 异常说明。  
  
## 备注  
 \<exception\> 标记使您可以指定哪些异常可被引发。  此标记可用在方法、属性、事件和索引器的定义中。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
 有关异常处理的更多信息，请参见[异常和异常处理](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#4](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/exception_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)