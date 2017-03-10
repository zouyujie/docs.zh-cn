---
title: "演练：定义类 (Visual Basic) | Microsoft Docs"
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
  - "类模块, 演练"
  - "类 [Visual Basic], 演练"
  - "代码, 退出"
  - "执行, 结束"
  - "执行, stopping"
  - "文件, 关闭"
  - "Initialize 事件"
  - "对象 [Visual Basic], 创建"
  - "对象 [Visual Basic], 初始化"
  - "程序终止"
  - "程序, 退出"
  - "Terminate 事件"
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 演练：定义类 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此演练演示如何定义类，然后使用这些类创建对象。  同时还说明如何为新类添加属性和方法，并演示如何初始化对象。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 定义类  
  
1.  单击**“文件”**菜单上的**“新建项目”**，创建一个项目。  此时将出现**“新建项目”**对话框。  
  
2.  从 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 项目模板列表中选择“Windows 应用程序”，以显示新项目。  
  
3.  在**“项目”**菜单中单击**“添加类”**，将一个新类添加到项目中。  将显示**“添加新项”**对话框。  
  
4.  选择**“类”**模板。  
  
5.  给新类 `UserNameInfo.vb` 命名，然后单击**“添加”**以显示新类的代码。  
  
     [!code-vb[VbVbalrOOP#5](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#5)]  
  
    > [!NOTE]
    >  可以使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]**“代码编辑器”**，在新类的名称之前键入 `Class` 关键字，将类添加到启动窗体中。  **“代码编辑器”**会提供相应的 `End Class` 语句。  
  
6.  在 `Class` 和 `End Class` 语句之间添加以下代码，为类定义一个私有字段：  
  
     [!code-vb[VbVbalrOOP#7](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#7)]  
  
     将字段声明为 `Private` 意味着该字段只能在该类内使用。  使用能够提供更多访问权限的访问修饰符（如 `Public`），便可以从类的外部访问这些字段。  有关更多信息，请参见 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
7.  通过添加以下代码为类定义属性：  
  
     [!code-vb[VbVbalrOOP#8](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#8)]  
  
8.  通过添加以下代码为类定义方法：  
  
     [!code-vb[VbVbalrOOP#9](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#9)]  
  
9. 通过添加名为 `Sub New` 的过程为新类定义参数化的构造函数：  
  
     [!code-vb[VbVbalrOOP#10](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#10)]  
  
     当创建基于此类的对象时，会自动调用 `Sub New` 构造函数。  此构造函数设置保存用户名的字段值。  
  
### 创建测试类的按钮  
  
1.  在**“解决方案资源管理器”**中右击启动窗体的名称，然后单击**“视图设计器”**，从而将启动窗体更改为设计模式。  默认情况下，“Windows 应用程序”项目的启动窗体的名称为 Form1.vb。  主窗体随即出现。  
  
2.  在主窗体中添加一个按钮，然后双击该按钮显示 `Button1_Click` 事件处理程序的代码。  添加下列代码以调用测试过程：  
  
     [!code-vb[VbVbalrOOP#12](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#12)]  
  
### 运行应用程序  
  
1.  按 F5 运行应用程序。  单击窗体上的按钮以调用测试过程。  它会显示一条消息，说明原来的 `UserName` 是“MOORE, BOBBY”，因为该过程调用了对象的 `Capitalize` 方法。  
  
2.  单击**“确定”**关闭该消息框。  `Button1 Click` 过程会更改 `UserName` 属性的值，并显示一条消息，说明 `UserName` 的新值为“Worden, Joe”。  
  
## 请参阅  
 [面向对象的编程](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)