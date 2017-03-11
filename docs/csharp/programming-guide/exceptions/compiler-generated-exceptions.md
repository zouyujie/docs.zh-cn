---
title: "编译器生成的异常（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "异常 [C#], 编译器生成的"
ms.assetid: 53b52f97-b366-4ed7-b05b-9eb78096b7f9
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# 编译器生成的异常（C# 编程指南）
有些异常在基本操作失败时由 .NET Framework 的公共语言运行时 \(CLR\) 自动引发。  下表列出了这些异常和它们的错误条件。  
  
|异常|说明|  
|--------|--------|  
|<xref:System.ArithmeticException>|在算术运算期间发生的异常（如 <xref:System.DivideByZeroException> 和 <xref:System.OverflowException>）的基类。|  
|<xref:System.ArrayTypeMismatchException>|当数组存储给定的元素时，如果由于该元素的实际类型与数组的实际类型不兼容而导致存储失败，就会引发此异常。|  
|<xref:System.DivideByZeroException>|在尝试用零除整数值时引发。|  
|<xref:System.IndexOutOfRangeException>|在尝试为数组设置小于零或超出数组界限的索引时引发。|  
|<xref:System.InvalidCastException>|当从基类型到接口或派生类型的显式转换在运行时失败时，就会引发此异常。|  
|<xref:System.NullReferenceException>|在尝试引用值为 [null](../../../csharp/language-reference/keywords/null.md) 的对象时引发。|  
|<xref:System.OutOfMemoryException>|在使用 [new](../../../csharp/language-reference/keywords/new-operator.md) 运算符分配内存的尝试失败时引发。  这表明可用于公共语言运行时的内存已耗尽。|  
|<xref:System.OverflowException>|在 `checked` 上下文中的算术运算溢出时引发。|  
|<xref:System.StackOverflowException>|当执行堆栈由于具有太多的挂起方法调用而耗尽时，就会引发此异常；这通常表明存在非常深的递归或无限递归。|  
|<xref:System.TypeInitializationException>|在静态构造函数引发异常并且不存在可以捕捉到它的兼容 `catch` 子句时引发。|  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try\-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)