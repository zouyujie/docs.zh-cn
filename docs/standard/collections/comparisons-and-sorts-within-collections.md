---
title: "集合内的比较和排序"
description: "集合内的比较和排序"
keywords: ".NET、.NET Core"
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c7b7c005-628d-427a-91ad-af0c3958c00e
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 6826c0c2e86d0a1add1f88b001c13143ee098634
ms.lasthandoff: 03/02/2017

---

# <a name="comparisons-and-sorts-within-collections"></a>集合内的比较和排序

[System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) 类在管理集合所涉及的几乎所有进程中执行比较，无论是搜索待删除的元素或返回键值对的值。

集合通常使用相等比较器和/或排序比较器。 有两个构造用于比较。 

## <a name="checking-for-equality"></a>检查等同性

诸如 `Contains`、`IndexOf`、`LastIndexOf` 和 `Remove` 的方法将相等比较器用于集合元素。 如果集合是泛型的，则按照以下原则比较项是否相等：

*   如果类型 T 实现 [IEquatable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IEquatable-1) 泛型接口，则相等比较器是该接口的 `Equals` 方法。

*   如果类型 T 未实现 `IEquatable<T>`，则使用 `Object.Equals`。

此外，字典集合的某些构造函数重载接受 [IEqualityComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEqualityComparer-1) 实现，用于比较键是否相等。

## <a name="determining-sort-order"></a>确定排序顺序

`BinarySearch` 和 `Sort` 等方法将排序比较器用于集合元素。 可在集合的元素间进行比较，或在元素或指定值之间进行比较。 为了比较对象，提出了默认比较器和显式比较器的概念。 

默认比较器依赖至少一个正在被比较的对象来实现 `IComparable` 接口。 在用作列表集合的值或字典集合的键的所有类上实现 `IComparable` 不失为一个好办法。 对泛型集合而言，等同性比较是根据以下内容确定的：

*   如果类型 T 实现 [System.IComparable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IComparable-1) 泛型接口，则默认比较器是该接口的 `CompareTo(T)` 方法。

*   如果类型 T 实现非泛型 [System.IComparable](https://docs.microsoft.com/dotnet/core/api/System.IComparable) 接口，则默认比较器是该接口的 `CompareTo`(Object) 方法。

*   如果类型 T 未实现任何接口，则没有默认比较器，必须显式提供一个比较器或比较委托。

为了提供显式比较，某些方法接受 `IComparer` 实现作为参数。 例如，`List<T>.Sort` 方法接受 [System.Collections.Generic.IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1) 实现。 

## <a name="equality-and-sort-example"></a>等同性和排序示例

以下代码展示了 [IEquatable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IEquatable-1) 和 [IComparable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IComparable-1) 在简单业务对象上的实现。 此外，如果对象被存储在列表中并已排序，那么你会发现调用 `Sort()` 方法会导致“Part”类型使用默认比较器，并通过使用匿名方法实现 `Sort(Comparison<T>)` 方法。

C#

```csharp
using System;
using System.Collections.Generic;
// Simple business object. A PartId is used to identify the type of part 
// but the part name can change. 
public class Part : IEquatable<Part> , IComparable<Part>
{
    public string PartName { get; set; }

    public int PartId { get; set; }

    public override string ToString()
    {
        return "ID: " + PartId + "   Name: " + PartName;
    }
    public override bool Equals(object obj)
    {
        if (obj == null) return false;
        Part objAsPart = obj as Part;
        if (objAsPart == null) return false;
        else return Equals(objAsPart);
    }
    public int SortByNameAscending(string name1, string name2)
    {

        return name1.CompareTo(name2);
    }

    // Default comparer for Part type.
    public int CompareTo(Part comparePart)
    {
          // A null value means that this object is greater.
        if (comparePart == null)
            return 1;

        else
            return this.PartId.CompareTo(comparePart.PartId);
    }
    public override int GetHashCode()
    {
        return PartId;
    }
    public bool Equals(Part other)
    {
        if (other == null) return false;
        return (this.PartId.Equals(other.PartId));
    }
    // Should also override == and != operators.

}
public class Example
{
    public static void Main()
    {
        // Create a list of parts.
        List<Part> parts = new List<Part>();

        // Add parts to the list.
        parts.Add(new Part() { PartName = "regular seat", PartId = 1434 });
        parts.Add(new Part() { PartName= "crank arm", PartId = 1234 });
        parts.Add(new Part() { PartName = "shift lever", PartId = 1634 }); ;
        // Name intentionally left null.
        parts.Add(new Part() {  PartId = 1334 });
        parts.Add(new Part() { PartName = "banana seat", PartId = 1444 });
        parts.Add(new Part() { PartName = "cassette", PartId = 1534 });


        // Write out the parts in the list. This will call the overridden 
        // ToString method in the Part class.
        Console.WriteLine("\nBefore sort:");
        foreach (Part aPart in parts)
        {
            Console.WriteLine(aPart);
        }


        // Call Sort on the list. This will use the 
        // default comparer, which is the Compare method 
        // implemented on Part.
        parts.Sort();


        Console.WriteLine("\nAfter sort by part number:");
        foreach (Part aPart in parts)
        {
            Console.WriteLine(aPart);
        }

        // This shows calling the Sort(Comparison(T) overload using 
        // an anonymous method for the Comparison delegate. 
        // This method treats null as the lesser of two values.
        parts.Sort(delegate(Part x, Part y)
        {
            if (x.PartName == null && y.PartName == null) return 0;
            else if (x.PartName == null) return -1;
            else if (y.PartName == null) return 1;
            else return x.PartName.CompareTo(y.PartName);
        });

        Console.WriteLine("\nAfter sort by name:");
        foreach (Part aPart in parts)
        {
            Console.WriteLine(aPart);
        }

        /*

            Before sort:
        ID: 1434   Name: regular seat
        ID: 1234   Name: crank arm
        ID: 1634   Name: shift lever
        ID: 1334   Name:
        ID: 1444   Name: banana seat
        ID: 1534   Name: cassette

        After sort by part number:
        ID: 1234   Name: crank arm
        ID: 1334   Name:
        ID: 1434   Name: regular seat
        ID: 1444   Name: banana seat
        ID: 1534   Name: cassette
        ID: 1634   Name: shift lever

        After sort by name:
        ID: 1334   Name:
        ID: 1444   Name: banana seat
        ID: 1534   Name: cassette
        ID: 1234   Name: crank arm
        ID: 1434   Name: regular seat
        ID: 1634   Name: shift lever

         */

    }
}
```

## <a name="see-also"></a>另请参阅

[IComparer](https://docs.microsoft.com/dotnet/core/api/System.Collections.IComparer)

[IEquatable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IEquatable-1)

[IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1)

[IComparable](https://docs.microsoft.com/dotnet/core/api/System.IComparable)

[IComparable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IComparable-1)

