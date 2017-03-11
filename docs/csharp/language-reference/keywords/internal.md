---
title: "internal（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "internal_CSharpKeyword"
  - "internal"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "internal 关键字 [C#]"
ms.assetid: 6ee0785c-d7c8-49b8-bb72-0a4dfbcb6461
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# internal（C# 参考）
`internal` 关键字是类型和类型的成员 [访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)。  只有在同一程序集的文件中，内部类型或成员才是可访问的，如下例所示：  
  
```  
public class BaseClass   
{  
    // Only accessible within the same assembly  
    internal static int x = 0;  
}  
```  
  
 从当前程序集或从包含类派生的类型，可以访问具有访问修饰符 `protected internal` 的类型或成员。  
  
 有关 `internal` 与其他访问修饰符的比较，请参见[可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)和[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 有关程序集的更多信息，请参见[程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 内部访问通常用于基于组件的开发，因为它使一组组件能够以私有方式进行合作，而不必向应用程序代码的其余部分公开。  例如，用于生成图形用户界面的框架可以提供 `Control` 和 `Form` 类，这两个类通过使用具有内部访问权限的成员进行合作。  由于这些成员是内部的，它们不向正在使用框架的代码公开。  
  
 从定义具有内部访问能力的类型或成员的程序集外部引用该类型或成员是错误的。  
  
## 示例  
 此示例包含两个文件：`Assembly1.cs` 和 `Assembly1`\_`a.cs`。  第一个文件包含内部基类 `BaseClass`。  在第二个文件中，实例化 `BaseClass` 的尝试将产生错误。  
  
```  
// Assembly1.cs  
// Compile with: /target:library  
internal class BaseClass   
{  
   public static int intM = 0;  
}  
```  
  
```  
// Assembly1_a.cs  
// Compile with: /reference:Assembly1.dll  
class TestAccess   
{  
   static void Main()   
   {  
      BaseClass myBase = new BaseClass();   // CS0122  
   }  
}  
```  
  
## 示例  
 在此示例中，使用与示例 1 中所用的文件相同的文件，并将 `BaseClass` 的可访问性级别更改为 `public`。  还将成员 `IntM` 的可访问性级别更改为 `internal`。  在此例中，您可以实例化类，但不能访问内部成员。  
  
```  
// Assembly2.cs  
// Compile with: /target:library  
public class BaseClass   
{  
   internal static int intM = 0;  
}  
```  
  
```  
// Assembly2_a.cs  
// Compile with: /reference:Assembly1.dll  
public class TestAccess   
{  
   static void Main()   
   {  
      BaseClass myBase = new BaseClass();   // Ok.  
      BaseClass.intM = 444;    // CS0117  
   }  
}  
```  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)