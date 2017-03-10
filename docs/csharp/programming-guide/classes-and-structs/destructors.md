---
title: "析构函数（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "~ [C#], 在析构函数中"
  - "C# 语言, 析构函数"
  - "析构函数 [C#]"
ms.assetid: 1ae6e46d-a4b1-4a49-abe5-b97f53d9e049
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# 析构函数（C# 编程指南）
析构函数用于析构类的实例。  
  
## 备注  
  
-   不能在结构中定义析构函数。  只能对类使用析构函数。  
  
-   一个类只能有一个析构函数。  
  
-   无法继承或重载析构函数。  
  
-   无法调用析构函数。  它们是被自动调用的。  
  
-   析构函数既没有修饰符，也没有参数。  
  
 例如，下面是类 `Car` 的析构函数的声明：  
  
 [!code-cs[csProgGuideObjects#86](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/destructors_1.cs)]  
  
 该析构函数隐式地对对象的基类调用 <xref:System.Object.Finalize%2A>。  这样，前面的析构函数代码被隐式地转换为以下代码：  
  
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
  
 这意味着对继承链中的所有实例递归地调用 `Finalize` 方法（从派生程度最大的到派生程度最小的）。  
  
> [!NOTE]
>  不应使用空析构函数。  如果类包含析构函数，`Finalize` 队列中则会创建一个项。  调用析构函数时，将调用垃圾回收器来处理该队列。  如果析构函数为空，只会导致不必要的性能损失。  
  
 程序员无法控制何时调用析构函数，因为这是由垃圾回收器决定的。  垃圾回收器检查是否存在应用程序不再使用的对象。  如果垃圾回收器认为某个对象符合析构，则调用析构函数（如果有）并回收用来存储此对象的内存。  程序退出时也会调用析构函数。  
  
 可以通过调用 <xref:System.GC.Collect%2A> 强制进行垃圾回收，但大多数情况下应避免这样做，因为这样会导致性能问题。  
  
## 使用析构函数释放资源  
 通常，与运行时不进行垃圾回收的开发语言相比，C\# 无需太多的内存管理。  这是因为 .NET Framework 垃圾回收器会隐式地管理对象的内存分配和释放。  但是，当应用程序封装窗口、文件和网络连接这类非托管资源时，应当使用析构函数释放这些资源。  当对象符合析构时，垃圾回收器将运行对象的 `Finalize` 方法。  
  
## 资源的显式释放  
 如果您的应用程序在使用昂贵的外部资源，我们还建议您提供一种在垃圾回收器释放对象前显式地释放资源的方式。  可通过实现来自 <xref:System.IDisposable> 接口的 `Dispose` 方法来完成这一点，该方法为对象执行必要的清理。  这样可大大提高应用程序的性能。  即使有这种对资源的显式控制，析构函数也是一种保护措施，可用来在对 `Dispose` 方法的调用失败时清理资源。  
  
 有关清理资源的更多详细信息，请参见下列主题：  
  
-   [Cleaning Up Unmanaged Resources](../Topic/Cleaning%20Up%20Unmanaged%20Resources.md)  
  
-   [Implementing a Dispose Method](../Topic/Implementing%20a%20Dispose%20Method.md)  
  
-   [using 语句](../../../csharp/language-reference/keywords/using-statement.md)  
  
## 示例  
 下面的示例创建三个类，这三个类构成了一个继承链。  类 `First` 是基类，`Second` 是从 `First` 派生的，而 `Third` 是从 `Second` 派生的。  这三个类都有析构函数。  在 `Main()` 中，创建了派生程度最大的类的实例。  注意：程序运行时，这三个类的析构函数将自动被调用，并且是按照从派生程度最大的到派生程度最小的次序调用。  
  
 [!code-cs[csProgGuideObjects#85](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/destructors_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.IDisposable>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Garbage Collection](../Topic/Garbage%20Collection.md)