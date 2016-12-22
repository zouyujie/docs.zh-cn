---
title: "/pdb (C# Compiler Options) | Microsoft Docs"
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
  - "/pdb"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-pdb compiler option [C#]"
  - "pdb compiler option [C#]"
  - "/pdb compiler option [C#]"
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /pdb (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/pdb** 编译器选项指定调试符号文件的名称和位置。  
  
## 语法  
  
```  
/pdb:filename  
```  
  
## 参数  
 `filename`  
 调试符号文件的名称和位置。  
  
## 备注  
 当您指定 [\/debug \(Emit Debugging Information\)](../../../csharp/language-reference/compiler-options/debug-compiler-option.md) 时，编译器将在创建输出文件（.exe 或 .dll）的同一目录下创建一个与输出文件同名的 .pdb 文件。  
  
 **\/pdb** 允许您为 .pdb 文件指定非默认的文件名和位置。  
  
 不能在 Visual Studio 开发环境中设置此编译器选项，也不能以编程方式对其进行更改。  
  
## 示例  
 编译 `t.cs` 并创建一个名为 tt.pdb 的 .pdb 文件：  
  
```  
csc /debug /pdb:tt t.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)