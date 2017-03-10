---
title: "需要引用包含类型“&lt;typename&gt;”的程序集“&lt;assemblyidentity&gt;”，但由于项目“&lt;projectname1&gt;”和“&lt;projectname2&gt;”之间存在二义性，无法找到合适的引用 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30969"
  - "vbc30969"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30969"
ms.assetid: 1b29dbc5-8268-45fe-bfc2-b2070a5c845c
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 需要引用包含类型“&lt;typename&gt;”的程序集“&lt;assemblyidentity&gt;”，但由于项目“&lt;projectname1&gt;”和“&lt;projectname2&gt;”之间存在二义性，无法找到合适的引用
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

表达式使用在项目外部定义的类型，如类、结构、接口、枚举或委托。 但是，你具有对定义该类型的多个程序集的项目引用。  
  
 引用的项目会生成名称相同的程序集。 因此，编译器无法确定对要访问的类型使用哪一个程序集。  
  
 若要访问另一个程序集中定义的类型，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器必须具有对该程序集的引用。 此引用必须单一、明确，不会导致项目之间循环引用。  
  
 **错误 ID：**BC30969  
  
### 更正此错误  
  
1.  确定产生最佳程序集引用的项目。 为便于确定，你可以使用文件访问轻松程度和更新频率等条件。  
  
2.  在项目属性中，添加对包含某程序集的文件的引用，该程序集定义正在使用的类型。  
  
## 请参阅  
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [有关无效的引用的疑难解答](/visual-studio/ide/troubleshooting-broken-references)