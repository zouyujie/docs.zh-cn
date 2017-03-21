---
title: "/recurse (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/recurse"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/recurse compiler option [C#]"
  - "recurse compiler option [C#]"
  - "-recurse compiler option [C#]"
ms.assetid: 4e8212e5-04e3-45b1-8a42-41bc50e683b0
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# /recurse (C# Compiler Options)
\/recurse 选项使您可以编译指定目录 \(dir\) 或项目目录的所有子目录中的源代码文件。  
  
## 语法  
  
```  
/recurse:[dir\]file  
```  
  
## 参数  
 `dir`（可选）  
 搜索开始的目录。  如果未指定此目录，则搜索从项目目录开始。  
  
 `file`  
 要搜索的文件。  允许使用通配符字符。  
  
## 备注  
 **\/recurse** 选项使您可以编译指定目录 \(`dir`\) 或项目目录的所有子目录中的源代码文件。  
  
 可以在文件名中使用通配符来编译项目目录中所有匹配的文件，而不需使用 **\/recurse**。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
## 示例  
 编译当前目录中的所有 C\# 文件：  
  
```  
csc *.cs  
```  
  
 编译 dir1\\dir2 目录及其任何子目录中的所有 C\# 文件，并生成 dir2.dll：  
  
```  
csc /target:library /out:dir2.dll /recurse:dir1\dir2\*.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)