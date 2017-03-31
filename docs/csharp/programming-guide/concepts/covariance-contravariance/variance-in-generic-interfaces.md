---
title: "泛型接口中的变体 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 4828a8f9-48c0-4128-9749-7fcd6bf19a06
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4c4f3ab00b4de2a6f38858dd5f332db3d47eb85b
ms.lasthandoff: 03/13/2017

---
# <a name="variance-in-generic-interfaces-c"></a>泛型接口中的变体 (C#)
.NET Framework 4 引入了对多个现有泛型接口的变体支持。 变体支持允许实现这些接口的类进行隐式转换。 下面的接口现在是变体：  
  
-   <xref:System.Collections.Generic.IEnumerable%601>（T 是协变）  
  
-   <xref:System.Collections.Generic.IEnumerator%601>（T 是协变）  
  
-   <xref:System.Linq.IQueryable%601>（T 是协变）  
  
-   <xref:System.Linq.IGrouping%602>（`TKey` 和 `TElement` 是协变）  
  
-   <xref:System.Collections.Generic.IComparer%601>（T 是逆变）  
  
-   <xref:System.Collections.Generic.IEqualityComparer%601>（T 是逆变）  
  
-   <xref:System.IComparable%601>（T 是逆变）  
  
 协变允许方法具有的返回类型比接口的泛型类型参数定义的返回类型的派生程度更大。 若要演示协变功能，请考虑以下泛型接口：`IEnumerable<Object>` 和 `IEnumerable<String>`。 `IEnumerable<String>` 接口不继承 `IEnumerable<Object>` 接口。 但是，`String` 类型会继承 `Object` 类型，在某些情况下，建议为这些接口互相指派彼此的对象。 下面的代码示例对此进行了演示。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 在 .NET Framework 早期版本中，在 `Option Strict On` 条件下，此代码会导致 C# 中出现编译错误。 但现在可使用 `strings` 代替 `objects`，如上例所示，因为 <xref:System.Collections.Generic.IEnumerable%601> 接口是协变接口。  
  
 逆变允许方法具有的实参类型比接口的泛型形参定义的类型的派生程度更小。 若要演示逆变，假设已创建了 `BaseComparer` 类来比较 `BaseClass` 类的实例。 `BaseComparer` 类实现 `IEqualityComparer<BaseClass>` 接口。 因为 <xref:System.Collections.Generic.IEqualityComparer%601> 接口现在是逆变接口，因此可使用 `BaseComparer` 比较继承 `BaseClass` 类的类的实例。 下面的代码示例对此进行了演示。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 有关更多示例，请参阅[在泛型集合的接口中使用变体 (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)。  
  
 只有引用类型才支持使用泛型接口中的变体。 值类型不支持变体。 例如，无法将 `IEnumerable<int>` 隐式转换为 `IEnumerable<object>`，因为整数由值类型表示。  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 还需记住，实现变体接口的类仍是固定类。 例如，尽管 <xref:System.Collections.Generic.List%601> 实现协变接口 <xref:System.Collections.Generic.IEnumerable%601>，但无法将 `List<Object>` 隐式转换为 `List<String>`。 以下代码示例阐释了这一点。  
  
```cs  
// The following line generates a compiler error  
// because classes are invariant.  
// List<Object> list = new List<String>();  
  
// You can use the interface object instead.  
IEnumerable<Object> listObjects = new List<String>();  
```  
  
## <a name="see-also"></a>请参阅  
 [在泛型集合的接口中使用变体 (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)   
 [创建变体泛型接口 (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)   
 [泛型接口](http://msdn.microsoft.com/library/88bf5b04-d371-4edb-ba38-01ec7cabaacf)   
 [委托中的变体 (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
