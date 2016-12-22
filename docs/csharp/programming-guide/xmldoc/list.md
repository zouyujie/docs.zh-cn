---
title: "&lt;list&gt;（C# 编程指南） | Microsoft Docs"
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
  - "list"
  - "<list>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<item> C# XML 标记"
  - "<list> C# XML 标记"
  - "<listheader> C# XML 标记"
  - "item C# XML 标记"
  - "list C# XML 标记"
  - "listheader C# XML 标记"
ms.assetid: c9620b1b-c2e6-43f1-ab88-8ab47308ffec
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;list&gt;（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## 语法  
  
```  
<list type="bullet" | "number" | "table">  
    <listheader>  
        <term>term</term>  
        <description>description</description>  
    </listheader>  
    <item>  
        <term>term</term>  
        <description>description</description>  
    </item>  
</list>  
```  
  
#### 参数  
 `term`  
 要定义的项，该项将在 `description` 中定义。  
  
 `description`  
 项目符号列表或编号列表中的项或者 `term` 的定义。  
  
## 备注  
 \<listheader\> 块用于定义表或定义列表中的标题行。  定义表时，只需为标题中的项提供一个项。  
  
 列表中的每一项都用一个 \<item\> 块来描述。  创建定义列表时，既需要指定 `term` 也需要指定 `description`。  但是，对于表、项目符号列表或编号列表，只需为 `description` 提供一个项。  
  
 列表或表所拥有的 \<item\> 块数可以根据需要而定。  
  
 使用 [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 [!code-cs[csProgGuideDocComments#6](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/list_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)