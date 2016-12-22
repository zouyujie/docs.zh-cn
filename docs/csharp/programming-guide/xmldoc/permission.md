---
title: "&lt;permission&gt;（C# 编程指南） | Microsoft Docs"
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
  - "permission"
  - "<permission>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<permission> C# XML 标记"
  - "permission C# XML 标记"
ms.assetid: 769e93fe-8404-443f-bf99-577aa42b6a49
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;permission&gt;（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## 语法  
  
```  
<permission cref="member">description</permission>  
```  
  
#### 参数  
 cref \= "`member`"  
 对可以通过当前编译环境进行调用的成员或字段的引用。  编译器检查到给定代码元素存在后，将 `member` 转换为输出 XML 中的规范化元素名。必须将 *member* 括在双引号 \(" "\) 中。  
  
 有关如何创建对泛型类型的 cref 引用的信息，请参见 [\<see\>](../Topic/%3Csee%3E%20\(C%23%20Programming%20Guide\).md)。  
  
 `description`  
 对成员的访问的说明。  
  
## 备注  
 \<permission\> 标记使您得以将成员的访问记入文档。  使用 <xref:System.Security.PermissionSet> 类可以指定对成员的访问。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#8](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/permission_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)