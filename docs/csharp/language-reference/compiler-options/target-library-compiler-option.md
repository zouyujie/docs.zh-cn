---
title: "/target:library (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/dll"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-target compiler options [C#], /target:library"
  - "target compiler options [C#], /target:library"
  - "/target compiler options [C#], /target:library"
ms.assetid: c5670e88-2126-47c1-8d1c-217923837d17
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# /target:library (C# Compiler Options)
**\/target:library** 选项使编译器创建一个动态链接库 \(DLL\) 而不是一个可执行文件 \(EXE\)。  
  
## 语法  
  
```  
/target:library  
```  
  
## 备注  
 DLL 创建后会带有 .dll 扩展名。  
  
 除非使用 [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) 选项另外指定，否则输出文件的名称采用第一个输入文件的名称。  
  
 在命令行上指定该选项时，下一个 **\/out** 或 **\/target:module** 选项之前的所有文件都将用于创建 .dll 文件。  
  
 生成 .dll 文件时，不需要 [main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md) 方法。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  修改**“输出类型”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## 示例  
 编译 `in.cs`，创建 `in.dll`：  
  
```  
csc /target:library in.cs  
```  
  
## 请参阅  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)