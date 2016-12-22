---
title: "编译器错误 CS0576 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0576"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0576"
ms.assetid: c409f8ba-4a59-48d3-9bd8-4e9053219875
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0576
命名空间“namespace”包含与别名“identifier”冲突的定义  
  
 尝试两次使用同一个命名空间。  
  
## 示例  
 以下示例生成 CS0576：  
  
```  
// CS0576.cs using SysIO = System.IO; public class SysIO { public void MyMethod() {} } public class Test { public static void Main() { SysIO.Stream s;   // CS0576 } }  
```