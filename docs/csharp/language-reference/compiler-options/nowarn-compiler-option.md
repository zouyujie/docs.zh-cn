---
title: "/nowarn (C# Compiler Options) | Microsoft Docs"
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
  - "/nowarn"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nowarn compiler option [C#]"
  - "/nowarn compiler option [C#]"
  - "-nowarn compiler option [C#]"
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /nowarn (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/nowarn** 选项允许您禁止编译器显示一个或多个警告。  用逗号分隔多个警告编号。  
  
## 语法  
  
```  
/nowarn:number1[,number2,...]  
```  
  
## 参数  
 `number1`, `number2`  
 您希望编译器取消的警告编号。  
  
## 备注  
 只应指定警告标识符的数值部分。  例如，若要取消 CS0028，可以指定 `/nowarn:28`。  
  
 编译器在无人参与的模式下忽略传递给 `/nowarn` 的警告编号，这些警告编号在先前版本中有效但已从编译器中移除。  例如，CS0679 在 Visual Studio .NET 2002 中有效但后来被删除。  
  
 `/nowarn` 选项无法禁止显示以下警告：  
  
-   编译器警告（等级 1）CS2002  
  
-   编译器警告（等级 1）CS2023  
  
-   编译器警告（等级 1）CS2029  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  有关详细信息，请参见[“项目设计器”\-\>“生成”页 \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp)。  
  
2.  单击**“生成”**属性页。  
  
3.  修改**“取消警告”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [C\# Compiler Errors](../../../csharp/language-reference/compiler-messages/index.md)