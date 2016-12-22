---
title: "/target:module (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/target:module"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-target compiler options [C#], /target:module"
  - "target compiler options [C#], /target:module"
  - "/target compiler options [C#], /target:module"
ms.assetid: 9af1e4fa-c749-44e7-ae58-90a3d05d4e72
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /target:module (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此选项导致编译器不会生成程序集清单。  
  
## 语法  
  
```  
/target:module  
```  
  
## 备注  
 默认情况下，使用此选项编译时所创建的输出文件具有 .netmodule扩展名。  
  
 没有程序集清单的文件无法由 .NET Framework 公共语言运行时加载。  但可以通过 [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 将这类文件并入程序集清单中。  
  
 如果在一次编译中创建了多个模块，一个模块中的 [internal](../../../csharp/language-reference/keywords/internal.md) 类型可用于此编译中的其他模块。  如果一个模块中的代码引用另一个模块中的 `internal` 类型，则两个模块都必须通过 **\/addmodule** 合并到一个程序集清单中。  
  
 Visual Studio 开发环境不支持创建模块。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## 示例  
 编译 `in.cs`，创建 `in.netmodule`：  
  
```  
csc /target:module in.cs  
```  
  
## 请参阅  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)