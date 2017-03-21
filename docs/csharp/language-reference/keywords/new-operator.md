---
title: "new 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "new 运算符关键字 [C#]"
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# new 运算符（C# 参考）
用于创建对象和调用构造函数。  例如：  
  
```  
Class1 obj  = new Class1();  
```  
  
 还可用于创建匿名类型的实例：  
  
```  
var query = from cust in customers  
            select new {Name = cust.Name, Address = cust.PrimaryAddress};  
```  
  
 `new` 运算符还用于调用值类型的默认构造函数。  例如：  
  
```  
int i = new int();  
```  
  
 在上一个语句中，`i` 初始化为 `0`，它是 `int` 类型的默认值。  该语句的效果等同于：  
  
```  
int i = 0;  
```  
  
 有关默认值的完整列表，请参见[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
 请记住，为[结构](../../../csharp/language-reference/keywords/struct.md)声明默认的构造函数是错误的，因为每一个值类型都隐式具有一个公共的默认构造函数。  可以在结构类型上声明参数化构造函数以设置其初始值，但是，只有在需要默认值之外的值时才必须这样做。  
  
 值类型对象（例如结构）是在堆栈上创建的，而引用类型对象（例如类）是在堆上创建的。  两种类型的对象都是自动销毁的，但是，基于值类型的对象是在超出范围时销毁，而基于引用类型的对象则是在对该对象的最后一个引用被移除之后在某个不确定的时间销毁。  对于占用固定资源（例如大量内存、文件句柄或网络连接）的引用类型，有时需要使用确定性终止以确保对象被尽快销毁。  有关更多信息，请参见 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)。  
  
 不能重载 `new` 运算符。  
  
 如果 `new` 运算符分配内存失败，将引发异常 <xref:System.OutOfMemoryException>。  
  
## 示例  
 在下面的示例中，通过使用 `new` 运算符创建并初始化一个 `struct` 对象和一个类对象，然后为它们赋值。  显示了默认值和所赋的值。  
  
 [!code-cs[csrefKeywordsOperator#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-operator_1.cs)]  
  
 注意，在示例中字符串的默认值为 `null`，  因此未显示它。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)