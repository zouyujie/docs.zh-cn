---
title: "/bugreport (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/bugreport"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/bugreport compiler option [C#]"
  - "-bugreport compiler option [C#]"
  - "bugreport compiler option [C#]"
ms.assetid: f39665e3-4f6f-4357-88a2-3274c7bec0c1
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# /bugreport (C# Compiler Options)
指定应将调试信息放在文件中，供以后分析使用。  
  
## 语法  
  
```  
/bugreport:file  
```  
  
## 参数  
 `file`  
 要包含 bug 报告的文件的名称。  
  
## 备注  
 **\/bugreport** 选项指定应将下面的信息放在 `file` 中：  
  
-   编译中所有源代码文件的副本。  
  
-   编译中使用的编译器选项列表。  
  
-   有关编译器、运行时和操作系统的版本信息。  
  
-   引用的程序集和模块（保存为十六进制数），.NET Framework 和 SDK 附带的程序集除外。  
  
-   编译器输出（如果有）。  
  
-   将会提示给您的问题的说明。  
  
-   关于考虑问题应如何解决（就此将会向您提示）的说明。  
  
 如果此选项与 **\/errorreport:prompt** 或 **\/errorreport:send** 一起使用，则文件中的信息将发送至 Microsoft Corporation。  
  
 由于所有源代码文件的副本都将放置在 `file` 中，因此可能需要在尽可能短的程序中重现所怀疑的代码缺陷。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
 注意，生成文件的内容会公开源代码，可能导致意外的信息泄露。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [\/errorreport \(Set Error Reporting Behavior\)](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)