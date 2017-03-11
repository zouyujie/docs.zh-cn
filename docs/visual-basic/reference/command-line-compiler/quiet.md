---
title: "/quiet | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/quiet"
  - "quiet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/quiet 编译器选项 [Visual Basic]"
  - "quiet 编译器选项 [Visual Basic]"
  - "-quiet 编译器选项 [Visual Basic]"
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# /quiet
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

防止编译器针对与语法相关的错误和警告显示代码。  
  
## 语法  
  
```  
/quiet  
```  
  
## 备注  
 默认情况下，`/quiet` 不起作用。  当编译器报告与语法有关的错误或警告时，还会输出源代码中的代码行。  对于分析编译器输出的应用程序，使编译器只输出诊断文本可能会是一种更方便的方法。  
  
 在下面的示例中，如果在没有 `/quiet` 的情况下进行编译，`Module1` 在输出错误的同时还将输出源代码。  
  
```  
Module Module1  
    Sub Main()  
        x()  
    End Sub  
End Module  
```  
  
 输出：  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
 `x`  
  
 `~`  
  
 如果使用 `/quiet` 进行编译，则编译器只输出如下内容：  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
> [!NOTE]
>  `/quiet` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译 `T2.vb`，并且不显示与语法有关的编译器诊断的代码：  
  
```  
vbc /quiet t2.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)