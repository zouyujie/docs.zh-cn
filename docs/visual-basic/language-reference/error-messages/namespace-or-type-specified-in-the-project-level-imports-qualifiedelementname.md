---
title: "在项目级 Imports“&lt;限定元素名&gt;”中指定的命名空间或类型不包含任何公共成员，或者找不到该命名空间或类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40057"
  - "bc40057"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40057"
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 在项目级 Imports“&lt;限定元素名&gt;”中指定的命名空间或类型不包含任何公共成员，或者找不到该命名空间或类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

项目级导入“\<qualifiedelementname\>”中指定的命名空间或类型不包含任何公共成员，或无法找到该命名空间或类型。请确保已定义命名空间或类型，且其中至少包含一个公共成员。请确保别名中不包含其他别名。  
  
 项目的导入属性所指定的包含元素无法被找到，或没有定义任何 `Public` 成员。  
  
 *“包含元素”*可以是命名空间、类、结构、模块、接口或枚举。  包含元素可包含成员，如变量、过程或其他包含元素。  
  
 导入的目的是允许代码访问命名空间或类型成员，而无须对它们进行限定。  项目还可能需要添加对命名空间或类型的引用。  有关更多信息，请参见 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md) 中的“导入包含元素”。  
  
 如果编译器无法找到指定的包含元素，则无法解析使用该包含元素的引用。  如果编译器找到的元素没有公开任何 `Public` 成员，则引用将不会成功。  在这两种情况下，导入元素是没有意义的。  
  
 使用**“项目设计器”**可指定要导入的元素。  使用**“引用”**页面的**“导入的命名空间”**节。  双击**“解决方案资源管理器”**中的**“我的项目”**图标，可以转到**“项目设计器”**。  
  
 **错误 ID：**BC40057  
  
### 更正此错误  
  
1.  打开**“项目设计器”**，然后切换到**“引用”**页面。  
  
2.  在**“导入的命名空间”**节中，验证是否可从项目中访问包含元素。  
  
3.  验证包含元素是否至少公开了一个 `Public` 成员。  
  
## 请参阅  
 [项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)