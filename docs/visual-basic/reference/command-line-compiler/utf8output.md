---
title: "/utf8output (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/utf8output 编译器选项 [Visual Basic]"
  - "utf8output 编译器选项 [Visual Basic]"
  - "-utf8output 编译器选项 [Visual Basic]"
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /utf8output (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用 UTF\-8 编码显示编译器输出。  
  
## 语法  
  
```  
/utf8output[+ | -]  
```  
  
## 参数  
 `+` &#124; `-`  
 可选。  该选项的默认设置为 `/utf8output-`，它表示编译器输出不使用 UTF\-8 编码。  指定 `/utf8output` 与指定 `/utf8output+` 的作用相同。  
  
## 备注  
 在某些国际配置中，编译器输出无法在控制台上正确显示。  在这种情况下，请使用 `/utf8output` 并将编译器输出重定向到一个文件中。  
  
> [!NOTE]
>  `/utf8output` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译 `In.vb` 并指示编译器使用 UTF\-8 编码显示输出。  
  
```  
vbc /utf8output in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)