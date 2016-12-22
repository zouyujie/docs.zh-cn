---
title: "/checked (C# Compiler Options) | Microsoft Docs"
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
  - "/checked"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "checked compiler option [C#]"
  - "-checked compiler option [C#]"
  - "/checked compiler option [C#]"
ms.assetid: fb7475d3-e6a6-4e6d-b86c-69e7a74c854b
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /checked (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/checked** 选项指定，不在 [checked](../../../csharp/language-reference/keywords/checked.md) 或 [unchecked](../../../csharp/language-reference/keywords/unchecked.md) 关键字的范围内、并且产生的值超出数据类型范围的整数算法语句是否将导致运行时异常。  
  
## 语法  
  
```  
/checked[+ | -]  
```  
  
## 备注  
 `checked` 或 `unchecked` 关键字范围内的整数算法语句不受 **\/checked** 选项的影响。  
  
 如果不在 `checked` 或 `unchecked` 关键字范围内的整数算法语句产生的值超出数据类型范围，并且编译中使用了 **\/checked\+** \(**\/checked**\)，则该语句将在运行时导致异常。  如果编译中使用的是 **\/checked\-**，则该语句在运行时不会导致异常。  
  
 该选项的默认值为 **\/checked\-**.  使用 **\/checked\-** 的一个方案是生成大型应用程序。  有时自动化的工具用于生成该应用程序，而且这种工具可以将 **\/checked** 自动设置为 \+。  可通过指定 **\/checked\-** 重写工具的全局默认值。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  有关更多信息，请参见 [“项目设计器”\-\>“生成”页 \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp)。  
  
2.  单击**“生成”**属性页。  
  
3.  单击**“高级”**按钮。  
  
4.  修改**“检查算法上溢\/下溢”**属性。  
  
 若要以编程方式访问此编译器选项，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.CheckForOverflowUnderflow%2A>。  
  
## 示例  
 使用以下命令编译 `t2.cs`。  命令中 `/checked` 的使用指定，任何不在 `checked` or `unchecked` 关键字范围内以及导致数据类型以外值的结果的文件中的整数算法语句，都会在测试时间内引发异常。  
  
```  
csc t2.cs /checked  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)