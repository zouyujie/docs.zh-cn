---
title: "/netcf | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/netcf"
  - "netcf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/netcf 编译器选项 [Visual Basic]"
  - "netcf 编译器选项 [Visual Basic]"
  - "-netcf 编译器选项 [Visual Basic]"
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /netcf
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将编译器的编译目标设置为 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)]。  
  
## 语法  
  
```  
/netcf  
```  
  
## 备注  
 `/netcf` 选项使 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将编译目标设置为 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] 而不是完整的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)]。  只存在于完整的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 中的语言功能将被禁用。  
  
 `/netcf` 选项旨在与 [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md) 一起使用。  `/netcf` 所禁用的语言功能与用 `/sdkpath` 导向的文件中不存在的语言功能相同。  
  
> [!NOTE]
>  `/netcf` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  当加载 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 设备项目时，将设置 `/netcf` 选项。  
  
 `/netcf` 选项将更改以下语言功能：  
  
-   禁用可终止程序执行的 [End \<关键字\> 语句](../../../visual-basic/language-reference/statements/end-keyword-statement.md) 关键字。  下面的程序在没有使用 `/netcf` 时可以正常编译和运行，但在使用 `/netcf` 的情况下将会在编译时失败。  
  
     [!code-vb[VbVbalrCompiler#34](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/netcf_1.vb)]  
  
-   所有形式的后期绑定都会被禁用。  当遇到可识别的后期绑定情况时，将生成编译时错误。  下面的程序在没有使用 `/netcf` 时可以正常编译和运行，但在使用 `/netcf` 的情况下将会在编译时失败。  
  
     [!code-vb[VbVbalrCompiler#35](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/netcf_2.vb)]  
  
-   禁用 [Auto](../../../visual-basic/language-reference/modifiers/auto.md)、[Ansi](../../../visual-basic/language-reference/modifiers/ansi.md) 和 [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md) 修饰符。  [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md) 语句的语法也被修改为 `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]`。  下面的代码显示 `/netcf` 对编译的影响。  
  
     [!code-vb[VbVbalrCompiler#36](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/netcf_3.vb)]  
  
-   在使用 `/netcf` 时，如果使用已从 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中移除的 Visual Basic 6.0 关键字，将会生成一个不同的错误。  这将影响用于以下关键字的错误信息：  
  
    -   `Open`  
  
    -   `Close`  
  
    -   `Put`  
  
    -   `Print`  
  
    -   `Write`  
  
    -   `Input`  
  
    -   `Lock`  
  
    -   `Unlock`  
  
    -   `Seek`  
  
    -   `Width`  
  
    -   `Name`  
  
    -   `FreeFile`  
  
    -   `EOF`  
  
    -   `Loc`  
  
    -   `LOF`  
  
    -   `Line`  
  
## 示例  
 下面的代码使用 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] 编译 `Myfile.vb`，并使用 C 驱动器上 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] 的默认安装目录中的 Mscorlib.dll 版本和 Microsoft.VisualBasic.dll 版本。  通常，应该使用最新版 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)]。  
  
```  
vbc /netcf /sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)