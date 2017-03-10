---
title: "/preferreduilang (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/preferreduilang"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "preferreduilang compiler option [C#]"
  - "/preferreduilang compiler option [C#]"
  - "-preferreduilang compiler option [C#]"
ms.assetid: 68b2462f-6778-48d7-8052-62805fe8e02c
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /preferreduilang (C# Compiler Options)
使用 `/preferreduilang` 编译器选项，则可指定 C\#编译器显示输出的语言，如错误消息。  
  
## 语法  
  
```  
/preferreduilang: language  
```  
  
## 参数  
 `language`  
 编译器输出用到的语言的[语言名称](http://go.microsoft.com/fwlink/p/?LinkId=236992) 。  
  
## 备注  
 可以使用 `/preferreduilang` 编译器选项指定C\# 编译器用于错误消息和其他命令行输出的语言。  如果语言的语言包不安装，使用操作系统的语言设置，因此，不会报告错误。  
  
```c#  
csc.exe /preferreduilang:ja-JP  
```  
  
## 要求  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)