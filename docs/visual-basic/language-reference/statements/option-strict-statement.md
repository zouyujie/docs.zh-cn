---
title: "Option Strict 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Strict"
  - "vb.OptionStrict"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "转换, implicit"
  - "隐式转换"
  - "后期绑定"
  - "Option Strict 语句"
  - "Strict 关键字"
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
caps.latest.revision: 49
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 49
---
# Option Strict 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使隐式数据类型转换仅限于进行扩大转换，禁止后期绑定，并禁止生成 `Object` 类型的隐式键入。  
  
## 语法  
  
```  
Option Strict { On | Off }  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`On`|可选。  启用 `Option Strict` 检查。|  
|`Off`|可选。  禁用 `Option Strict` 检查。|  
  
## 备注  
 当 `Option Strict On` 或 `Option Strict` 出现在文件中时，以下情况将导致编译时错误：  
  
-   隐式收缩转换  
  
-   后期绑定  
  
-   在 `Object` 类型中隐式键入结果  
  
> [!NOTE]
>  在您可在 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 上设置的警告配置中，存在与导致编译时错误的条件相对应的三种设置。  关于如何使用这些设置，请参见本主题后面的 [在 IDE 中设置警告配置](../../../visual-basic/language-reference/statements/option-strict-statement.md#conditions)。  
  
 `Option Strict Off` 语句为所有三种情况关闭错误和警告检查，即使关联的 IDE 设置指定要打开这些错误或警告。  `Option Strict On` 语句打开检查所有三个条件的错误和警告，因此，即使关联的 IDE 设置指定关闭这些错误或警告。  
  
 如果使用 `Option Strict` 语句，则它必须在文件中出现在任何其他源代码语句之前。  
  
 当您将 `Option Strict` 到 `On`时， Visual Basic 检查数据类型对于所有程序元素指定。  使用局部类型推断，数据类型可以显式指定或指定。  指定数据类型所有编程元素的由于下列原因，建议:  
  
-   它为变量和参数启用 IntelliSense 支持。  这可让您在键入代码时看到变量的属性和其他成员。  
  
-   启用编译器执行类型检查。  类型检查有助于您找到可以在运行时因类型转换错误而失败的语句。  它还标识对不支持这些方法的对象上的方法的调用。  
  
-   它加快代码的执行。  其中一个原因是，如果不为编程元素指定数据类型， Visual Basic 编译器将其分配 `Object` 类型。  生成代码可能需要来回转换在 `Object` 和其他数据类型之间，降低性能。  
  
## 隐式收缩转换错误  
 当存在为收缩转换的隐式数据类型转换时，出现隐式收缩转换错误。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 可将许多数据类型转换为其他数据类型。  在将一种数据类型的值转换为另一种精度较低或容量较小的数据类型时，可能发生数据丢失。  如果此类“收缩转换”失败，则会发生运行时错误。  `Option Strict` 确保可为这些收缩转换提供编译时通知，从而可避免这种错误。  有关更多信息，请参见[隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)和 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
 会导致错误的转换包括表达式中发生的隐式转换。  有关更多信息，请参见下列主题：  
  
-   [\+ 运算符](../../../visual-basic/language-reference/operators/addition-operator.md)  
  
-   [\+\= 运算符](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)  
  
-   [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md)  
  
-   [\/\= 运算符](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)  
  
-   [Char 数据类型](../../../visual-basic/language-reference/data-types/char-data-type.md)  
  
 当您通过使用 [& 运算符](../../../visual-basic/language-reference/operators/concatenation-operator.md) 连接字符串时，所有转换为字符串被都认为会扩大。  即使在 `Option Strict` 开启时，这样的转换也不会产生隐形收缩转换错误。  
  
 当您调用了具有不同于相应参数的数据类型的参数的方法时，进行收缩转换会导致编译时错误（如果 `Option Strict` 处于开启状态）。  可以通过使用扩大转换或显式转换避免编译时错误。  
  
 在编译从 `For Each…Next` 集合中的元素到循环控制变量的转换时，禁止显示隐式收缩转换错误。  即使 `Option Strict` 处于开启状态，也将发生这种情况。  更多信息，请参见 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 中的“收缩转换”一节。  
  
## 后期绑定错误  
 如果某个对象被分配给声明为 `Object` 类型的变量的属性或方法，该对象就是后期绑定的。  有关更多信息，请参见 [早期绑定和后期绑定](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)。  
  
## 隐式对象类型错误  
 适当的类型无法推断为已声明的变量时出现隐式对象类型错误，因此将推断 `Object` 类型。  这主要发生在您使用 `Dim` 语句（而不使用 `As` 子句）声明一个变量，并且 `Option Infer` 处于关闭状态的情况。  有关更多信息，请参见 [Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md) 和 [Visual Basic 语言规范](../../../visual-basic/reference/language-specification.md)。  
  
 对于方法参数，如果`Option Strict` 是关闭的则 `As` 子句为可选项。  但是，如果任何一个参数使用 `As` 子句，则所有参数都必须使用。  如果 `Option Strict` 开启，则每个参数定义都需要  `As` 子句。  
  
 如果您在不使用 `As` 子句的情况下声明一个变量，并将其设置为 `Nothing`，则变量将具有 `Object` 类型。  在 `Option Strict` 为 On 以及 `Option Infer` 为 On 这种情况下，不会出现任何编辑时错误。  其示例为 `Dim something = Nothing`。  
  
### 默认数据类型和值  
 下表描述了在 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md) 中指定数据类型和初始值设定项的各种组合的结果。  
  
|||||  
|-|-|-|-|  
|是否指定数据类型？|是否指定初始值设定项？|示例|结果|  
|否|否|`Dim qty`|如果 `Option Strict` 为 off（默认），则变量将设置为 `Nothing`。<br /><br /> 如果 `Option Strict` 为 on，则会发生编译时错误。|  
|否|是|`Dim qty = 5`|如果 `Option Infer` 为 on（默认），则该变量采用初始值设定项的数据类型。  请参见 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。<br /><br /> 如果 `Option Infer` 处于关闭状态，并且 `Option Strict` 处于关闭状态，则该变量采用 `Object` 数据类型。<br /><br /> 如果 `Option Infer` 为 off，并且 `Option Strict` 为 on，则会发生编译时错误。|  
|是|否|`Dim qty As Integer`|变量初始化为数据类型的默认值。  有关更多信息，请参见 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。|  
|是|是|`Dim qty  As Integer = 5`|如果初始值设定项的数据类型不能转换为指定的数据类型，将发生编译时错误。|  
  
## 当 Option Strict 语句不存在时  
 如果源代码中不包含 `Option Strict` 语句，则使用 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 上的**Option strict**设置。  **“编译页”**包含提供额外控件设置，该控件针对产生错误的条件。  
  
 如果您要使用命令行编译器，则可使用 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md) 编译器选项指定 `Option Strict` 设置。  
  
### 在 IDE 中设置 Option Strict  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  在**“编译”**选项卡上，设置**“Option Strict”**框中的值。  
  
###  <a name="conditions"></a> 在 IDE 中设置警告配置  
 使用[“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 代替 `Option Strict` 语句时，可以对生成错误的情况实行附加控制。  **“编译页面”**的**“警告配置”**有与 `Option Strict` 开启时引起编译时间错误的三种情况相对应的设置。  这些设置如下：  
  
-   **隐式转换**  
  
-   **后期绑定；调用在运行时可能失败**  
  
-   **隐式类型；假定的对象**  
  
 将**“选项严格”**设置为**“开启”**时，所有这三个警告配置设置都将被设置为**“错误”**。  将**“选项严格”**设置为**“关闭”**时，所有这三个设置都被设置为**“无”**。  
  
 可单独将各警告配置设置更改为**“无”**、**“警告”**或**“错误”**。  如果三个警告配置都设置为 **出错**，则 `On` 会出现在 `Option strict` 框中。  如果三个都设置为 **无**，则 `Off` 会出现在此框中。  对于这些配置的任何其他组合，显示 **“（自定义）”**。  
  
### 要设置新项目的“选项严格”默认设置  
 创建项目时，**“编译”**选项卡上的**“选项严格”**设置将在**“选项”**对话框中设置为**“选项严格”**设置。  
  
 若要在此对话框设置 `Option Strict`，请在**工具**菜单上单击**选项**。  在**“选项”**对话框中展开**“项目和解决方案”**，然后单击**“VB 默认值”**。  **“VB 默认值”**中的初始默认值设置为 `Off`。  
  
### 在命令行中设置“Option Strict”  
 将 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md) 编译器选项包括在 **vbc** 命令中。  
  
## 示例  
 以下示例演示收缩转换的隐型转换引起的编译时错误。  这类错误对应于“编译页”上的“隐式转换”条件。  
  
 [!code-vb[VbVbalrStatements#161](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/option-strict-statement_1.vb)]  
  
## 示例  
 以下示例演示了一个后期绑定引起的编译时错误。  这类错误对应于“编译页”上的“后期绑定；运行时调用可能失败”条件。  
  
 [!code-vb[VbVbalrStatements#162](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/option-strict-statement_2.vb)]  
  
## 示例  
 以下示例演示声明为 `Object` 类型的变量引起的错误。  这类错误对应于“编译页”上的“隐式类型；对象假设”条件。  
  
 [!code-vb[VbVbalrStatements#163](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/option-strict-statement_3.vb)]  
  
 [!code-vb[VbVbalrStatements#164](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/option-strict-statement_4.vb)]  
  
## 请参阅  
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)   
 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [如何：访问对象的成员](../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Office 解决方案中的后期绑定](/office-dev/office-dev/late-binding-in-office-solutions)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [“选项”对话框 \-\>“项目”\-\>“Visual Basic 默认值”](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)