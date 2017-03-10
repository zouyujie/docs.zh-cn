---
title: "/target:exe (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/exe"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "target compiler options [C#], /target:exe"
  - "/target compiler options [C#], /target:exe"
  - "-target compiler options [C#], /target:exe"
ms.assetid: bda5717d-1b91-4848-956b-fcf85c30e432
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# /target:exe (C# Compiler Options)
**\/target:exe** 选项使编译器创建可执行 \(EXE\) 的控制台应用程序。  
  
## 语法  
  
```  
/target:exe  
```  
  
## 备注  
 默认情况下，**\/target:exe** 选项有效。  将创建带扩展名 .exe 的可执行文件。  
  
 使用 [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) 创建可执行的 Windows 程序。  
  
 除非另外使用 [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) 选项指定，否则输出文件名采用包含 [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md) 方法的输入文件名。  
  
 在命令行上指定该选项时，下一个 **\/out** 或 **\/target:module** 选项之前的所有文件都将用于创建 .exe 文件  
  
 在编译到 .exe 文件中的源代码文件中要求有且仅有一个 **main** 方法。  [\/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) 编译器选项使您可以在代码中包含多个具有 **main** 方法的类的情况下，指定包含 **main** 方法的类。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  修改**“输出类型”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## 示例  
 下列每个命令行都编译 `in.cs`，创建 `in.exe`：  
  
```  
csc /target:exe in.cs  
csc in.cs  
```  
  
## 请参阅  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)