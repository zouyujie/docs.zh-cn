---
title: "/nologo (Visual Basic) | Microsoft Docs"
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
  - "/nologo 编译器选项 [Visual Basic]"
  - "标志, 取消显示启动"
  - "nologo 编译器选项 [Visual Basic]"
  - "-nologo 编译器选项 [Visual Basic]"
ms.assetid: 25ef54b6-d676-4639-a2d2-a747a158bc07
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /nologo (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

编译过程中禁止显示版权标志和通知消息。  
  
## 语法  
  
```  
/nologo  
```  
  
## 备注  
 如果指定 `/nologo`，则编译器将不显示版权标志。  默认情况下，`/nologo` 不生效。  
  
> [!NOTE]
>  `/nologo` 选项不能在 Visual Studio 开发环境内部使用，它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译 `T2.vb` 并且不显示版权标志。  
  
```  
vbc /nologo t2.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)