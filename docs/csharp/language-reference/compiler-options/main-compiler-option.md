---
title: "/main (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/main"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-main compiler option [C#]"
  - "main compiler option [C#]"
  - "/main compiler option [C#]"
ms.assetid: 975cf4d5-36ac-4530-826c-4aad0c7f2049
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# /main (C# Compiler Options)
如果有多个类包含 **Main** 方法，此选项指定包含程序入口点的类。  
  
## 语法  
  
```  
/main:class  
```  
  
## 参数  
 `class`  
 包含 **Main** 方法的类型。  
  
## 备注  
 如果编译包括多个具有 [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md) 方法的类型，可以指定哪个类型包含要用作程序入口点的 **Main** 方法。  
  
 此选项用在编译 .exe 文件时。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  修改**“启动对象”**属性。  
  
     若要以编程方式设置此编译器选项，请参见 <xref:VSLangProj80.ProjectProperties3.StartupObject%2A>。  
  
## 示例  
 编译 `t2.cs` 和 `t3.cs`，并指定将在 `Test2` 中找到 **Main** 方法：  
  
```  
csc t2.cs t3.cs /main:Test2  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)