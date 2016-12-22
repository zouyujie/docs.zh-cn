---
title: "演练：创建和实现接口 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "接口实现, 演练"
  - "接口, 创建"
  - "接口, 测试"
  - "接口, 演练"
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 演练：创建和实现接口 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

接口描述了属性、方法和事件的特性，但是却将实现的细节留给了结构或类。  
  
 本演练将说明如何声明和实现一个接口。  
  
> [!NOTE]
>  本演练不提供有关如何以创建用户界面。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### 定义一个接口  
  
1.  打开一个新的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Windows 应用程序项目。  
  
2.  在**“项目”**菜单上，单击**“添加模块”**，向项目中添加一个新的模块。  
  
3.  将新的模块命名为 `Module1.vb`，然后单击**“添加”**。  显示该新模块的代码。  
  
4.  通过在 `Module1` 内的 `Module` 和 `End Module` 语句之间键入 `Interface TestInterface`，然后按 Enter 来定义一个名为 `TestInterface` 的接口。  **“代码编辑器”**将缩进 `Interface` 关键字并添加一个 `End Interface` 语句来形成代码块。  
  
5.  通过在 `Interface` 和 `End Interface` 语句之间放置以下代码，定义该接口的属性、方法和事件：  
  
     [!code-vb[VbVbalrOOP#98](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_1.vb)]  
  
## 实现  
 您可能注意到，用于声明接口成员的语法与用于声明类成员的语法是不同的。  这一差别反映了这样一个事实，即接口不能包含实现代码。  
  
#### 实现接口  
  
1.  将以下语句添加到 `Module1` 中的 `End Interface` 语句之后，但在 `End Module` 语句之前，然后按下 Enter，从而添加一个名为 `ImplementationClass` 的类：  
  
     [!code-vb[VbVbalrOOP#99](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_2.vb)]  
  
     如果您使用的是集成开发环境，按下 Enter 时**“代码编辑器”**将提供一条匹配的 `End Class` 语句。  
  
2.  将以下 `Implements` 语句添加到 `ImplementationClass` 中，这一操作将命名该类实现的接口：  
  
     [!code-vb[VbVbalrOOP#100](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_3.vb)]  
  
     当在类或结构顶部分别列出了其他项的 `Implements` 语句时，该语句表示类或结构将实现某个接口。  
  
     如果您使用的是集成开发环境，按下 Enter 时**“代码编辑器”**将实现 `TestInterface` 需要的类成员，然后可以跳过下一步。  
  
3.  如果您使用的不是集成开发环境，则必须实现 `MyInterface` 接口的所有成员。  将以下代码添加到 `ImplementationClass` 中以实现 `Event1`、`Method1` 和 `Prop1`：  
  
     [!code-vb[VbVbalrOOP#101](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_4.vb)]  
  
     `Implements` 语句指定要实现的接口和接口成员。  
  
4.  通过向存储属性值的类中添加一个私有字段，完成 `Prop1` 的定义：  
  
     [!code-vb[VbVbalrOOP#102](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_5.vb)]  
  
     从属性 get 访问器返回 `pval` 的值。  
  
     [!code-vb[VbVbalrOOP#103](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_6.vb)]  
  
     在属性 set 访问器中设置 `pval` 的值。  
  
     [!code-vb[VbVbalrOOP#104](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_7.vb)]  
  
5.  通过添加以下代码完成 `Method1` 的定义。  
  
     [!code-vb[VbVbalrOOP#105](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_8.vb)]  
  
#### 测试接口的实现  
  
1.  在**“解决方案资源管理器”**中，右击项目的启动窗体，再单击**“查看代码”**。  编辑器将显示启动窗体的类。  默认情况下，启动窗体称为 `Form1`。  
  
2.  将以下 `testInstance` 字段添加到 `Form1` 类中：  
  
     [!code-vb[VbVbalrOOP#120](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_9.vb)]  
  
     通过将 `testInstance` 声明为 `WithEvents`，`Form1` 类可以处理其事件。  
  
3.  将以下事件处理程序添加到 `Form1` 类中，以处理由 `testInstance` 引发的事件：  
  
     [!code-vb[VbVbalrOOP#106](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_10.vb)]  
  
4.  将一个命名为 `Test` 的子例程添加到 `Form1` 类中以测试实现类：  
  
     [!code-vb[VbVbalrOOP#107](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_11.vb)]  
  
     `Test` 过程创建实现 `MyInterface` 的类的一个实例，并将该实例赋给 `testInstance` 字段，设置一个属性，然后通过该接口运行一个方法。  
  
5.  添加代码以从启动窗体的 `Form1 Load` 过程中调用 `Test` 过程：  
  
     [!code-vb[VbVbalrOOP#108](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_12.vb)]  
  
6.  按 F5 运行 `Test` 过程。  显示消息“Prop1 was set to 9”。  单击“确定”之后，将显示消息“The X parameter for Method1 is 5”。  单击“确定”，将显示消息“The event handler caught the event”。  
  
## 请参阅  
 [Implements 语句](../../../../visual-basic/language-reference/statements/implements-statement.md)   
 [接口](../../../../visual-basic/programming-guide/language-features/interfaces/index.md)   
 [Interface 语句](../../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Event 语句](../../../../visual-basic/language-reference/statements/event-statement.md)