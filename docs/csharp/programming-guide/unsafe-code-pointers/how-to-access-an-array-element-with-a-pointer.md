---
title: "如何：通过指针访问数组元素（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "指针 [C#], 数组访问"
ms.assetid: 6c46f2af-a730-4855-8638-f136d9abaa12
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 如何：通过指针访问数组元素（C# 编程指南）
在不安全的上下文中，可通过使用指针元素访问来访问内存中的元素，如下面的示例所示：  
  
```  
 char* charPointer = stackalloc char[123];  
for (int i = 65; i < 123; i++)  
{  
    charPointer[i] = (char)i; //access array elements  
}  
```  
  
 方括号中的表达式必须能够隐式转换为 `int`、`uint`、`long` 或 `ulong`。  操作 p\[e\] 等效于 \*\(p\+e\)。  与 C 和 C\+\+ 一样，指针元素访问不检查越界错误。  
  
## 示例  
 在此示例中，123 内存位置被分配给字符数组 `charPointer`。  该数组用于在两个 [for](../../../csharp/language-reference/keywords/for.md) 循环中显示小写字母和大写字母。  
  
 请注意，表达式 `charPointer[i]` 与表达式 `*(charPointer + i)` 等效，使用这两个表达式可获得相同的结果。  
  
 [!code-cs[csProgGuidePointers#11](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-an-array-element-with-a-pointer_1.cs)]  
  
 [!code-cs[csProgGuidePointers#12](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-an-array-element-with-a-pointer_2.cs)]  
  
  **大写字母：**  
**ABCDEFGHIJKLMNOPQRSTUVWXYZ**  
**小写字母：**  
**abcdefghijklmnopqrstuvwxyz**   
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)