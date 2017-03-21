---
title: "/vbruntime | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbruntime"
  - "/vbruntime"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/vbruntime 编译器选项 [Visual Basic]"
  - "vbruntime 编译器选项 [Visual Basic]"
  - "-vbruntime 编译器选项 [Visual Basic]"
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /vbruntime
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定编译器是应该在不引用 Visual Basic 运行库的情况下进行编译，还是在引用特定运行库的情况下进行编译。  
  
## 语法  
  
```  
/vbruntime:{ - | + | * | path }  
```  
  
## 参数  
 \-  
 在不引用 Visual Basic 运行库的情况下进行编译。  
  
 \+  
 引用默认的 Visual Basic 运行库进行编译。  
  
 \*  
 在不引用 Visual Basic 运行库的情况下编译，并将核心功能从 Visual Basic 运行库嵌入程序集。  
  
 `path`  
 引用指定的库 \(DLL\) 进行编译。  
  
## 备注  
 使用 `/vbruntime` 编译器选项，您可以指定编译器是否应在不引用 Visual Basic 运行库的情况下进行编译。  如果在不引用 Visual Basic 运行库的情况下进行编译，则会对调用 Visual Basic 运行时帮助器的代码或语言构造记录错误或警告。  （“Visual Basic 运行时帮助器”是在 Microsoft.VisualBasic.dll 中定义的一个函数，在运行时调用以执行特定的语言语义。）  
  
 `/vbruntime+` 选项作用下的行为与未指定 `/vbruntime` 开关时的行为相同。  可以使用 `/vbruntime+` 选项重写之前的 `/vbruntime` 开关。  
  
 ，当您使用 `/vbruntime-` 或 `vbruntime:``path` 选项时， `My` 类型的大多数对象不可用。  
  
## 嵌入 Visual Basic 运行时核心功能  
 `/vbruntime*` 通过此选项您可以在不引用运行库的情况下进行编译。  而是，在用户程序集中嵌入 Visual Basic 运行库中的核心功能。  可以使用此选项，如果应用程序在不包含 Visual Basic 运行时的平台上运行。  
  
 以下运行时成员均是嵌入式运行时成员：  
  
-   <xref:Microsoft.VisualBasic.CompilerServices.Conversions> 类  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29> 方法  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29> 方法  
  
-   <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29> 方法  
  
-   <xref:Microsoft.VisualBasic.Constants.vbBack> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCr> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCrLf> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbFormFeed> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbLf> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNewLine> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullChar> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullString> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbTab> 常数  
  
-   <xref:Microsoft.VisualBasic.Constants.vbVerticalTab> 常数  
  
-   `My` 类型的对象  
  
 如果您使用 `/vbruntime*` 选项编译，并且您的代码引用未使用核心功能嵌入的 Visual Basic 运行库中的成员，则编译器将返回错误，指示该成员不可用。  
  
## 引用指定的库  
 您可以使用 `path` 参数，通过引用自定义运行库而不是默认的 Visual Basic 运行库进行编译。  
  
 如果 `path` 参数的值是 DLL 的完全限定路径，则编译器将使用该文件作为运行库。  如果 `path` 参数的值不是 DLL 的完全限定路径，则 Visual Basic 编译器将首先在当前文件夹中搜索所标识的 DLL。  然后，在使用 [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md) 编译器选项指定的路径中进行搜索。  如果未使用 `/sdkpath` 编译器选项，则编译器将在 .NET Framework 文件夹 \(`%systemroot%\Microsoft.NET\Framework\versionNumber`\) 中搜索所标识的 DLL。  
  
## 示例  
 下面的示例演示如何使用 `/vbruntime` 选项来引用自定义库进行编译。  
  
```  
vbc /vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## 请参阅  
 [Visual Basic 核心 – Visual Studio 2010 SP1 中的新编译模式](http://blogs.msdn.com/b/vbteam/archive/2011/01/10/vb-core-new-compilation-mode-in-visual-studio-2010-sp1.aspx)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)