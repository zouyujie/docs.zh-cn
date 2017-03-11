---
title: "&lt;see&gt;（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<see>"
  - "see"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<see> C# XML 标记"
  - "cref [C#], <see> 标记"
  - "交叉引用 [C#]"
  - "see C# XML 标记"
ms.assetid: 0200de01-7e2f-45c4-9094-829d61236383
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# &lt;see&gt;（C# 编程指南）
## 语法  
  
```  
<see cref="member"/>  
```  
  
#### 参数  
 cref \= "`member`"  
 对可以通过当前编译环境进行调用的成员或字段的引用。  编译器检查给定的代码元素是否存在，并将 `member` 传递给输出 XML 中的元素名称。应将 *member* 放在双引号 \(" "\) 中。  
  
## 备注  
 \<see\> 标记使您得以从文本内指定链接。  使用 [\<seealso\>](../../../csharp/programming-guide/xmldoc/seealso.md) 指示文本应该放在“另请参见”节中。  用 [cref 特性](../../../csharp/programming-guide/xmldoc/cref-attribute.md)创建指向代码元素的文档页内部超链接。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
 下面的示例用一个摘要章节演示 \<see\> 标记。  
  
 [!code-cs[csProgGuideDocComments#12](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/see_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)