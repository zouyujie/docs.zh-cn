---
title: "/recurse | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "/recurse 编译器选项 [Visual Basic]"
  - "recurse 编译器选项 [Visual Basic]"
  - "-recurse 编译器选项 [Visual Basic]"
ms.assetid: 84a0b670-33ae-44c4-a46a-b90388809317
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /recurse
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

编译指定目录或项目目录的所有子目录中的源代码文件。  
  
## 语法  
  
```  
/recurse:[dir\]file  
```  
  
## 参数  
 `dir`  
 可选。  搜索开始的目录。  如果不指定此参数，则会从项目目录中开始搜索。  
  
 `file`  
 必选。  要搜索的文件。  允许使用通配符字符。  
  
## 备注  
 可以在文件名中使用通配符来编译项目目录中所有匹配的文件，而不需使用 `/recurse`。  如果不指定输出文件名，编译器将基于处理的第一个输入文件来生成输出文件名。  如果按字母顺序来查看，这通常是已编译文件列表中的第一个文件。  因此，最好使用 `/out` 选项指定输出文件。  
  
> [!NOTE]
>  `/recurse` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译当前目录中的所有 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 文件。  
  
```  
vbc *.vb  
```  
  
 下面的代码编译 `Test\ABC` 目录以及其下任何目录中的所有 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 文件，然后生成 `Test.ABC.dll`。  
  
```  
vbc /target:library /out:Test.ABC.dll /recurse:Test\ABC\*.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/out](../../../visual-basic/reference/command-line-compiler/out.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)