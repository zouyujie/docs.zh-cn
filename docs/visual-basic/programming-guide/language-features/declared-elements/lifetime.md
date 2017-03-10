---
title: "Visual Basic 中的生存期 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "已声明的元素, 生存期"
  - "生存期"
  - "生存期, 已声明的元素"
  - "生存期, Visual Basic"
  - "共享变量生存期"
  - "静态变量, 生存期"
  - "静态变量, Visual Basic"
ms.assetid: bd91e390-690a-469a-9946-8dca70bc14e7
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Visual Basic 中的生存期
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

已声明元素的*“生存期”*是元素可供使用的时间周期。  变量是唯一具有生存期的元素。  因此，编译器将过程参数和函数返回值视为变量的特殊情况。  变量的生存期表示它可以存储值的时间周期。  在生存期内变量的值可以更改，但变量总是存储某些值。  
  
## 不同的生存期  
 *“成员变量”*（在模块级并且在任何过程外部声明）的生存期一般与声明该变量的元素的生存期相同。  在类或结构中声明的非共享变量作为声明该变量的类或结构的每个实例的单独副本存在。  每个这样的变量的生存期都与它的实例的生存期相同。  但是，`Shared` 变量仅有一个生存期，即应用程序运行所持续的全部时间。  
  
 *“局部变量”*（在过程内部声明）仅在声明变量的过程的运行阶段存在。  这同样适用于过程的参数和任何函数返回值。  但是，如果该过程调用其他过程，则局部变量在被调用过程运行期间保留它们的值。  
  
## 生存期的开始  
 当控制进入声明局部变量的过程时，局部变量的生存期便开始了。  过程一开始运行，每个局部变量即被初始化为其数据类型的默认值。  当过程遇到指定初始值的 `Dim` 语句时，它将那些变量设置为那些值，即使代码已经给它们赋了其他值。  
  
 结构变量的每个成员被视为单独的变量初始化。  同样，数组变量的每个元素也单独初始化。  
  
 在过程内部的块中声明的变量（例如 `For` 循环）在进入过程时被初始化。  不管代码是否执行该块，这些初始化都会生效。  
  
## 生存期的结束  
 当过程终止时，不保留其局部变量的值，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将回收它们占用的内存。  下次调用该过程时，将再度创建并重新初始化它的所有局部变量。  
  
 当类或结构的实例终止时，它的非共享变量便失去它们的内存和值。  类或结构的每个新实例创建并初始化它的非共享变量。  但是，`Shared` 变量一直保留到应用程序停止运行时。  
  
## 生存期的扩展  
 如果用 `Static` 关键字声明局部变量，该变量的生存期要比其过程的执行时间长。  下表显示了过程声明如何确定 `Static` 变量存在的时间长度。  
  
|过程位置与共享|静态变量生存期开始|静态变量生存期结束|  
|-------------|---------------|---------------|  
|在模块中（默认为共享）|第一次调用过程时|当应用程序停止运行时|  
|在类中，`Shared`（过程不是实例成员）|对特定的实例或者对类或结构名称本身第一次调用过程时|当应用程序停止运行时|  
|在类的实例中，非 `Shared`（过程是实例成员）|对特定的实例第一次调用过程时|当释放实例以进行垃圾回收 \(GC\) 时|  
  
## 同名的静态变量  
 可以在多个过程中用相同的名称来声明静态变量。  如果这样做，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将每个这样的变量视为单独的元素。  初始化这些变量中的某一个不会影响其他变量的值。  这同样适用于使用一组重载来定义过程、并在每个重载中使用相同的名称声明静态变量的情况。  
  
## 静态变量的包含元素  
 可以在类中（即在该类的过程内）声明静态局部变量。  但是，不能在结构内声明静态局部变量（作为结构成员或该结构内过程的局部变量）。  
  
## 示例  
  
### 说明  
 下面的示例使用 [Static](../../../../visual-basic/language-reference/modifiers/static.md) 关键字声明变量。  （请注意，当 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 使用 `Static` 这样的修饰符时，您不需要 `Dim` 关键字。）  
  
### 代码  
 [!code-vb[VbVbalrKeywords#13](../../../../visual-basic/language-reference/codesnippet/visualbasic/lifetime_1.vb)]  
  
### 注释  
 在前面的示例中，过程 `runningTotal` 返回到调用代码后，变量 `applesSold` 继续存在。  下次调用 `runningTotal` 时，`applesSold` 保留其以前计算的值。  
  
 如果已经在不使用 `Static` 的情况下声明 `applesSold`，则调用 `runningTotal` 以后，不保留以前的累积值。  下次调用 `runningTotal` 时，将重新创建 `applesSold`，并将其初始化为 0，`runningTotal` 将只返回调用它时所用的值。  
  
### 编译代码  
 可以将静态局部变量的值初始化为其声明的一部分。  如果将数组声明为 `Static`，则可以初始化它的秩（维数）、每个维度的长度和每个元素的值。  
  
### 安全性  
 在前面的示例中，通过在模块级声明 `applesSold` 可产生相同的生存期。  但是，如果这样更改变量的范围，此过程将不再拥有对该变量的独占访问权。  由于其他过程可以访问 `applesSold` 并更改它的值，因此流量合计可能是不可靠的，并且代码可能会更难维护。  
  
## 请参阅  
 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md)   
 [Nothing](../../../../visual-basic/language-reference/nothing.md)   
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)