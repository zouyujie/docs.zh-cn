---
title: "扩展方法 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ExtensionMethods"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "扩展数据类型"
  - "扩展方法 [Visual Basic]"
ms.assetid: b8020aae-374d-46a9-bcb7-8cc2390b93b6
caps.latest.revision: 41
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 41
---
# 扩展方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过扩展方法，开发人员可以向已定义的数据类型添加自定义功能，而不用创建新的派生类型。  通过使用这些扩展方法，可以编写一个能够像调用现有类型的实例方法那样进行调用的方法。  
  
## 备注  
 扩展方法只能是 `Sub` 过程或 `Function` 过程。  您无法定义一个扩展属性、字段或事件。  所有扩展方法都必须使用 <xref:System.Runtime.CompilerServices?displayProperty=fullName> 命名空间中的扩展特性 `<Extension()>` 进行标记。  
  
 扩展方法定义中的第一个参数指定方法所扩展的数据类型。  运行方法时，第一个参数被绑定到调用该方法的数据类型的实例。  
  
## 示例  
  
### 描述  
 下面的示例定义 <xref:System.String> 数据类型的 `Print` 扩展。  该方法使用 `Console.WriteLine` 显示字符串。  `Print` 方法的参数 `aString` 将确保方法扩展 <xref:System.String> 类。  
  
 [!code-vb[VbVbalrExtensionMethods#1](./codesnippet/VisualBasic/extension-methods_1.vb)]  
  
 请注意，扩展方法定义是用扩展特性 `<Extension()>` 进行标记的。  是否对在其中定义方法的模块进行标记是可选的，但必须对模块中的每个扩展方法进行标记。  必须导入 <xref:System.Runtime.CompilerServices> 才能访问扩展特性。  
  
 扩展方法只能在模块中声明。  通常，在其中定义扩展方法的模块与在其中调用扩展方法的模块不同。  如果需要，应改为导入包含扩展方法的模块，以将其引入到范围中。  当包含 `Print` 的模块位于范围中之后，可以像调用不带参数的普通实例方法（比如 `ToUpper`）那样来调用该方法：  
  
 [!code-vb[VbVbalrExtensionMethods#2](./codesnippet/VisualBasic/extension-methods_2.vb)]  
  
 下一个示例 `PrintAndPunctuate` 同样是对 <xref:System.String> 的扩展，这次是用两个参数定义的。  第一个参数 `aString` 确保扩展方法扩展 <xref:System.String>。  第二个形参 `punc` 将用作标点符号字符串，在调用方法时以实参形式传入。  此方法显示后跟标点符号的字符串。  
  
 [!code-vb[VbVbalrExtensionMethods#3](./codesnippet/VisualBasic/extension-methods_3.vb)]  
  
 此方法是通过为 `punc` 传入字符串实参调用的：`example.PrintAndPunctuate(".")`  
  
 下面的示例演示定义和调用的 `Print` 与 `PrintAndPunctuate`。  将在定义模块中导入 <xref:System.Runtime.CompilerServices>，以便能够访问扩展特性。  
  
### 代码  
  
```vb#  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
  
    <Extension()>   
    Public Sub Print(ByVal aString As String)  
        Console.WriteLine(aString)  
    End Sub  
  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
```  
  
 接下来，将扩展方法引入到范围中并调用这些方法。  
  
```vb#  
Imports ConsoleApplication2.StringExtensions  
Module Module1  
  
    Sub Main()  
  
        Dim example As String = "Example string"  
        example.Print()  
  
        example = "Hello"  
        example.PrintAndPunctuate(".")  
        example.PrintAndPunctuate("!!!!")  
  
    End Sub  
End Module  
```  
  
### 注释  
 只要这些扩展方法或类似的扩展方法处于范围中，就可以运行它们。  如果包含扩展方法的模块处于范围中，则该模块在 IntelliSense 中可见，并且可以像调用普通实例方法那样调用该模块。  
  
 请注意，调用方法时，不会为第一个形参传递任何实参。  以前的方法定义中的参数 `aString` 被绑定到 `example`（这是调用这些方法的 `String` 的实例）。  编译器将使用 `example` 作为发送到第一个形参的实参。  
  
 如果针对设置为 `Nothing` 的对象调用扩展方法，则执行该扩展方法。  这不适用于普通实例方法。  可以显式检查扩展方法中的 `Nothing`。  
  
## 可扩展的类型  
 可以对能在 Visual Basic 参数列表中进行描述的大多数类型定义扩展方法，其中类型包括：  
  
-   类（引用类型）  
  
-   结构（值类型）  
  
-   接口  
  
-   委托  
  
-   ByRef 和 ByVal 参数  
  
-   泛型方法参数  
  
-   数组  
  
 由于第一个参数指定扩展方法所扩展的数据类型，所以它是必需的，而不能是可选的。  因此，`Optional` 参数和 `ParamArray` 参数不能是参数列表中的第一个参数。  
  
 在后期绑定中，不会考虑扩展方法。  在下面的示例中，语句 `anObject.PrintMe()` 引发 <xref:System.MissingMemberException> 异常，如果删除了第二个 `PrintMe` 扩展方法定义，您将会看到同样的异常。  
  
 [!code-vb[VbVbalrExtensionMethods#9](./codesnippet/VisualBasic/extension-methods_4.vb)]  
  
## 最佳做法  
 扩展方法提供了一种方便有效的方式来扩展现有类型。  但是，若要成功使用这些扩展方法，有几点需要注意的地方。  这些注意事项主要适用于类库的作者，但它们可能会影响任何使用扩展方法的应用程序。  
  
 大多数情况下，添加到不属于您的类型的扩展方法比添加到由您控制的类型的扩展方法更易受到攻击。  在不属于您的类中可能会存在许多能够影响扩展方法的内容。  
  
-   如果存在签名与调用语句中的实参兼容的任何可访问的实例成员，并且不需要从实参向形参进行收缩转换，则与任何扩展方法相比，将优先使用实例方法。  因此，如果在某个点将相应的实例方法添加到类中，则所依赖的现有扩展成员可能变得无法访问。  
  
-   原先的扩展方法作者无法阻止其他程序员编写比他的扩展方法优先的冲突扩展方法。  
  
-   可以通过将扩展方法放置在它们自己的命名空间中来增强可靠性。  之后，您的库使用者可以从库的其余部分包含或排除某个命名空间，也可以在多个命名空间中进行选择。  
  
-   扩展接口可能比扩展类更安全，尤其是当您不拥有该接口或类时。  接口更改将影响实现该接口的每一个类。  因此，作者不大可能在接口中添加或更改方法。  但是，如果类实现两个接口，并且它们包含具有相同签名的扩展方法，则这两个扩展方法都不可见。  
  
-   扩展可以扩展的最具体的类型。  在类型层次结构中，如果选择一个从中派生许多其他类型的类型，则很可能将引入实例方法或那些可能会影响您的扩展方法的其他扩展方法。  
  
## 扩展方法、实例方法和属性  
 当范围内实例方法的签名与调用语句的实参兼容时，则与任何扩展方法相比，将优先选择该实例方法。  即使扩展方法匹配性更高，也优先选择该实例方法。  在下面的示例中，`ExampleClass` 包含一个名为 `ExampleMethod` 的实例方法，该方法具有一个类型为 `Integer` 的形参。  扩展方法 `ExampleMethod` 扩展 `ExampleClass`，并且具有一个类型为 `Long` 的形参。  
  
 [!code-vb[VbVbalrExtensionMethods#4](./codesnippet/VisualBasic/extension-methods_5.vb)]  
  
 在下面的代码中，对 `ExampleMethod` 的第一次调用将调用扩展方法，因为 `arg1` 为 `Long`，并且仅与扩展方法中的 `Long` 形参兼容。  对 `ExampleMethod` 的第二次调用具有一个 `Integer` 实参 `arg2`，它将调用实例方法。  
  
 [!code-vb[VbVbalrExtensionMethods#5](./codesnippet/VisualBasic/extension-methods_6.vb)]  
  
 现在反转这两个方法中的形参的数据类型：  
  
 [!code-vb[VbVbalrExtensionMethods#6](./codesnippet/VisualBasic/extension-methods_7.vb)]  
  
 这一次，`Main` 中的代码两次都调用实例方法。  这是因为 `arg1` 和 `arg2` 都可以扩大转换为 `Long`，并且在这两种情况下实例方法都优先于扩展方法。  
  
 [!code-vb[VbVbalrExtensionMethods#7](./codesnippet/VisualBasic/extension-methods_8.vb)]  
  
 因此，扩展方法不能替换现有的实例方法。  但是，如果扩展方法与实例方法的名称相同，但签名不冲突，则可以访问这两个方法。  例如，如果类 `ExampleClass` 包含一个名为 `ExampleMethod` 且不带参数的方法，则允许使用具有相同名称和不同签名的扩展方法，如下面的代码所示。  
  
 [!code-vb[VbVbalrExtensionMethods#8](./codesnippet/VisualBasic/extension-methods_9.vb)]  
  
 此代码的输出如下所示：  
  
 `Extension method`  
  
 `Instance method`  
  
 对于属性，情况要简单一些：如果扩展方法具有与它扩展的类的属性相同的名称，则扩展方法不可见且无法访问。  
  
## 扩展方法优先级  
 如果两个具有相同签名的扩展方法都处于范围中且都可以访问，则将调用优先级较高的扩展方法。  扩展方法的优先级基于用于将方法引入到范围中的机制。  以下列表由高至低显示了优先级层次结构。  
  
1.  在当前模块内定义的扩展方法。  
  
2.  在当前命名空间或其任何一个父命名空间（其中子命名空间的优先级比父命名空间的优先级高）中的数据类型内定义的扩展方法。  
  
3.  在当前文件的任何类型导入内定义的扩展方法。  
  
4.  在当前文件的任何命名空间导入内定义的扩展方法。  
  
5.  在任何项目级类型导入内定义的扩展方法。  
  
6.  在任何项目级命名空间导入内定义的扩展方法。  
  
 如果优先级不能确定要调用哪个方法，则可以使用完全限定名来指定将要调用的方法。  如果在名为 `StringExtensions` 的模块中定义了先前示例中的 `Print` 方法，则完全限定名是 `StringExtensions.Print(example)`，而不是 `example.Print()`。  
  
## 请参阅  
 <xref:System.Runtime.CompilerServices>   
 <xref:System.Runtime.CompilerServices.ExtensionAttribute>   
 [扩展方法](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [Module 语句](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)