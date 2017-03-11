---
title: "/warnaserror (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/warnaserror"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/warnaserror compiler option [C#]"
  - "-warnaserror compiler option [C#]"
  - "warnaserror compiler option [C#]"
ms.assetid: 04680ec3-08d6-4e2e-a274-38310e10e33c
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /warnaserror (C# Compiler Options)
**\/warnaserror\+** 选项将所有警告都视为错误  
  
## 语法  
  
```  
/warnaserror[<U>+</U> | -][:warning-list]  
```  
  
## 备注  
 将一般报告为警告的任何消息都报告为错误，并且暂停生成过程（不生成输出文件）。  
  
 默认情况下启用 **\/warnaserror\-**，这导致警告不会妨碍生成输出文件。  **\/warnaserror** 与 **\/warnaserror\+** 相同，它使警告被视为错误。  
  
 （可选）如果您希望只将几个特定的警告视为错误，可以指定一个以逗号分隔的列表，其中列出被视为错误的警告编号。  
  
 使用 [\/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md) 可指定您希望编译器显示的警告等级。  可以使用 [\/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) 禁用某些警告。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  修改**“将警告视为错误”**属性。  
  
     若要以编程方式设置此编译器选项，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.TreatWarningsAsErrors%2A>。  
  
## 示例  
 编译 `in.cs` 并且让编译器不显示警告：  
  
```  
csc /warnaserror in.cs  
csc /warnaserror:642,649,652 in.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)