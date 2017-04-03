---
title: "Main() 和命令行自变量（C# 编程指南）| Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- CS5001
- main_CSharpKeyword
- Main
dev_langs:
- CSharp
helpviewer_keywords:
- Main method [C#]
- C# language, command-line arguments
- arguments [C#], command-line
- command line [C#], arguments
- command-line arguments [C#], Main method
ms.assetid: 73a17231-cf96-44ea-aa8a-54807c6fb1f4
caps.latest.revision: 30
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
ms.openlocfilehash: f6934a09c5f980f845e19b28e462cc601e154512
ms.lasthandoff: 03/13/2017

---
# <a name="main-and-command-line-arguments-c-programming-guide"></a>Main() 和命令行参数（C# 编程指南）
`Main` 方法是 C# 控制台应用程序或 Windows 应用程序的入口点 （库和服务不要求使用 `Main` 方法作为入口点）。 `Main` 方法是应用程序启动后调用的第一个方法。  
  
 C# 程序中只能有一个入口点。 如果多个类包含 `Main` 方法，必须使用 **/main** 编译器选项来编译程序，以指定将哪个 `Main` 方法用作入口点。 有关详细信息，请参阅 [/main（C# 编译器选项）](../../../csharp/language-reference/compiler-options/main-compiler-option.md)。  
  
 [!code-cs[csProgGuideMain#17](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-and-command-line-arguments_1.cs)]  
  
## <a name="overview"></a>概述  
  
-   `Main` 方法是 .exe 程序的入口点，也是程序控制开始和结束的位置。  
  
-   `Main` 在类或结构中声明。 `Main` 必须是[静态](../../../csharp/language-reference/keywords/static.md)方法，不得为[公共](../../../csharp/language-reference/keywords/public.md)方法 （在前面的示例中，它获得的是[私有](../../../csharp/language-reference/keywords/private.md)成员的默认访问权限）。封闭类或结构不一定要是静态的。  
  
-   `Main` 的返回类型可以是 `void` 或 `int`。  
  
-   使用或不使用包含命令行自变量的 `string[]` 参数声明 `Main` 方法都行。 使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 创建 Windows 窗体应用程序时，可以手动添加此参数，也可以使用 <xref:System.Environment> 类来获取命令行自变量。 参数被读取为从零开始编制索引的命令行自变量。 与 C 和 C++ 不同，程序的名称不被视为第一个命令行自变量。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [命令行参数](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)  
  
-   [如何：显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)  
  
-   [如何：使用 foreach 访问命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)  
  
-   [Main() 返回值](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [使用 csc.exe 通过命令行生成内容](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [C# 程序内部探究](../../../csharp/programming-guide/inside-a-program/index.md)   
 [\<paveover>C# 示例应用程序](http://msdn.microsoft.com/en-us/9a9d7aaa-51d3-4224-b564-95409b0f3e15)
