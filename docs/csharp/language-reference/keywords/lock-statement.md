---
title: "“锁定”语句（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "lock_CSharpKeyword"
  - "lock"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lock 关键字 [C#]"
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
caps.latest.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 43
---
# “锁定”语句（C# 参考）
`lock` 关键字将语句块标记为临界区，方法是获取给定对象的互斥锁，执行语句，然后释放该锁。  下面的示例包含一个 `lock` 语句。  
  
```  
  
class Account  
{  
    decimal balance;  
    private Object thisLock = new Object();  
  
    public void Withdraw(decimal amount)  
    {  
        lock (thisLock)  
        {  
            if (amount > balance)  
            {  
                throw new Exception("Insufficient funds");  
            }  
            balance -= amount;  
        }  
    }  
}  
  
```  
  
 有关更多信息，请参见 [线程同步](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 备注  
 `lock` 关键字可确保当一个线程位于代码的临界区时，另一个线程不会进入该临界区。  如果其他线程尝试进入锁定的代码，则它将一直等待（即被阻止），直到该对象被释放。  
  
 [线程](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md) 这节讨论了线程处理。  
  
 `lock` 关键字在块的开始处调用 <xref:System.Threading.Monitor.Enter%2A>，而在块的结尾处调用 <xref:System.Threading.Monitor.Exit%2A>。  <xref:System.Threading.ThreadInterruptedException> 引发，如果 <xref:System.Threading.Thread.Interrupt%2A> 中断等待输入 `lock` 语句的线程。  
  
 通常，应避免锁定 `public` 类型，否则实例将超出代码的控制范围。  常见的结构 `lock (this)`、`lock (typeof (MyType))` 和 `lock ("myLock")` 违反此准则：  
  
-   如果实例可以被公共访问，将出现 `lock (this)` 问题。  
  
-   如果 `MyType` 可以被公共访问，将出现 `lock (typeof (MyType))` 问题。  
  
-   由于进程中使用同一字符串的任何其他代码都将共享同一个锁，所以出现 `lock("myLock")` 问题。  
  
 最佳做法是定义 `private` 对象来锁定, 或 `private static` 对象变量来保护所有实例所共有的数据。  
  
 在 `lock` 语句的正文不能使用 [等待](../../../csharp/language-reference/keywords/await.md) 关键字。  
  
## 示例  
 下面演示在 C\# 中使用未锁定的线程的简单示例。  
  
 [!code-cs[csrefKeywordsFixedLock#5](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#5)]  
  
## 示例  
 下例使用线程和 `lock`。  只要 `lock` 语句存在，语句块就是临界区并且 `balance` 永远不会是负数。  
  
 [!code-cs[csrefKeywordsFixedLock#6](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#6)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Reflection.MethodImplAttributes>   
 <xref:System.Threading.Mutex>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [线程](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [语句关键字](../../../csharp/language-reference/keywords/statement-keywords.md)   
 [监视器](../Topic/Monitors.md)   
 [Interlocked Operations](../Topic/Interlocked%20Operations.md)   
 [AutoResetEvent](../Topic/AutoResetEvent.md)   
 [线程同步](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)