---
title: "/platform (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/platform"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "platform compiler option [C#]"
  - "-platform compiler option [C#]"
  - "/platform compiler option [C#]"
ms.assetid: c290ff5e-47f4-4a85-9bb3-9c2525b0be04
caps.latest.revision: 46
caps.handback.revision: 46
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /platform (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定公共语言运行时 \(CLR\) 的哪个版本可以运行程序集。  
  
## 语法  
  
```  
/platform:string  
```  
  
#### 参数  
 `string`  
 anycpu\(默认值\)，anycpu32bitpreferred，ARM，x64，x86、或者Itanium。  
  
## 备注  
  
-   **anycpu**（默认值）将编译程序集为使其在任意平台上都可以运行。  在任何可能的时候，应用程序作为 64 位进程运行；仅当该模式只可用时，才会回退到 32 位。  
  
-   **anycpu32bitpreferred** 将程序集编译成可在任何平台上运行。  应用程序在支持 64 位和 32 位应用程序的系统以32 位模式运行。  可以仅仅为针对 .NET Framework 4.5 的项目指定此选项。  
  
-   **ARM**编译程序集，以便可以在具有高级 RISC \(ARM\) 计算机处理器的计算机运行。  
  
-   **x64** 将程序集编译成可由 64 位公共语言运行库在支持 AMD64 或 EM64T 指令集的计算机上运行。  
  
-   **x86**将程序集编译为由与 x86 兼容的 32 位公共语言运行时运行。  
  
-   **Itanium**将程序集编译为由采用 Itanium 处理器的计算机上的 64 位公共语言运行时运行。  
  
 在 64 位 Windows 操作系统上：  
  
-   用 **\/platform:x86** 编译的程序集将在运行于 WOW64 下的 32 位 CLR 上执行。  
  
-   用 **\/platform:anycpu** 编译的 DLL 将在加载该进程的同一 CLR 上执行。  
  
-   用 **\/platform:anycpu** 编译的可执行文件将在 64 位 CLR 上执行。  
  
-   用 **\/platform:anycpu32bitpreferred** 编译的可执行文件将在 32 位 CLR 上执行。  
  
 **anycpu32bitpreferred** 设置只对为可执行 \(.exe\) 文件有效，因此，它需要 .NET Framework 4.5。  
  
 有关开发在 Windows 64 位操作系统上运行的应用程序的更多信息，请参见 [64 位应用程序](../Topic/64-bit%20Applications.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  修改 **目标平台** 属性，因此，若要面向 .NET Framework 4.5，选择或清除**首选 32 位** 复选框。  
  
 **Note**  
 **\/platform** 在 Visual C\# 速成版开发环境中不可用。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.PlatformTarget%2A>。  
  
## 示例  
 下面的示例演示如何使用 **\/platform**选项来指定应只由64 位 Windows 操作系统上的 64 位 CLR 运行的应用程序。  
  
```  
csc /platform:anycpu filename.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)