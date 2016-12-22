---
title: "未定义 Sub 或 Function (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrID35"
dev_langs: 
  - "VB"
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 未定义 Sub 或 Function (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`Sub` 或 `Function` 必须先定义才能调用。  此错误的可能原因包括：  
  
-   过程名称拼写错误。  
  
-   尝试调用另一个项目中的过程，但未在**“引用”**对话框中明确添加对该项目的引用。  
  
-   指定了一个调用过程不可见的过程。  
  
-   声明了一个未在指定库或代码资源中的 Windows 动态链接库 \(DLL\) 例程或 Macintosh 代码资源例程。  
  
### 更正此错误  
  
1.  确保过程名称拼写正确。  
  
2.  在**“引用”**对话框中查找要调用的过程所在项目的名称。  如果未显示，则单击**“浏览”**按钮进行搜索。  选中项目名称左侧的复选框，然后单击**“确定”**。  
  
3.  检查例程的名称。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)