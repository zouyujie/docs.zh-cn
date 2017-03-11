---
title: "如何：获取指针变量的值（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "指针表达式 [C#], 间接寻址"
  - "指针 [C#], * 运算符"
  - "指针 [C#], 间接寻址"
  - "变量 [C#], 指针"
ms.assetid: 460a813a-4995-44c1-9de2-213b91dc7668
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# 如何：获取指针变量的值（C# 编程指南）
使用指针间接运算符可获取位于指针所指向的位置的变量。  表达式采用下面的形式，其中， `p` 是指针类型：  
  
```  
*p;  
```  
  
 不能对除指针类型以外的任何类型的表达式使用一元间接寻址运算符。  此外，不能将它应用于 [void](../../../csharp/language-reference/keywords/void.md) 指针。  
  
 当向 [null](../../../csharp/language-reference/keywords/null.md) 指针应用间接寻址运算符时，结果将取决于具体的实现。  
  
## 示例  
 下面的示例使用不同类型的指针访问 `char` 类型的变量。  注意，`theChar` 的地址在不同的运行中是不同的，因为分配给变量的物理地址可能会更改。  
  
 [!code-cs[csProgGuidePointers#5](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers2.cs#5)]  
  
 [!code-cs[csProgGuidePointers#6](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#6)]  
  
  **theChar 的值 \= Z**  
**theChar 的地址 \= 12F718**  
**pChar 的值 \= Z**  
**pInt 的值 \= 90**   
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)