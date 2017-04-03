---
title: "void（C# 参考）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- void_CSharpKeyword
- void
dev_langs:
- CSharp
helpviewer_keywords:
- void keyword [C#]
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b4aa3c7c54e5e4d53975262adbbd9b54c701a69e
ms.lasthandoff: 03/13/2017

---
# <a name="void-c-reference"></a>void（C# 参考）
当用作一种方法的返回类型时，`void` 将指定该方法不返回值。  
  
 方法的参数列表中不允许有 `void`。 无参数且不返回值的方法的声明方式如下：  
  
```  
public void SampleMethod()  
{  
    // Body of the method.  
}  
  
```  
  
 `void` 还可用于在不安全的上下文中将指针声明为未知类型。 有关详细信息，请参阅[指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)。  
  
 `void` 是 .NET Framework <xref:System.Void?displayProperty=fullName> 类型的一个别名。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)
