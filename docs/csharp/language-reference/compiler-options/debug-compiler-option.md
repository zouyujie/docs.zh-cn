---
title: "/debug (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/debug"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "debug compiler option [C#]"
  - "-debug compiler option [C#]"
  - "/debug compiler option [C#]"
ms.assetid: e2b48c07-01bc-45cc-a52c-92e9085eb969
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# /debug (C# Compiler Options)
**\/debug** 选项使编译器生成调试信息并将其放置在一个或多个输出文件中。  
  
## 语法  
  
```  
/debug[+ | -]  
/debug:{full | pdbonly}  
```  
  
## 参数  
 `+` &#124; `-`  
 指定 `+` 或只指定 **\/debug** 将使编译器生成调试信息，并将这些信息放置在一个程序数据库（.pdb 文件）中。  指定 `-`（在不指定 **\/debug** 时有效）将导致不创建任何调试信息。  
  
 `full` &#124; `pdbonly`  
 指定编译器生成的调试信息类型。  full 参数在没有指定 **\/debug:pdbonly** 时有效，它允许将调试器附加到正在运行的程序。  指定 pdbonly 允许在调试器中启动程序时进行源代码调试，但仅在正在运行的程序附加到调试器时才显示汇编程序。  
  
## 备注  
 使用该选项创建调试版本。  如果未指定 **\/debug**、**\/debug\+** 或 **\/debug:full**，则无法调试程序的输出文件。  
  
 如果使用 **\/debug:full**，请注意 **\/debug:full** 可能会对 JIT 优化代码的速度和大小有一些影响，并且可能会稍微影响代码质量。  我们建议在生成发布代码时使用 **\/debug:pdbonly** 或不使用 PDB。  
  
> [!NOTE]
>  **\/debug:pdbonly** 和 **\/debug:full** 的一个区别是：使用 **\/debug:full** 时，编译器会发出 <xref:System.Diagnostics.DebuggableAttribute>，用于通知 JIT 编译器有可用的调试信息。  因此，如果使用 **\/debug:full**，而代码中包含设置为 false 的 <xref:System.Diagnostics.DebuggableAttribute>，则会发生错误。  
  
 有关如何配置应用程序的调试性能的信息，请参见[使映像更易于调试](../Topic/Making%20an%20Image%20Easier%20to%20Debug.md)。  
  
 若要更改 .pdb 文件的位置，请参见 [\/pdb \(Specify Debug Symbol File\)](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  单击**“高级”**按钮。  
  
4.  修改**“调试信息”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DebugSymbols%2A>。  
  
## 示例  
 将调试信息放置在输出文件 `app.pdb` 中：  
  
```  
csc /debug /pdb:app.pdb test.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)