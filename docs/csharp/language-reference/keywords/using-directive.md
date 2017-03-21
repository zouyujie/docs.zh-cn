---
title: "using 指令（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "using 指令 [C#]"
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# using 指令（C# 参考）
`using` 指令有三种用途：  
  
-   允许在命名空间中使用类型，这样无需在该命名空间中限定某个类型的使用：  
  
    ```c#  
    using System.Text;  
    ```  
  
-   允许访问类型的静态成员，而无需限定使用类型名称进行访问：  
  
    ```c#  
    using static System.Math;  
    ```  
  
-   为命名空间或类型创建别名。  这称为 *using 别名指令*。  
  
    ```c#  
    using Project = PC.MyCompany.Project;  
    ```  
  
 `using` 关键字还用于创建 *using 语句*，此类语句有助于确保正确处理 <xref:System.IDisposable> 对象（如文件和字体）。  有关详细信息，请参阅 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)。  
  
## Using Static 类型  
 你可以访问类型的静态成员，而无需限定使用类型名称进行访问：  
  
```c#  
using static System.Console;   
using static System.Math;  
class Program   
{   
    static void Main()   
    {   
        WriteLine(Sqrt(3*3 + 4*4));   
    }   
}  
  
```  
  
 `Using static` 仅导入可访问的静态成员和指定类型中声明的嵌套类型。  不导入继承的成员。  可以从任何带 using static 指令的已命名类型导入，包括 Visual Basic 模块。  如果 F\# 顶级函数在元数据中显示为一个已命名类型（其名称是有效的 C\# 标识符）的静态成员，则可以导入该 F\# 函数。  
  
 `Using static` 使指定类型中声明的扩展方法可用于扩展方法查找。  但是，扩展方法的名称不导入到代码中非限定引用的作用域中。  
  
 同一编译单元或命名空间中通过不同 using static 命令从不同类型导入的具有相同名称方法组成一个方法组。  这些方法组内的重载解决方法遵循一般 C\# 规则。  
  
## 备注  
 `using` 指令的范围限于显示它的文件。  
  
 创建 `using` 别名，以便更易于将标识符限定为命名空间或类型。  using 别名指令的右侧必须始终是一个完全限定类型，而与前面的 using 指令无关。  
  
 创建 `using` 指令，以便在命名空间中使用类型而不必指定命名空间。  `using` 指令不为你提供对嵌套在指定命名空间中的任何命名空间的访问权限。  
  
 命名空间分为两类：用户定义的命名空间和系统定义的命名空间。  用户定义的命名空间是在代码中定义的命名空间。  有关系统定义的命名空间的列表，请参阅 [.NET Framework 类库](http://go.microsoft.com/fwlink/?LinkID=227195)。  
  
 有关引用其他程序集中的方法的示例，请参阅[创建和使用 C\# DLL](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 示例 1  
  
### 说明  
 下面的示例显示如何为命名空间定义和使用 `using` 别名：  
  
### 代码  
 [!code-cs[csrefKeywordsNamespace#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_1.cs)]  
  
### 批注  
 using 别名指令的右侧不能有开放式泛型类型。  例如，不能为 List\<T\> 创建 using 别名，但可以为 List\<int\> 创建。  
  
## 示例 2  
  
### 说明  
 下面的示例显示如何为类定义 `using` 指令和 `using` 别名：  
  
### 代码  
 [!code-cs[csrefKeywordsNamespace#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [使用命名空间](../../../csharp/programming-guide/namespaces/using-namespaces.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [命名空间](../../../csharp/programming-guide/namespaces/index.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)