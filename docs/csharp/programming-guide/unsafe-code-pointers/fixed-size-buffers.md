---
title: "固定大小的缓冲区（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "固定大小缓冲区 [C#]"
  - "不安全缓冲区 [C#]"
  - "不安全代码 [C#], 固定大小缓冲区"
ms.assetid: 6220d454-947c-4977-ac9d-9308c6ed5051
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# 固定大小的缓冲区（C# 编程指南）
在 C\# 中，可以使用 [fixed](../../../csharp/language-reference/keywords/fixed-statement.md) 语句在数据结构中创建带有固定大小数组的缓冲区。  使用现有代码（如使用其他语言、预先存在的 DLL 或 COM 项目编写的代码）时，这种方法非常有用。  固定数组可采用允许普通结构成员使用的任何特性或修饰符。  唯一的限制是，数组类型必须是 `bool`、`byte`、 `char`、 `short`、`int`、`long`、`sbyte`、`ushort`、`uint`、`ulong`、`float` 或 `double`。  
  
```  
private fixed char name[30];  
```  
  
## 备注  
 在早期版本的 C\# 中，声明 C\+\+ 样式的固定大小结构是很困难的，因为包含数组的 C\# 结构不包含数组元素。  相反，该结构包含对元素的引用。  
  
 C\# 2.0 添加了在 [struct](../../../csharp/language-reference/keywords/struct.md)（当用在 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 代码块中时）中嵌入固定大小的数组的功能。  
  
 例如，在 C\# 2.0 之前，下面的 `struct` 的大小为 8 字节。  `pathName` 数组是对堆分配数组的引用：  
  
 [!code-cs[csProgGuidePointers#19](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#19)]  
  
 从 C\# 2.0 开始，`struct` 可以包含嵌入的数组。  在下面的示例中，`fixedBuffer` 数组有固定的大小。  若要访问数组的元素，应使用 `fixed` 语句建立指向第一个元素的指针。  `fixed` 语句将 `fixedBuffer` 实例固定到内存中的特定位置。  
  
 [!code-cs[csProgGuidePointers#20](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#20)]  
  
 128 个元素的 `char` 数组的大小为 256 字节。  在固定大小的 [char](../../../csharp/language-reference/keywords/char.md) 缓冲区中，每个字符始终占用两个字节，而与编码无关。  即使将 char 缓冲区封送到具有 `CharSet = CharSet.Auto` 或 `CharSet = CharSet.Ansi` 的 API 方法或结构，也是如此。  有关更多信息，请参见 <xref:System.Runtime.InteropServices.CharSet>。  
  
 另一种常见的固定大小的数组是 [bool](../../../csharp/language-reference/keywords/bool.md) 数组。  `bool` 数组中元素的大小始终为一个字节。  `bool` 数组不适合于创建位数组或缓冲区。  
  
> [!NOTE]
>  除了用 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md) 创建的内存之外，C\# 编译器和公共语言运行时 \(CLR\) 不执行任何安全缓冲区溢出检查。  与所有不安全代码一样，请谨慎使用。  
  
 不安全缓冲区与常规数组在以下方面不同：  
  
-   不安全缓冲区只能用在不安全上下文中。  
  
-   不安全缓冲区始终是向量（或一维数组）。  
  
-   数组的声明应包括计数，如 `char id[8]`。  而不能使用 `char id[]`。  
  
-   不安全缓冲区只能是不安全上下文中的结构的实例字段。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [互操作性](../../../csharp/programming-guide/interop/interoperability.md)