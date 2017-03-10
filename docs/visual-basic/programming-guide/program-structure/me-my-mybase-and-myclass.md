---
title: "Visual Basic 中的 Me、My、MyBase 和 MyClass | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "MyClass"
  - "vb.Me"
  - "MyBase"
  - "vb.MyBase"
  - "Me"
  - "vb.MyClass"
  - "vb.This"
  - "vb.My"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "当前实例, Me 关键字"
  - "Me 关键字"
  - "Me 关键字, 引用对象的当前实例"
  - "Me 关键字, 与相似编程元素的关系"
  - "My 对象"
  - "MyBase 关键字, 与相似编程元素的关系"
  - "MyClass 关键字, 与相似编程元素的关系"
  - "自引用"
  - "自引用, Me 关键字"
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Visual Basic 中的 Me、My、MyBase 和 MyClass
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的 `Me`、`My`、`MyBase` 和 `MyClass` 具有类似的名称，但其用途各不相同。  本主题描述上述每个实体，以帮助您区分它们。  
  
## Me  
 `Me` 关键字为引用代码正在运行的类或结构的特定实例提供了一条途径。  `Me` 的行为方式类似于引用当前实例的对象变量或结构变量。  在向另一个类、结构或模块中的过程传递关于某个类或结构的当前执行实例的信息时，使用 `Me` 尤其有用。  
  
 例如，假定在某模块中有以下过程。  
  
```  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 可以使用以下语句来调用此过程并将 <xref:System.Windows.Forms.Form> 类的当前实例作为参数传递。  
  
```  
ChangeFormColor(Me)  
```  
  
## My  
 `My` 功能提供了容易而直观的方法来访问大量 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类，从而使 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 用户能够与计算机、应用程序、设置、资源等进行交互。  
  
## MyBase  
 `MyBase` 关键字的行为方式类似于引用当前类实例的基类的对象变量。  `MyBase` 通常用于访问派生类中被重写或被隐藏的基类成员。  `MyBase.New` 用于从派生类构造函数中显式调用基类构造函数。  
  
## MyClass  
 `MyClass` 关键字的行为方式类似于最初实现时引用类的当前实例的对象变量。  `MyClass` 类似于 `Me`，但调用前者的所有方法都被视为是 `NotOverridable`。  
  
## 请参阅  
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)