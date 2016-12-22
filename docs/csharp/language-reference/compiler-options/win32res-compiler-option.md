---
title: "/win32res (C# Compiler Options) | Microsoft Docs"
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
  - "/win32res"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "win32res compiler option"
  - "/win32res compiler option [C#]"
  - "-win32res compiler option [C#]"
  - "win32res compiler option [C#]"
ms.assetid: 3c33f750-6948-4c7e-a27e-bef98f77255b
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /win32res (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/win32res** 选项在输出文件中插入 Win32 资源。  
  
## 语法  
  
```  
/win32res:filename  
```  
  
## 参数  
 `filename`  
 要添加到输出文件的资源文件。  
  
## 备注  
 Win32 资源文件可以用[资源编译器](http://go.microsoft.com/fwlink/?LinkId=148370)创建。  在编译 Visual C\+\+ 程序时会调用资源编译器；.res 文件是用 .rc 文件创建的。  
  
 Win32 资源可以包含版本或位图（图标）信息，这些信息有助于在文件资源管理器中标识您的应用程序。  如果不指定 **\/win32res**，编译器将根据程序集版本生成版本信息。  
  
 请参见 [\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)（用于引用 .NET Framework 资源文件）或 [\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)（用于附加 .NET Framework 资源文件）。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  单击**“资源文件”**按钮，然后使用组合框选择文件。  
  
## 示例  
 编译 `in.cs`，并附加 Win32 资源文件 `rf.res` 以生成 `in.exe`：  
  
```  
csc /win32res:rf.res in.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)