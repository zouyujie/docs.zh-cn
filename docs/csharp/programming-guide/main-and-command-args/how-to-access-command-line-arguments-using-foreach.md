---
title: "如何：使用 foreach 访问命令行参数（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "命令行参数 [C#]"
ms.assetid: 89c3e335-3f5b-4e24-8c5a-b8036561fe8a
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：使用 foreach 访问命令行参数（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

循环访问数组的另一种方法是使用 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 语句，如下面的示例所示。  `foreach` 语句可以用于循环访问数组、.NET Framework 集合类或任何实现 <xref:System.Collections.IEnumerable> 接口的类或结构。  
  
> [!NOTE]
>  在 Visual Studio 中运行应用程序时，可以在[“项目设计器”\-\>“调试”页](/visual-studio/ide/reference/debug-page-project-designer)中指定命令行参数。  
  
## 示例  
 下面的示例演示如何使用 `foreach` 输出命令行参数。  
  
 [!code-cs[csProgGuideMain#10](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-access-command-line-arguments-using-foreach_1.cs)]  
  
 [!code-cs[csProgGuideMain#11](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-access-command-line-arguments-using-foreach_2.cs)]  
  
## 请参阅  
 <xref:System.Array>   
 <xref:System.Collections>   
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [foreach，in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Main\(\) 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [如何：显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Main\(\) 返回值](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)