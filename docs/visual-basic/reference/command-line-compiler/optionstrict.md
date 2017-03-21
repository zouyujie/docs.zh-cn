---
title: "/optionstrict | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/optionstrict"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/optionstrict 编译器选项 [Visual Basic]"
  - "optionstrict 编译器选项 [Visual Basic]"
  - "-optionstrict 编译器选项 [Visual Basic]"
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /optionstrict
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

强制使用严格类型语义以限制隐式类型转换。  
  
## 语法  
  
```  
/optionstrict[+ | -]  
/optionstrict[:custom]  
```  
  
## 参数  
 `+` &#124; `-`  
 可选。  `/optionstrict+` 选项限制隐式类型转换。  此选项的默认值为 `/optionstrict-`。  `/optionstrict+` 选项与 `/optionstrict` 相同。  这两个选项都可用于许可类型语义。  
  
 `custom`  
 必选。  不遵从严格语言语义时发出警告。  
  
## 备注  
 当 `/optionstrict+` 有效时，只能隐式地进行扩大类型转换。  如果隐式地进行收缩类型转换（例如将 `Decimal` 类型对象赋给一个 Integer 类型的对象），将会报错。  
  
 要为隐式收缩类型转换生成警告，请使用 `/optionstrict:custom`。  使用 `/nowarn:numberlist` 以忽略特定警告，而且 `/warnaserror:numberlist` 将特定警告视为错误。  
  
### 在 Visual Studio IDE 中设置 \/optionstrict  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上单击**“属性”**。有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“编译”**选项卡。  
  
3.  修改**“Option Strict”**框中的值。  
  
### 以编程方式设置 \/optionstrict  
  
-   请参见 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)。  
  
## 示例  
 下面的代码使用严格的类型语义编译 `Test.vb`。  
  
```  
vbc /optionstrict+ test.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [\/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)   
 [\/warnaserror](../../../visual-basic/reference/command-line-compiler/warnaserror.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [“选项”对话框 \-\>“项目”\-\>“Visual Basic 默认值”](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)