---
title: "&lt;message&gt; 此错误也可能是由于将文件引用与程序集“&lt;assemblyname&gt;”的项目引用混合使用所造成的 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30971"
  - "vbc30971"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30971"
ms.assetid: 75d2e8b5-2fdc-4623-8b32-cba805dab7db
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;message&gt; 此错误也可能是由于将文件引用与程序集“&lt;assemblyname&gt;”的项目引用混合使用所造成的
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

\<message\> 此错误也可能是由于将文件引用与程序集“\<assemblyname\>”的项目引用混合使用所造成的。 在此情况下，请尝试将项目“\<projectname1\>”中的“\<assemblyfilename\>”的文件引用替换为“\<projectname2\>”的项目引用。  
  
 你项目中的代码访问了另一个项目的成员，但你的解决方案配置不允许使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器来解析引用。  
  
 若要访问另一个程序集中定义的类型，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器必须具有对该程序集的引用。 此引用必须单一、明确，不会导致项目之间循环引用。  
  
 **错误 ID：**BC30971  
  
### 更正此错误  
  
1.  确定产生最佳程序集引用的项目。 为便于确定，你可以使用文件访问轻松程度和更新频率等条件。  
  
2.  在项目属性中，添加对包含某程序集的项目的引用，该程序集定义正在使用的类型。  
  
## 请参阅  
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [有关无效的引用的疑难解答](/visual-studio/ide/troubleshooting-broken-references)