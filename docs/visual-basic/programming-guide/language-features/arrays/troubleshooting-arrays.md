---
title: "数组疑难解答 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数组 [Visual Basic], 编译错误"
  - "数组 [Visual Basic], 声明错误"
  - "数组 [Visual Basic], 初始化错误"
  - "数组 [Visual Basic], 疑难解答"
  - "数组疑难解答"
  - "Visual Basic 疑难解答, 数组"
ms.assetid: f4e971c7-c0a4-4ed7-a77a-8d71039f266f
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 数组疑难解答 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本页列出了使用数组过程中出现的一些常见问题。  
  
## 声明和初始化数组时的编译错误  
 如果错误理解用于声明、创建和初始化数组的规则，将产生编译错误。  下面列出了最常见的错误原因：  
  
-   在声明数组变量时，在指定维长度后提供了 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md) 子句。  以下代码行显示了此类型的无效声明。  
  
     `Dim INVALIDsingleDimByteArray(2) As Byte = New Byte()`  
  
     `Dim INVALIDtwoDimShortArray(1, 1) As Short = New Short(,)`  
  
     `Dim INVALIDjaggedByteArray(1)() As Byte = New Byte()()`  
  
-   指定的维长度超过了交错数组的顶级数组。  以下代码行显示了此类型的无效声明。  
  
     `Dim INVALIDjaggedByteArray(1)(1) As Byte`  
  
-   在指定元素值时遗漏了 `New` 关键字。  以下代码行显示了此类型的无效声明。  
  
     `Dim INVALIDoneDimShortArray() As Short = Short() {0, 1, 2, 3}`  
  
-   提供 `New` 子句时没有使用括号 \(`{}`\)。  以下代码行显示了此类型的无效声明。  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte()`  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte(2)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(,)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(1, 1)`  
  
## 访问的数组超出界限  
 在初始化数组的过程中，将为每一维指定一个上限和一个下限。  每次访问数组元素时，都必须为每一维指定一个有效的索引或下标。  如果任何索引低于其下限或高于其上限，将引发 <xref:System.IndexOutOfRangeException> 异常。  编译器无法检测到这种错误，因而在运行时将发生错误。  
  
### 确定界限  
 如果其他组件向您的代码中传递数组（如作为过程参数），您将不清楚该数组的大小或其维长度。  此时，您应首先确定数组每一维的上限，然后再尝试访问任何数组元素。  如果数组不是使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] `New` 子句创建的，则下限可能不是 0，因此，最好也同时确定其下限。  
  
### 指定维度  
 在确定多维数组的界限时，请注意维度的指定方式。  <xref:System.Array.GetLowerBound%2A> 和 <xref:System.Array.GetUpperBound%2A> 方法的 `dimension` 参数是从 0 开始的，而 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] <xref:Microsoft.VisualBasic.Information.LBound%2A> 和 <xref:Microsoft.VisualBasic.Information.UBound%2A> 函数的 `Rank` 参数是从 1 开始的。  
  
## 请参阅  
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [如何：在 Visual Basic 中初始化数组变量](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)