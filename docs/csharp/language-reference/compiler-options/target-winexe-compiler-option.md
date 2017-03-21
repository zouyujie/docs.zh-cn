---
title: "/target:winexe (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/target:winexe"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/target compiler options [C#], /target:winexe"
  - "-target compiler options [C#], /target:winexe"
  - "target compiler options [C#], /target:winexe"
ms.assetid: b5a0619c-8caa-46a5-a743-1cf68408ad7a
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# /target:winexe (C# Compiler Options)
**\/target:winexe** 选项使编译器创建可执行 \(EXE\) 的 Windows 程序。  
  
## 语法  
  
```  
/target:winexe  
```  
  
## 备注  
 将创建带扩展名 .exe 的可执行文件。  Windows 程序是一种由 .NET Framework 库或使用 Win32 API 提供一个用户界面的程序。  
  
 使用 [\/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md) 创建控制台应用程序。  
  
 除非另外使用 [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) 选项指定，否则输出文件名采用包含 [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md) 方法的输入文件名。  
  
 在命令行指定该选项时，直至下一个 **\/out** 或 [\/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 选项之前的所有文件都将用于创建 Windows 程序。  
  
 在编译到 .exe 文件中的源代码文件中要求有且仅有一个 **main** 方法。  [\/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) 选项使您可以在代码中包含多个具有 **main** 方法的类的情况下，指定包含 **main** 方法的类。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  修改**“输出类型”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## 示例  
 将 `in.cs` 编译成 Windows 程序：  
  
```  
csc /target:winexe in.cs  
```  
  
## 请参阅  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)