---
title: "如何：显示命令行参数（C# 编程指南） | Microsoft Docs"
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
  - "命令行参数 [C#], 显示"
ms.assetid: b8479f2d-9e05-4d38-82da-2e61246e5437
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：显示命令行参数（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以通过 `Main` 的可选参数来访问通过命令行提供给可执行文件的参数。  参数以字符串数组的形式提供。  数组的每个元素都包含一个参数。  参数之间的空白被移除。  例如，下面是对一个假想的可执行文件的命令行调用：  
  
|命令行输入|传递给 Main 的字符串数组|  
|-----------|---------------------|  
|**executable.exe a b c**|"a"<br /><br /> "b"<br /><br /> “c”|  
|**executable.exe one two**|"one"<br /><br /> "two"|  
|**executable.exe "one two" three**|"one two"<br /><br /> "three"|  
  
> [!NOTE]
>  在 Visual Studio 中运行应用程序时，可以在[“项目设计器”\-\>“调试”页](/visual-studio/ide/reference/debug-page-project-designer)中指定命令行参数。  
  
## 示例  
 本示例显示了传递给命令行应用程序的命令行参数。  显示的输出对应于上表中的第一项。  
  
 [!code-cs[csProgGuideMain#9](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-display-command-line-arguments_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Main\(\) 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [如何：使用 foreach 访问命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Main\(\) 返回值](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)