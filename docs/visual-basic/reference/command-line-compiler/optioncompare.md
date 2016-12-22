---
title: "/optioncompare | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/optioncompare"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/optioncompare 编译器选项 [Visual Basic]"
  - "optioncompare 编译器选项 [Visual Basic]"
  - "-optioncompare 编译器选项 [Visual Basic]"
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /optioncompare
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定如何进行字符串比较。  
  
## 语法  
  
```  
/optioncompare:{binary | text}  
```  
  
## 备注  
 可以下面两种格式之一指定 `/optioncompare`：若指定 `/optioncompare:binary`，则使用二进制字符串比较；若指定 `/optioncompare:text`，则使用文本字符串比较。  在默认情况下，编译器使用 `/optioncompare:binary`。  
  
 在 Microsoft Windows 中，使用的代码页决定二进制排序顺序。  典型的二进制排序顺序如下所示：  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 基于文本的字符串比较是建立在由您的系统区域设置决定的不区分大小写的文本排序顺序基础上。  典型的文本排序顺序如下所示：  
  
 `(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
### 在 Visual Studio IDE 中设置 \/optioncompare  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“编译”**选项卡。  
  
3.  修改**“比较选项”**框中的值。  
  
### 以编程方式设置 \/optioncompare  
  
-   请参见 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)。  
  
## 示例  
 下面的代码编译 `rojFile.vb` 并使用二进制字符串比较：  
  
```  
vbc /optioncompare:binary projFile.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [“选项”对话框 \-\>“项目”\-\>“Visual Basic 默认值”](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)