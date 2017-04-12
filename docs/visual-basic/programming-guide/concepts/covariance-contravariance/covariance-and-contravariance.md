---
title: "协变和逆变 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 59224c46-9931-466b-8c6e-3648c3e609c6
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b785e298c5ba38a8e3d8cc549b2dcf2df1ef6bd8
ms.lasthandoff: 03/13/2017

---
# <a name="covariance-and-contravariance-visual-basic"></a>协变和逆变 (Visual Basic)
在 Visual Basic 中，协变和逆变启用隐式引用转换为数组类型、 委托类型和泛型类型参数。 协变将保留赋值兼容性，并逆变还原它。  
  
 下面的代码演示赋值兼容性、 协变和逆变之间的差异。  
  
```vb  
' Assignment compatibility.   
Dim str As String = "test"  
' An object of a more derived type is assigned to an object of a less derived type.   
Dim obj As Object = str  
  
' Covariance.   
Dim strings As IEnumerable(Of String) = New List(Of String)()  
' An object that is instantiated with a more derived type argument   
' is assigned to an object instantiated with a less derived type argument.   
' Assignment compatibility is preserved.   
Dim objects As IEnumerable(Of Object) = strings  
  
' Contravariance.             
' Assume that there is the following method in the class:   
' Shared Sub SetObject(ByVal o As Object)  
' End Sub  
Dim actObject As Action(Of Object) = AddressOf SetObject  
  
' An object that is instantiated with a less derived type argument   
' is assigned to an object instantiated with a more derived type argument.   
' Assignment compatibility is reversed.   
Dim actString As Action(Of String) = actObject  
```  
  
 对于数组协变允许隐式将派生程度更大的类型的数组转换为派生程度更小的类型的数组。 但此操作不是类型安全的如下面的代码示例中所示。  
  
```vb  
Dim array() As Object = New String(10) {}  
' The following statement produces a run-time exception.  
' array(0) = 10  
```  
  
 对方法组的协变和逆变支持允许匹配方法签名与委托类型。 这使您可以将分配给委托不仅具有匹配签名，但还返回多个派生类型 （协变） 或方法的方法接受具有较少比指定的委托类型的派生的类型 （逆变） 的参数。 有关详细信息，请参阅[委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)和[使用委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)。  
  
 下面的代码示例说明为方法组支持协变和逆变。  
  
```vb  
Shared Function GetObject() As Object  
    Return Nothing  
End Function  
  
Shared Sub SetObject(ByVal obj As Object)  
End Sub  
  
Shared Function GetString() As String  
    Return ""  
End Function  
  
Shared Sub SetString(ByVal str As String)  
  
End Sub  
  
Shared Sub Test()  
    ' Covariance. A delegate specifies a return type as object,  
    ' but you can assign a method that returns a string.  
    Dim del As Func(Of Object) = AddressOf GetString  
  
    ' Contravariance. A delegate specifies a parameter type as string,  
    ' but you can assign a method that takes an object.  
    Dim del2 As Action(Of String) = AddressOf SetObject  
End Sub  
```  
  
 在.NET Framework 4 或更高版本的 Visual Basic 支持协变和逆变在泛型接口和委托中，并允许隐式转换的泛型类型参数。 有关详细信息，请参阅[泛型接口 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)和[委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)。  
  
 下面的代码示例演示泛型接口的隐式引用转换。  
  
```vb  
Dim strings As IEnumerable(Of String) = New List(Of String)  
Dim objects As IEnumerable(Of Object) = strings  
```  
  
 泛型接口或委托称为*变体*如果其泛型参数声明为协变或逆变。 Visual Basic 让您可以创建您自己的变体接口和委托。 有关详细信息，请参阅[创建变体泛型接口 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)和[委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)。  
  
## <a name="related-topics"></a>相关主题  
  
|标题|说明|  
|-----------|-----------------|  
|[泛型接口 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)|讨论泛型接口中的协变和逆变，提供 .NET Framework 中的变体泛型接口列表。|  
|[创建变体泛型接口 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)|演示如何创建自定义的变体接口。|  
|[泛型集合 (Visual Basic 中) 的接口中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)|显示中如何支持协变和逆变<xref:System.Collections.Generic.IEnumerable%601>和<xref:System.IComparable%601>界面可帮助您重用代码。</xref:System.IComparable%601> </xref:System.Collections.Generic.IEnumerable%601>|  
|[委托 (Visual Basic 中) 中的变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)|协变和逆变在泛型和非泛型委托中的讨论并提供.NET Framework 中的变体泛型委托的列表。|  
|[在委托 (Visual Basic 中) 中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)|演示如何在非泛型委托中使用协变和逆变支持来匹配方法签名与委托类型。|  
|[对 Func 和 Action 泛型委托 (Visual Basic 中) 中使用变体](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)|显示中如何支持协变和逆变`Func`和`Action`委托可以帮助您重用代码。|
