---
title: "&lt;seealso&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cref"
  - "<seealso>"
  - "seealso"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<seealso> C# XML 标记"
  - "cref [C#]"
  - "cref [C#], 请参见"
  - "交叉引用 [C#], 标记"
  - "seealso C# XML 标记"
ms.assetid: 8e157f3f-f220-4fcf-9010-88905b080b18
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# &lt;seealso&gt;（C# 编程指南）
## 语法  
  
```  
<seealso cref="member"/>  
```  
  
#### 参数  
 cref \= "`member`"  
 对可以通过当前编译环境进行调用的成员或字段的引用。  编译器检查到给定代码元素存在后，将 `member` 传递给输出 XML 中的元素名。必须将 `member` 括在双引号 \(" "\) 中。  
  
 有关如何创建对泛型类型的 cref 引用的信息，请参见 [\<see\>](../../../csharp/programming-guide/xmldoc/see.md)。  
  
## 备注  
 \<seealso\> 标记使您得以指定希望在“请参见”一节中出现的文本。  使用 [\<see\>](../../../csharp/programming-guide/xmldoc/see.md) 从文本内指定链接。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 有关使用 \<seealso\> 的示例，请参见 [\<summary\>](../../../csharp/programming-guide/xmldoc/summary.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)