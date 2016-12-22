---
title: "Option Infer 语句 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.OptionInfer"
  - "vb.Infer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "声明变量, 推断"
  - "Infer 关键字"
  - "推断出的变量声明"
  - "Option Infer 语句"
  - "变量 [Visual Basic], 声明"
ms.assetid: 4ad3e6e9-8f5b-4209-a248-de22ef6e4652
caps.latest.revision: 72
caps.handback.revision: 72
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Option Infer 语句
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

允许声明变量时使用局部类型推理。  
  
## 语法  
  
```  
Option Infer { On | Off }  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`On`|可选。  启用局部类型推理。|  
|`Off`|可选。  禁用局部类型推理。|  
  
## 备注  
 若要在文件中设置 `Option Infer`，请在任何其他源代码之前、文件顶部键入 `Option Infer On` 或 `Option Infer Off`。  如果为文件中 `Option Infer` 设置的值与在 IDE 中或在命令行上设置的值冲突，则文件中的值优先。  
  
 将 `Option Infer` 设置为 `On`时，你可以无需显式声明数据类型就声明本地变量。  编译器会从其初始化表达式的类型推断出变量的数据类型。  
  
 在下图中，`Option Infer` 处于打开状态。  声明 `Dim someVar = 2` 中的变量由类型推理声明为整数。  
  
 ![声明的 IntelliSense 视图。](../../../visual-basic/language-reference/statements/media/optioninferasinteger.png "optionInferAsInteger")  
Option Infer 处于打开状态时的 IntelliSense  
  
 在下图中，`Option Infer` 处于关闭状态。  声明 `Dim someVar = 2` 中的变量由类型推理声明为 `Object`。  在此示例中，在 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 上将“Option Strict”设置为“关闭”。  
  
 ![声明的 IntelliSense 视图。](../../../visual-basic/language-reference/statements/media/optioninferasobject.png "optionInferAsObject")  
Option Infer 处于关闭状态时的 IntelliSense  
  
> [!NOTE]
>  变量声明为 `Object` 时，可在程序运行时更改运行时类型。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 执行称为*装箱*和*取消装箱*的操作以在 `Object` 和值类型间转换，这减缓了执行速度。  有关装箱和取消装箱的信息，请参阅 [Visual Basic 语言规范](../../../visual-basic/reference/language-specification.md)。  
  
 类型推理适用于过程级，且在类、结构、模块或接口中的过程之外不适用。  
  
 有关附加信息，请参见 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  
  
## 当 Option Infer 语句不存在时  
 如果源代码不包括 `Option Infer` 语句，则使用 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 上的“Option Infer”设置。  如果使用命令行编译器，请使用 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) 编译器选项。  
  
#### 若要在 IDE 中设置 Option Infer  
  
1.  在“解决方案资源管理器”中，选择项目。  在“项目”菜单上，单击“属性”。  有关详细信息，请参阅 [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/zh-cn/983f3c18-832f-4666-afec-74b716ff3e0e)。  
  
2.  单击“编译”选项卡。  
  
3.  设置“Option infer”框中的值。  
  
 创建新项目时，将“编译”选项卡上的“Option Infer”设置为“VB 默认值”对话框中的“Option Infer”设置。  若要访问“工具”菜单上的“VB 默认值”对话框，请单击“选项”。  在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”。  “VB 默认值”中的初始默认设置为 `On`。  
  
#### 若要设置命令行上的 Option Infer  
  
-   包括 **vbc** 命令中的 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) 编译器选项。  
  
## 默认数据类型和值  
 下表描述了指定 `Dim` 语句中数据类型和初始值设定项的各种组合的结果。  
  
|||||  
|-|-|-|-|  
|是否指定数据类型？|是否指定初始值设定项？|示例|结果|  
|否|否|`Dim qty`|如果 `Option Strict` 处于关闭状态（默认），则将变量设置为 `Nothing`。<br /><br /> 如果 `Option Strict` 处于打开状态，则发生编译时错误。|  
|否|是|`Dim qty = 5`|如果 `Option Infer` 处于打开状态（默认），则变量采用初始值设定项的数据类型。  请参阅 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。<br /><br /> 如果 `Option Infer` 和 `Option Strict` 均处于关闭状态，则变量采用 `Object` 的数据类型。<br /><br /> 如果 `Option Infer` 处于关闭状态但 `Option Strict` 处于打开状态，则发生编译时错误。|  
|是|否|`Dim qty As Integer`|将变量初始化为数据类型的默认值。  有关详细信息，请参阅 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。|  
|是|是|`Dim qty  As Integer = 5`|如果初始值设定项的数据类型不可转换为指定数据类型，则会发生编译时错误。|  
  
## 示例  
 下例演示了 `Option Infer` 语句启用局部类型推理的方式。  
  
 [!code-vb[VbVbalrTypeInference#6](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_1.vb)]  
  
## 示例  
 下例演示了变量被标识为 `Object` 时运行时类型可以改变的情况。  
  
 [!code-vb[VbVbalrTypeInference#11](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_2.vb)]  
  
## 请参阅  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [“选项”对话框 \-\>“项目”\-\>“Visual Basic 默认值”](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)