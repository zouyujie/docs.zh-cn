---
title: "/help，/?(Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/?编译器选项 [Visual Basic]"
  - "/help 编译器选项 [Visual Basic]"
  - "? 编译器选项 [Visual Basic]"
  - "-?编译器选项 [Visual Basic]"
  - "help 编译器选项 [Visual Basic]"
  - "-help 编译器选项 [Visual Basic]"
ms.assetid: eb984aa5-ac98-4d0b-a0d2-24238d7bc8dc
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# /help，/?(Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

显示编译器选项。  
  
## 语法  
  
```  
/help  
' -or-  
/?  
```  
  
## 备注  
 如果在编译中包括了该选项，则不会创建输出任何文件，并且不进行编译。  
  
> [!NOTE]
>  `/help` 选项不能在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码从命令行显示帮助：  
  
```  
vbc /help  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)