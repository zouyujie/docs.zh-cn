---
title: "如何：使用指针复制字节数组（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数组 [C#], byte"
  - "字节数组 [C#]"
  - "指针 [C#], 复制字节"
ms.assetid: ec16fbb4-a24e-45f5-a763-9499d3fabe0a
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# 如何：使用指针复制字节数组（C# 编程指南）
下面的示例使用指针将字节从一个数组复制到另一个数组。  
  
 此示例使用 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 关键字，它使您能够在 `Copy` 方法中使用指针。  [fixed](../../../csharp/language-reference/keywords/fixed-statement.md) 语句用于声明指向源数组和目标数组的指针。  这将锁定源数组和目标数组在内存中的位置，使其不会因为垃圾回收操作而移动。  这些数组的内存块将在 `fixed` 块结束时取消锁定。  因为此示例中的 `Copy` 方法使用了 `unsafe` 关键字，所以必须使用 **\/unsafe** 编译器选项编译此方法。  若要在 Visual Studio 中设置选项，请右击项目名称，然后单击**“属性”**。  在**“生成”**选项卡上，选择**“允许不安全代码”**。  
  
## 示例  
 [!code-cs[csProgGuidePointers#3](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers2.cs#3)]  
  
 [!code-cs[csProgGuidePointers#18](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#18)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [\/unsafe \(Enable Unsafe Mode\)](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)   
 [Garbage Collection](../Topic/Garbage%20Collection.md)