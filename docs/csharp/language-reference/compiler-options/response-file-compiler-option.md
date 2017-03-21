---
title: "@ (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "@"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "response files, specifying for compilation [C#]"
  - "@ compiler option"
ms.assetid: dda4fa9f-a02c-400f-8b6a-d58834e13d7f
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# @ (C# Compiler Options)
@ 选项使您可以指定包含编译器选项和要编译的源代码文件的文件。  
  
## 语法  
  
```  
@response_file  
```  
  
## 参数  
 `response_file`  
 一个列出编译器选项或要编译的源代码文件的文件。  
  
## 备注  
 编译器在处理编译器选项和源代码文件时将它们视为是在命令行上指定的。  
  
 若要在一次编译中指定多个响应文件，请指定多个响应文件选项。  例如：  
  
```  
@file1.rsp @file2.rsp  
```  
  
 在响应文件中，多个编译器选项和源代码文件可以出现在同一行中。  单个编译器选项的指定必须出现在同一行中（不能跨行）。  响应文件可以带有以 \# 符号开始的注释。  
  
 从响应文件内部指定编译器选项就如同在命令行发出这些命令。  有关更多信息，请参见[从命令行生成](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)。  
  
 编译器在遇到命令选项时会进行处理。  因此，命令行参数可以重写先前在响应文件中列出的选项。  反之，响应文件中的选项也将重写先前在命令行或其他响应文件中列出的选项。  
  
 C\# 提供 csc.rsp 文件，该文件与 csc.exe 文件位于同一目录中。  有关 csc.rsp 的更多信息，请参见 [\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)。  
  
 不能在 Visual Studio 开发环境中设置此编译器选项，也不能以编程方式对其进行更改。  
  
## 示例  
 以下几行来自一个示例响应文件：  
  
```  
# build the first output file  
/target:exe /out:MyExe.exe source1.cs source2.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)