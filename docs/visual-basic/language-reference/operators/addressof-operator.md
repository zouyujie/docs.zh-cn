---
title: "AddressOf 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "AddressOf"
  - "vb.AddressOf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "地址, 传递到 API 过程"
  - "AddressOf 运算符"
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# AddressOf 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

创建引用特定过程的过程委托实例。  
  
## 语法  
  
```  
  
AddressOf procedurename  
```  
  
## 部件  
 `procedurename`  
 必选。  指定新创建的过程委托将引用的过程。  
  
## 备注  
 `AddressOf` 运算符创建一个指向由 `procedurename` 指定的函数的函数委托。  如果指定的过程是实例方法，则此函数委托同时引用此实例和方法。  接着，调用此函数委托时，将调用指定实例的指定方法。  
  
 `AddressOf` 运算符可以用作委托构造函数的操作数，或可以用在编译器能够确定委托类型的上下文中。  
  
## 示例  
 本示例使用 `AddressOf` 运算符指定一个委托以处理按钮的 `Click` 事件。  
  
 [!code-vb[VbVbalrDelegates#8](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_1.vb)]  
  
## 示例  
 下面的示例使用 `AddressOf` 运算符来指定线程的启动函数。  
  
 [!code-vb[VbVbalrDelegates#9](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_2.vb)]  
  
## 请参阅  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)