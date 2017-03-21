---
title: "Delegate 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Delegate"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "delegate 关键字"
  - "Delegate 语句"
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# Delegate 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用于声明委托。  委托是一种引用类型，它引用类型的 `Shared` 方法或对象的实例方法。  任何具有匹配参数和返回类型的过程都可用于创建此委托类的实例。  然后就可以通过委托实例来调用过程。  
  
## 语法  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`attrlist`|可选。  应用于此委托的特性列表。  多个特性以逗号分隔。  [特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)必须用尖括号（“`<`”和“`>`”）括起来。|  
|`accessmodifier`|可选。  指定哪些代码可以访问此委托。  可以是如下内容之一：<br /><br /> -   [公共](../../../visual-basic/language-reference/modifiers/public.md)。  可以访问声明委托的元素的任何代码都可以访问该委托。<br />-   [受保护](../../../visual-basic/language-reference/modifiers/protected.md)。  只有委托的类或派生类中的代码可以访问该委托。<br />-   [友元](../../../visual-basic/language-reference/modifiers/friend.md)。  只有同一程序集中的代码可以访问该委托。<br />-   [私有](../../../visual-basic/language-reference/modifiers/private.md)。  只有声明委托的元素内的代码可以访问该委托。<br /><br /> 您可以指定 `Protected Friend`，以便可以从委托类、派生类或同一程序集中的代码进行访问。|  
|`Shadows`|可选。  指定此委托重新声明并隐藏基类中的同名编程元素或重载元素集。  可以用其他任何类型的元素来隐藏任何类型的被声明元素。<br /><br /> 对于被隐藏的元素来说，从隐藏该元素的派生类无法使用它，除非是从不能访问隐藏元素的位置进行访问。  例如，如果 `Private` 元素隐藏一个基类元素，则无权访问 `Private` 元素的代码会改为访问基类元素。|  
|`Sub`|可选项，但是 `Sub` 或 `Function` 必须出现。  将此过程声明为不返回值的委托 `Sub` 过程。|  
|`Function`|可选项，但是 `Sub` 或 `Function` 必须出现。  将此过程声明为返回值的委托 `Function` 过程。|  
|`name`|必选。  委托类型的名称；符合标准变量命名规则。|  
|`typeparamlist`|可选。  此委托的类型参数列表。  以逗号分隔多个类型参数。  （可选）可以使用 `In` 和 `Out` 泛型修饰符将每个类型参数声明为 Variant。  必须将[类型列表](../../../visual-basic/language-reference/statements/type-list.md)用括号括起来，并用 `Of` 关键字引入。|  
|`parameterlist`|可选。  调用过程时传递给过程的参数列表。  必须将 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md) 用括号括起来。|  
|`type`|在您指定 `Function` 过程时必选。  返回值的数据类型。|  
  
## 备注  
 `Delegate` 语句定义委托类的参数和返回类型。  任何具有匹配参数和返回类型的过程都可用于创建此委托类的实例。  然后就可以调用委托的 `Invoke` 方法，通过委托实例调用此过程。  
  
 可以在命名空间、模块、类或结构级别声明委托，但不能在过程内声明。  
  
 每个委托类都定义一个被传递对象方法规范的构造函数。  委托构造函数的参数必须是对方法或 lambda 表达式的引用。  
  
 若要指定对方法的引用，请使用下面的语法：  
  
 `AddressOf` \[`expression`.\]`methodname`  
  
 `expression` 的编译时类型必须是类或接口的名称，而该类或接口包含签名与委托类的签名相匹配的指定名称的方法。  `methodname` 可以是共享方法，也可以是实例方法。  即使为类的默认方法创建了委托，`methodname` 也不是可选项。  
  
 若要指定 lambda 表达式，请使用下面的语法：  
  
 `Function` \(\[`parm` As `type`, `parm2` As `type2`, ...\]\) `expression`  
  
 函数的签名必须与委托类型的签名相匹配。  有关 lambda 表达式的更多信息，请参见 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 有关委托的更多信息，请参见[委托](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)。  
  
## 示例  
 下面的示例使用 `Delegate` 语句声明一个委托，对两个数字进行运算并返回一个数字。  `DelegateTest` 方法将获取此类型委托的实例，并使用该实例对两个数字进行运算。  
  
 [!code-vb[VbVbalrDelegates#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegate-statement_1.vb)]  
  
## 请参阅  
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [如何：使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)