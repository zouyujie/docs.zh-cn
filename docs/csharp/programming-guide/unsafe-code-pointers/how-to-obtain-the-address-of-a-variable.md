---
title: "如何：获取变量的地址（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "指针表达式 [C#], address-of 运算符"
  - "指针 [C#], & 运算符"
  - "变量 [C#], address of"
ms.assetid: 44fe2cd9-a64f-4ef5-be2a-09ce807c0182
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# 如何：获取变量的地址（C# 编程指南）
要获取计算结果为固定变量的一元表达式的地址，请使用 address\-of 运算符：  
  
```  
int number;  
int* p = &number; //address-of operator &  
```  
  
 address\-of 运算符仅适用于变量。  如果该变量是可移动变量，则在获取其地址之前，可以使用 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)暂时固定此变量。  
  
 确保初始化该变量是程序员的责任。  如果变量未初始化，编译器不会发出错误消息。  
  
 不能获取常数或值的地址。  
  
## 示例  
 此示例声明一个指向 `int` 的指针 `p`，并将整数变量 `number` 的地址赋值给该指针。  给 \*p 赋值的结果是初始化变量 `number`。  如果对此赋值语句进行注释，则将取消对变量 `number` 的初始化，但是不会发出编译时错误。  注意该示例如何使用[成员访问](../../../csharp/programming-guide/unsafe-code-pointers/how-to-access-a-member-with-a-pointer.md)运算符 `->` 来获取和显示存储在指针中的地址。  
  
 [!code-cs[csProgGuidePointers#7](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers2.cs#7)]  
  
 [!code-cs[csProgGuidePointers#8](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#8)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)