---
title: "Visual Basic 的新增功能 | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- VB.StartPage.WhatsNew
dev_langs:
- VB
helpviewer_keywords:
- new features, Visual Basic
- what's new [Visual Basic]
- Visual Basic, what's new
ms.assetid: d7e97396-7f42-4873-a81c-4ebcc4b6ca02
caps.latest.revision: 145
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 55cf69a06a047c12f027007ed7180bf74307f2c9
ms.lasthandoff: 03/13/2017

---
# <a name="whats-new-for-visual-basic"></a>Visual Basic 的新增功能
此页列出每个 Visual Basic 版本的重要功能名以及该语言最新版本中的新功能和增强功能的说明。  
  
## <a name="previous-versions"></a>早期版本  
 Visual Basic/Visual Studio .NET 2002  
 首次发布  
  
 Visual Basic/Visual Studio .NET 2003  
 移位运算符、循环变量声明  
  
 Visual Basic/Visual Studio .NET 2005  
 `My` 类型和帮助程序类型（对应用程序、计算机、文件系统、网络的访问）  
  
 Visual Basic/Visual Studio .NET 2008  
 语言集成查询 (LINQ)、XML 文本、本地类型推断、对象初始值设定项、匿名类型、扩展方法、本地 `var` 类型推断、lambda 表达式、`if` 运算符、分部方法、可以为 null 的值类型  
  
 Visual Basic、Visual Studio .NET 2010  
 自动实现的属性、集合初始值设定项、隐式行继续符、动态、泛型协变/逆变、全局命名空间访问  
  
 Visual Basic/Visual Studio .NET 2012  
 `Async` / `await`、迭代器、调用方信息特性  
  
 Visual Basic/Visual Studio .NET 2013  
 .NET Compiler Platform (“Roslyn”) 的技术预览  
  
 Visual Basic/Visual Studio .NET 2015  
 当前版本，请参阅下文  
  
## <a name="current-version"></a>当前版本  
 [Nameof](../../csharp/language-reference/keywords/nameof.md)  
 可以在错误消息中使用类型或成员的非限定字符串名，而无需对字符串进行硬编码。  这使代码可以在重构时保持正确。  此功能也可用于挂接“模型-视图-控制器”MVC 链接并触发属性更改事件。  
  
 [字符串内插](../../csharp/language-reference/keywords/interpolated-strings.md)  
 可以使用字符串内插表达式构造字符串。  内插字符串表达式类似于包含表达式的模板字符串。  与[复合格式设置](../../standard/base-types/composite-format.md)相比，内插字符串在自变量方面更易于理解。  
  
 [Null 条件成员访问和索引编制](../../csharp/language-reference/operators/null-conditional-operators.md)  
 可以在执行成员访问 (`?.`) 或索引 (`?[]`) 操作之前以非常轻量的语法方式测试是否存在 null。  这些运算符可帮助编写更少的代码来处理 null 检查，尤其是对于下降到数据结构。  如果左操作数或对象引用为 null，则操作会返回 null。  
  
 [多行字符串](../../visual-basic/programming-guide/language-features/strings/string-basics.md)  
 字符串可以包含换行符序列。  不再需要使用 `<xml><![CDATA[...text with newlines...]]></xml>.Value` 这种旧的解决方法  
  
 注释  
 可以在隐式行继续符之后、初始值设定项表达式内部以及 LINQ 表达式项之间放置注释。  
  
 更智能的完全限定名称解析  
 如果提供了 `Threading.Thread.Sleep(1000)` 这类代码，Visual Basic 过去会查找命名空间“Threading”，发现它在 System.Threading 与 System.Windows.Threading 混淆，然后报告错误。  Visual Basic 现在将这两个可能的命名空间结合在一起进行考虑。  如果显示完成列表，则 Visual Studio 编辑器会在完成列表中列出这两种类型中的成员。  
  
 以年份开头的日期文本  
 可以使用 yyyy-mm-dd 格式的日期文本 `#2015-03-17 16:10 PM#`。  
  
 只读接口属性  
 可以使用读写属性实现只读接口属性。  该接口可保证最小功能，不会阻止实现类允许设置属性。  
  
 [TypeOf \<表达式> IsNot \<类型>](../../visual-basic/language-reference/operators/typeof-operator.md)  
 为提高代码的可读性，现在可以将 `TypeOf` 与 `IsNot` 一起使用。  
  
 [#Disable Warning \<ID> 和 #Enable Warning \<ID>](../../visual-basic/language-reference/directives/directives.md)  
 可以对源文件中的区域禁用和启用特定警告。  
  
 XML 文档注释改进  
 编写文档注释时，可获取智能编辑器和生成支持，以用于验证参数名、正确处理 `crefs`（泛型、运算符等）、着色和重构。  
  
 [部分模块和接口定义](../../visual-basic/language-reference/modifiers/partial.md)  
 除了类和结构之外，还可以声明部分模块和接口。  
  
 [方法体中的 #Region 指令](../../visual-basic/language-reference/directives/region-directive.md)  
 可以将 #Region…#End Region 限定符放置在文件中、函数内部甚至是跨越函数体的任何位置。  
  
 [替代定义是隐式重载](../../visual-basic/language-reference/modifiers/overrides.md)  
 如果你向定义添加 `Overrides` 修饰符，则编译器会隐式添加 `Overloads`，以便你可以在常见情况下输入更少的代码。  
  
 特性参数中允许使用 CObj  
 当 CObj(...) 在特性构造中使用时，编译器过去会发出错误，指出它不是常量。  
  
 从不同接口声明和使用不明确的方法  
 以下代码以前会生成错误，从而阻止你声明 `IMock` 或调用 `GetDetails`（如果这些内容已在 C# 中声明）：  
  
```vb  
Interface ICustomer  
  Sub GetDetails(x As Integer)  
End Interface  
  
Interface ITime  
  Sub GetDetails(x As String)  
End Interface  
  
Interface IMock : Inherits ICustomer, ITime  
  Overloads Sub GetDetails(x As Char)  
End Interface  
  
Interface IMock2 : Inherits ICustomer, ITime  
End Interface  
  
```  
  
 现在，编译器会使用正常的重载决策规则来选择最合适的 `GetDetails` 进行调用，你可以在 Visual Basic 中声明接口关系（如示例中所示的这些关系）。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 2017 中的新增功能](https://docs.microsoft.com/en-us/visualstudio/ide/whats-new-in-visual-studio)
