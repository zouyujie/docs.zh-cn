---
title: "/optimize (C# Compiler Options) | Microsoft Docs"
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
  - "/optimize"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/optimize compiler option [C#]"
  - "-o compiler option [C#]"
  - "optimize compiler option [C#]"
  - "/o compiler option [C#]"
  - "-optimize compiler option [C#]"
  - "compiler optimization [C#]"
  - "o compiler option [C#]"
ms.assetid: 6dd5b6f2-cd1d-4593-a9f4-1c2ed9404ca0
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /optimize (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/optimize** 选项启用或禁用由编译器执行以使输出文件更小、更快和更有效的优化。  
  
## 语法  
  
```  
/optimize[+ | -]  
```  
  
## 备注  
 **\/optimize** 选项还通知公共语言运行时在运行时优化代码。  
  
 默认情况下，将禁用优化。  指定 **\/optimize\+** 以启用优化。  
  
 在生成要由程序集使用的模块时，请使用与该程序集的设置相同的 **\/optimize** 设置。  
  
 **\/o** 是 **\/optimize** 的缩写形式。  
  
 可以组合 **\/optimize** 和 [\/debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md) 选项。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  修改**“优化代码”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.Optimize%2A>。  
  
## 示例  
 生成 `t2.cs`并允许编译器优化：  
  
```  
csc t2.cs /optimize  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)