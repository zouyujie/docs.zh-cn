---
title: "析构函数（C# 编程指南）| Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- ~ [C#], in destructors
- C# language, destructors
- destructors [C#]
ms.assetid: 1ae6e46d-a4b1-4a49-abe5-b97f53d9e049
caps.latest.revision: 24
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6940be34b6cc15f006901e6d14d2a38ebb5d012a
ms.lasthandoff: 03/13/2017

---
# <a name="destructors-c-programming-guide"></a>析构函数（C# 编程指南）
析构函数用于析构类的实例。  
  
## <a name="remarks"></a>备注  
  
-   无法在结构中定义析构函数。 它们仅用于类。  
  
-   一个类只能有一个析构函数。  
  
-   析构函数不能继承或重载。  
  
-   不能手动调用析构函数。 可以自动调用它们。  
  
-   析构函数不使用修饰符或参数。  
  
 例如，以下是类 `Car` 的析构函数声明：  
  
 [!code-cs[csProgGuideObjects#86](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/destructors_1.cs)]  
  
 析构函数隐式调用对象基类中的 <xref:System.Object.Finalize%2A>。 因此，前面的析构函数代码可隐式转换为下面的代码：  
  
```  
protected override void Finalize()  
{  
    try  
    {  
        // Cleanup statements...  
    }  
    finally  
    {  
        base.Finalize();  
    }  
}  
```  
  
 这意味着，对继承链（从派生程度最高到派生程度最低）中的所有实例以递归方式调用 `Finalize` 方法。  
  
> [!NOTE]
>  不应使用空的析构函数。 如果类包含析构函数，则在 `Finalize` 队列中创建了一个条目。 调用析构函数时，将调用垃圾回收器来处理此队列。 如果析构函数为空，这只会导致不必要的性能损失。  
  
 程序员无法控制何时调用析构函数，因为这由垃圾回收器决定。 垃圾回收器检查应用程序不再使用的对象。 如果它认为某个对象符合销毁条件，则调用析构函数（如果有），并回收用来存储此对象的内存。 程序退出后还可以调用析构函数。  
  
 可以通过调用 <xref:System.GC.Collect%2A> 强制进行垃圾回收，但多数情况下应避免此操作，因为它可能会造成性能问题。  
  
## <a name="using-destructors-to-release-resources"></a>使用析构函数释放资源  
 一般来说，C# 所占用的内存管理空间比使用不面向带有垃圾回收机制的运行时的语言进行开发时所使用的内存管理空间要少。 这是因为 .NET Framework 垃圾回收器会隐式管理对象的内存分配和释放。 但是，如果应用程序封装非托管的资源，例如窗口、文件和网络连接，则应使用析构函数释放这些资源。 当对象符合销毁条件时，垃圾回收器运行对象的 `Finalize` 方法。  
  
## <a name="explicit-release-of-resources"></a>显式释放资源  
 如果应用程序正在使用昂贵的外部资源，我们还建议在垃圾回收器释放对象前显式释放资源。 若要实现此操作，可从执行必要的对象清除的 <xref:System.IDisposable> 接口实现 `Dispose` 方法。 这样可大大提高应用程序的性能。 如果调用 `Dispose` 方法失败，那么即使拥有对资源的显式控制，析构函数也会成为清除资源的一个保障。  
  
 有关清除资源的详细信息，请参阅下列主题：  
  
-   [Cleaning Up Unmanaged Resources](http://msdn.microsoft.com/library/a17b0066-71c2-4ba4-9822-8e19332fc213)（清理未托管资源）  
  
-   [实现 Dispose 方法](http://msdn.microsoft.com/library/eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9)  
  
-   [using 语句](../../../csharp/language-reference/keywords/using-statement.md)  
  
## <a name="example"></a>示例  
 以下示例创建了三个类，并且这三个类构成了一个继承链。 类 `First` 是基类，`Second` 派生自 `First`，`Third` 派生自 `Second`。 所有三个类都具有析构函数。 在 `Main()` 中，已创建派生程度最高的类的一个实例。 当程序运行时，请注意，将按顺序（从派生程度最高到派生程度最低）自动调用这三个类的析构函数。  
  
 [!code-cs[csProgGuideObjects#85](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/destructors_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.IDisposable>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [垃圾回收](../../../standard/garbagecollection/index.md)
