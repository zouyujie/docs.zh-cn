---
title: "创建和引发异常（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "捕获异常 [C#]"
  - "异常 [C#], 创建"
  - "异常 [C#], 引发"
  - "引发异常 [C#]"
ms.assetid: 6bbba495-a115-4c6d-90cc-1f4d7b5f39e2
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# 创建和引发异常（C# 编程指南）
异常用于指示在运行程序时发生了错误。  此时将创建一个描述错误的异常对象，然后使用 [throw](../../../csharp/language-reference/keywords/throw.md) 关键字“引发”该对象。  然后运行时搜索最兼容的异常处理程序。  
  
 当存在下列一种或多种情况时，程序员应引发异常：  
  
-   方法无法完成其中定义的功能。  
  
     例如，如果方法的参数具有无效值：  
  
     [!code-cs[csProgGuideExceptions#12](../../../csharp/programming-guide/exceptions/codesnippet/csharp/creating-and-throwing-ex_1.cs)]  
  
-   根据对象的状态，对某个对象进行不适当的调用。  
  
     一个示例可能尝试对只读文件执行写操作。  在对象状态不允许某项操作的情况下，引发 <xref:System.InvalidOperationException> 的一个实例或基于此类的派生类的对象。  以下为引发 <xref:System.InvalidOperationException> 对象的方法的示例：  
  
     [!code-cs[csProgGuideExceptions#13](../../../csharp/programming-guide/exceptions/codesnippet/csharp/creating-and-throwing-ex_2.cs)]  
  
-   方法的参数导致了异常。  
  
     在此情况下，应捕获原始异常并创建一个 <xref:System.ArgumentException> 实例。  原始异常应作为 <xref:System.Exception.InnerException%2A> 参数传递给 <xref:System.ArgumentException> 的构造函数：  
  
     [!code-cs[csProgGuideExceptions#14](../../../csharp/programming-guide/exceptions/codesnippet/csharp/creating-and-throwing-ex_3.cs)]  
  
 异常包含一个名为 <xref:System.Exception.StackTrace%2A> 的属性。  此字符串包含当前调用堆栈上的方法的名称，以及为每个方法引发异常的位置（文件名和行号）。  <xref:System.Exception.StackTrace%2A> 对象由公共语言运行时 \(CLR\) 从 `throw` 语句点开始自动创建，因此必须从堆栈跟踪的开始点引发异常。  
  
 所有异常都包含一个名为 <xref:System.Exception.Message%2A> 的属性。  应该设置此字符串来解释发生异常的原因。  注意，不应将安全敏感信息放在消息文本中。  除 <xref:System.Exception.Message%2A> 之外，<xref:System.ArgumentException> 还包含一个名为 <xref:System.ArgumentException.ParamName%2A> 的属性，应将该属性设置为导致引发异常的参数的名称。  对于属性设置器，<xref:System.ArgumentException.ParamName%2A> 应设置为 `value`。  
  
 公共的受保护方法应在其无法完成预期功能时引发异常。  引发的异常类应该是符合错误条件的最确切的可用异常。  这些异常应编写为类功能的一部分，派生类或对原始类的更新应保留相同的行为，以实现向后兼容性。  
  
## 引发异常时要避免的情况  
 下表确定了在引发异常时要避免的做法：  
  
-   不应使用异常来更改正常执行过程中的程序流程。  异常只能用于报告和处理错误条件。  
  
-   只能引发异常，而不能作为返回值或参数返回异常。  
  
-   不要从自己的源代码中有意引发 <xref:System.Exception?displayProperty=fullName>、<xref:System.SystemException?displayProperty=fullName>、<xref:System.NullReferenceException?displayProperty=fullName> 或 <xref:System.IndexOutOfRangeException?displayProperty=fullName>。  
  
-   不要创建可在调试模式下引发但不会在发布模式下引发的异常。  若要在开发阶段确定运行时错误，请改用调试断言。  
  
## 定义异常类  
 程序可以引发 <xref:System> 命名空间中的预定义异常类（前面注明的情况除外），或通过从 <xref:System.Exception> 派生来创建它们自己的异常类。  派生类至少应定义四个构造函数：一个是默认构造函数，一个用来设置消息属性，一个用来设置 <xref:System.Exception.Message%2A> 属性和 <xref:System.Exception.InnerException%2A> 属性。  第四个构造函数用于序列化异常。  新异常类应该可序列化。  例如：  
  
 [!code-cs[csProgGuideExceptions#15](../../../csharp/programming-guide/exceptions/codesnippet/csharp/creating-and-throwing-ex_4.cs)]  
  
 仅当新属性提供的数据有助于解决异常时，才应将其添加到异常类。  如果向派生的异常类添加了新属性，则应重写 `ToString()` 以返回添加的信息。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [异常层次结构](../Topic/Exception%20Hierarchy.md)   
 [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)