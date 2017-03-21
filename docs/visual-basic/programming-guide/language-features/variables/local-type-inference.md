---
title: "局部类型推理 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "local type inference"
  - "vb.TypeInfer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "隐式类型的局部变量 [Visual Basic]"
  - "推理 [Visual Basic]"
  - "本地类型推理 [Visual Basic]"
  - "Option Infer 语句"
  - "类型推理 [Visual Basic]"
  - "变量 [Visual Basic], 类型推理"
ms.assetid: b8307f18-2e56-4ab3-a45a-826873f400f6
caps.latest.revision: 43
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 43
---
# 局部类型推理 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

Visual Basic 编译器使用类型推理来确定未使用 `As` 子句声明的局部变量的数据类型。  编译器将通过初始化表达式的类型推断出变量的类型。  这使您可以声明变量，而无需显式声明类型，如下面的示例中所示。声明的结果是，`num1` 和 `num2` 都被强类型化为整数。  
  
 [!code-vb[VbVbalrTypeInference#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_1.vb)]  
  
> [!NOTE]
>  如果不希望前面示例中的 `num2` 类型化为 `Integer`，则可以使用声明（如 `Dim num3 As Object = 3` 或 `Dim num4 As Double = 3`）指定另一个类型。  
  
 局部类型推理在过程级别适用。  它不能用于在模块级别（在类、结构、模块或接口内，但不在过程或块内）声明变量。  如果上面示例中的 `num2` 是类的字段而不是过程中的局部变量，则在 `Option Strict` 打开时该声明会导致错误，而在 `Option Strict` 关闭时该声明会将 `num2` 分类为 `Object`。  类似，局部类型推理不应用于声明为 `Static` 的过程级别变量。  
  
## 类型推理与后期绑定  
 使用类型推理的代码类似于依赖后期绑定的代码。  但是，类型推理可将变量设置为强类型，而不是使变量保留为 `Object`。  编译器使用变量的初始值设定项，在编译时确定变量的类型，以生成早期绑定代码。  在前面的示例中，与 `num1` 一样，`num2` 被类型化为 `Integer`。  
  
 早期绑定变量的行为与后期绑定变量的行为不同，只有在运行时才知道后期绑定变量的类型。  在早期知道类型，使得编译器可以在执行之前确定问题，准确地分配内存，并且执行其他优化。  早期绑定还使 Visual Basic 集成开发环境 \(IDE\) 可以提供有关对象的成员的 IntelliSense 帮助。  早期绑定还可有利于达到更高的性能。  这是因为存储在后期绑定变量中的所有数据都必须包装为类型 `Object`，在运行时访问该类型的成员，会使得程序运行较慢。  
  
## 示例  
 当局部变量未使用 `As` 子句进行声明，并且被初始化时，会发生类型推理。  编译器将赋予的初始值的类型用作变量的类型。  例如，下面的每行代码声明一个 `String` 类型的变量。  
  
 [!code-vb[VbVbalrTypeInference#2](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_2.vb)]  
  
 下面的代码演示创建一个整数数组的两种等效方式。  
  
 [!code-vb[VbVbalrTypeInference#3](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_3.vb)]  
  
 可以很方便地使用类型推理确定循环控制变量的类型。  在下面的代码中，编译器推断出 `number` 为 `Integer`，因为前面示例中的 `someNumbers2` 是一个整数数组。  
  
 [!code-vb[VbVbalrTypeInference#4](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_4.vb)]  
  
 可以在 `Using` 语句中使用局部类型推理来确定资源名称的类型，如下面的示例所示。  
  
 [!code-vb[VbVbalrTypeInference#7](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_5.vb)]  
  
 还可以从函数的返回值推断变量的类型，如下面的示例所示。  `pList1` 和 `pList2` 都是进程数组，因为 `Process.GetProcesses` 返回进程数组。  
  
 [!code-vb[VbVbalrTypeInference#5](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_6.vb)]  
  
## Option Infer  
 `Option Infer` 可以指定局部类型推理是否在特定文件授予权限。  若要启用或阻止该选项，请在文件的开头键入下列语句之一。  
  
 `Option Infer On`  
  
 `Option Infer Off`  
  
 如果没有在代码中指定 `Option Infer` 的值，则编译器默认为 `Option Infer On`。  对于从 [!INCLUDE[vb_orcas_long](../../../../visual-basic/misc/includes/vb-orcas-long-md.md)] 或早期版本升级的项目，编译器默认为 `Option Infer Off`。  
  
 如果在文件中为 `Option Infer` 设置的值与 IDE 或命令行中设置的值发生冲突，则文件中的值优先。  
  
 有关更多信息，请参见 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)和[“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)。  
  
## 限制  
 类型推理只能用于非静态局部变量；而不能用于确定类字段、属性或函数的类型。  
  
## 请参阅  
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [早期绑定和后期绑定](../../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)   
 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [For...Next 语句](../../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [\/optioninfer](../../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)