---
title: "/win32icon (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/win32icon"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "win32icon compiler option [C#]"
  - "/win32icon compiler option [C#]"
  - "-win32icon compiler option [C#]"
ms.assetid: 756d9b6d-ab07-41b7-ba58-5bd88f711138
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# /win32icon (C# Compiler Options)
**\/win32icon** 选项在输出文件中插入 .ico 文件，这样.赋予输出文件在 Windows 资源管理器中的所需外观。  
  
## 语法  
  
```  
/win32icon:filename  
```  
  
## 参数  
 `filename`  
 要添加到输出文件的 .ico 文件。  
  
## 备注  
 可以使用[资源编译器](http://go.microsoft.com/fwlink/?LinkId=148370)创建.ico 文件。  编译 Visual C\+\+ 程序时将调用资源编译器；.ico 文件是从 .rc 文件创建的。  
  
 请参见 [\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)（用于引用 .NET Framework 资源文件）或 [\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)（用于附加 .NET Framework 资源文件）。  要导入 .res 文件，请参见 [\/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  修改**“应用程序图标”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.ApplicationIcon%2A>。  
  
## 示例  
 编译 `in.cs`，并附加 .ico 文件 `rf.ico` 以生成 `in.exe`：  
  
```  
csc /win32icon:rf.ico in.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)