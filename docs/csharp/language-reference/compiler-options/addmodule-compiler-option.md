---
title: "/addmodule (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/addmodule"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/addmodule compiler option [C#]"
  - "-addmodule compiler option [C#]"
  - "addmodule compiler option [C#]"
ms.assetid: ed604546-0dc2-4bd4-9a3e-610a8d973e58
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /addmodule (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此选项将一个使用 target:module 开关创建的模块添加到当前的编译中。  
  
## 语法  
  
```  
/addmodule:file[;file2]  
```  
  
## 参数  
 `file`, `file2`  
 包含元数据的输出文件。  该文件不能包含程序集清单。  若要导入多个文件，请用逗号或分号分隔文件名。  
  
## 备注  
 运行时，所有用 **\/addmodule** 添加的模块必须与输出文件在同一目录中。  也就是说，编译时可以在任何目录中指定模块，但是在运行时模块必须在应用程序目录中。  如果模块在运行时不在应用程序目录中，您将遇到 <xref:System.TypeLoadException>。  
  
 `file` 不能包含程序集。  例如，如果输出文件用 [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) 创建，则其元数据可以用 **\/addmodule** 导入。  
  
 如果输出文件用 **\/target** 选项而不是 **\/target:module** 创建，则其元数据无法用 **\/addmodule** 导入，但是可以用 [\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 导入。  
  
 此编译器选项在 Visual Studio 中不可用；项目不能引用模块。  另外，不能以编程方式更改此编译器选项。  
  
## 示例  
 编译源文件 `input.cs` 并从 `metad1.netmodule` 和 `metad2.netmodule` 中添加元数据来产生 `out.exe`：  
  
```  
csc /addmodule:metad1.netmodule;metad2.netmodule /out:out.exe input.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [多文件程序集](../Topic/Multifile%20Assemblies.md)   
 [如何：生成多文件程序集](../Topic/How%20to:%20Build%20a%20Multifile%20Assembly.md)