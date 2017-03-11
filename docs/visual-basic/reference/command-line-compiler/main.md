---
title: "/main | Microsoft Docs"
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
  - "/main 编译器选项 [Visual Basic]"
  - "main 编译器选项 [Visual Basic]"
  - "-main 编译器选项 [Visual Basic]"
ms.assetid: 83fc339d-6652-415d-b205-b5133319b5b0
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /main
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定包含 `Sub Main` 过程的类或模块。  
  
## 语法  
  
```  
/main:location  
```  
  
## 参数  
 `location`  
 必选。  这是类或模块的完全限定位置，该类或模块包含程序启动时要调用的 `Sub Main` 过程。  其形式可能为 **\/main:module** 或 **\/main:namespace.module**。  
  
## 备注  
 创建可执行文件或 Windows 可执行程序时，请使用此选项。  如果省略 **\/main** 选项，编译器会在所有公共类和模块中搜索有效的共享 `Sub Main`。  
  
 有关 `Main` 过程的各种形式的论述，请参见 [Visual Basic 中的 Main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)。  
  
 如果 `location` 是一个从 <xref:System.Windows.Forms.Form> 继承的类，且该类没有 `Main` 过程，则编译器会提供一个用以启动应用程序的默认 `Main` 过程。  这样就可以在命令行编译在开发环境中创建的代码。  
  
 [!code-vb[VbVbalrCompiler#16](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/main_1.vb)]  
  
### 在 Visual Studio 集成开发环境中设置 \/main  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  
  
     有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“应用程序”**选项卡。  
  
3.  确保没有选中**“启用应用程序框架”**复选框。  
  
4.  修改**“启动对象”**框中的值。  
  
## 示例  
 下面的代码编译 `T2.vb` 和 `T3.vb`，同时指定可以在 `Test2` 类中找到 `Sub Main` 过程。  
  
```  
vbc t2.vb t3.vb /main:Test2  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [NIB: Visual Basic Version of Hello, World](http://msdn.microsoft.com/zh-cn/9d030b60-e148-4366-a462-69532f02294c)   
 [Visual Basic 中的 Main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)