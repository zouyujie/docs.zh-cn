---
title: "已声明的元素名称 (Visual Basic) | Microsoft Docs"
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
  - "[] 转义字符 [Visual Basic]"
  - "区分大小写, 已声明的元素名称"
  - "声明语句, 已声明的元素"
  - "声明, 元素"
  - "已声明的元素, 关于声明的元素"
  - "已声明的元素, 区分大小写"
  - "已声明的元素, 标识符"
  - "已声明的元素, 名称"
  - "已声明的元素, 有效名称"
  - "声明元素"
  - "元素名称"
  - "转义字符"
  - "转义名称"
  - "标识符, 已声明的元素"
  - "标识符, 元素"
  - "名称, 已声明的元素"
  - "名称, 元素"
  - "名称, 命名规则"
  - "名称, Visual Basic 规则"
  - "命名规则"
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# 已声明的元素名称 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

每个已声明的元素都有名称（也称为“*标识符”）*，代码就是用这些名称来引用已声明的元素。  
  
## 规则  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的元素名称必须遵循下列规则：  
  
-   必须以字母或下划线 \(`_`\) 开头。  
  
-   必须只包含字母、十进制数字和下划线。  
  
-   如果名称以下划线开头，则必须包含至少一个字母或十进制数字。  
  
-   长度不能超过 1023 个字符。  
  
 1023 个字符的长度限制还适用于完全限定名的整个字符串，如 `outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement`。  
  
 下面的示例演示一些有效的元素名称。  
  
 `aB123__45`  
  
 `_567`  
  
 下面的示例演示一些无效的元素名称。  第一个名称仅包含一个下划线，第二个名称以十进制数字开头，第三个名称包含一个无效字符 \($\)。  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
>  以下划线 \(`_`\) 开始的元素名称不是 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\) 的组成部分，因此符合 CLS 的代码不能使用定义这类元素名称的组件。  但是，元素名称中任何其他位置的下划线都是符合 CLS 的。  
  
### 名称长度原则  
 在实际使用时，应该使名称尽可能地短，但仍然能够清楚地标识元素的性质。  这样就会提高代码的可读性，并减小行的长度和源文件大小。  
  
 另一方面，名称不应该太短，以致于不足以描述元素所表示的内容和代码使用它的方式。  这对于代码的可读性是很重要的。  如果他人尝试理解您的代码，或者您自己在编写它很长时间之后查看它，适当元素名称可以节省相当多的时间。  
  
## 转义名称  
 通常，元素名不得与 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 的任何保留关键字匹配，如 `Case` 或 `Friend`。  但是，可以定义用中括号 \(`[ ]`\) 括起来的“转义名称”。  由于中括号消除了所有的多义性，因此转义名称可以与任何 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 关键字匹配。  以后在代码中引用该名称时同样使用中括号。  
  
 通常，应仅在下列情况下使用转义名称：  
  
-   您的代码是从 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 的先前版本迁移而来，而该版本没有保留用作名称的关键字；或者  
  
-   您使用的代码是用另一种语言编写的，该语言不保留给定关键字。  
  
 否则，如果元素的名称与关键字冲突，则应该考虑重命名该元素。  集成开发环境 \(IDE\) 提供了一种重命名元素的简单方法。  有关更多信息，请参见 [重构和“重命名”对话框](../../../../visual-basic/developing-apps/using-ide/refactoring-and-rename-dialog-box.md)。  
  
## 名称的大小写敏感性  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的元素名称不区分大小写。  这意味着编译器在比较两个只有字母大小写不同的名称时，将它们解释为相同的名称。  例如，它将 `ABC` 和 `abc` 视为相同的已声明元素。  
  
 但是，公共语言运行时 \(CLR\) 使用区分大小写的绑定。  因此，当生成程序集或 DLL 并使其可用于其他程序集时，名称将不再是不区分大小写的。  例如，如果用名为 `ABC` 的元素定义某个类，并且其他程序集通过公共语言运行时使用该类，则它们必须用 `ABC` 来引用此元素。  如果以后要重新编译该类并将此元素的名称更改为 `abc`，则其他使用该类的程序集将无法再访问此元素。  因此，在发布程序集的更新版本时，不能更改任何公共元素的字母大小写。  
  
## 名称和区域设置  
 名称的比较与区域设置无关。  如果两个名称在一个区域设置中是匹配的，则它们在所有区域设置中都一定是匹配的。  
  
## 请参阅  
 [已声明的元素](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)   
 [已声明元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [语句](../../../../visual-basic/language-reference/statements/index.md)