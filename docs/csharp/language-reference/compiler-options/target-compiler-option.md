---
title: "/target (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/target"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "target compiler options [C#]"
  - "/target compiler options [C#]"
  - "assemblies [C#], compiling"
  - "-target compiler options [C#]"
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /target (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/target** 编译器选项可以指定为以下四种形式之一：  
  
 [\/target:appcontainerexe](../Topic/-target:appcontainerexe%20\(C%23%20Compiler%20Options\).md)  
 创建 [!INCLUDE[win8_appname_long](../../../csharp/language-reference/compiler-options/includes/win8_appname_long_md.md)] 应用的 .exe 文件。  
  
 [\/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md)  
 创建 .exe 文件。  
  
 [\/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md)  
 创建代码库。  
  
 [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)  
 创建模块。  
  
 [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)  
 创建 Windows 程序。  
  
 [\/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)  
 创建一个 .winmdobj 中间文件。  
  
 如果不指定 **\/target:module**，**\/target** 会将 .NET Framework 程序集清单放入输出文件中。  有关更多信息，请参见[公共语言运行时中的程序集](../Topic/Assemblies%20in%20the%20Common%20Language%20Runtime.md)和[公共特性](../Topic/Common%20Attributes%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 程序集清单放置在编译中的第一个 .exe 输出文件中，如果没有 .exe 输出文件，会放置在第一个 DLL 中。  例如，在以下的命令行中，清单将放置在 `1.exe` 中：  
  
```  
csc /out:1.exe t1.cs /out:2.netmodule t2.cs  
```  
  
 编译器每次编译只创建一个程序集清单。  关于编译中所有文件的信息全放在程序集清单中。  除用 **\/target:module** 创建的文件之外，所有输出文件都可以包含程序集清单。  在命令行生成多个输出文件时，只能创建一个程序集清单，且必须放置在命令行上指定的第一个输出文件中。  无论第一个输出文件是什么（**\/target:exe**、**\/target:winexe**、**\/target:library** 或 **\/target:module**），在同一编译中生成的任何其他输出文件都必须是模块 \(**\/target:module**\)。  
  
 如果创建了一个程序集，则可以用 <xref:System.CLSCompliantAttribute> 特性指示全部或部分代码是符合 CLS 的。  
  
```  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 有关以编程方式设置此编译器选项的更多信息，请参见 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [\/subsystemversion \(Specify minimum subsystem version\)](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)