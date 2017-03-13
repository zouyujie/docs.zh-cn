---
title: "/imports (Visual Basic) | Microsoft Docs"
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
  - "/imports 编译器选项 [Visual Basic]"
  - "imports 编译器选项 [Visual Basic]"
  - "-imports 编译器选项 [Visual Basic]"
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /imports (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

从指定的程序集导入命名空间。  
  
## 语法  
  
```  
/imports:namespaceList  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`namespaceList`|必选。  要导入的逗号分隔的命名空间列表。|  
  
## 备注  
 `/imports` 选项将导入在当前源文件集中定义的或来自任何被引用的程序集的任何命名空间。  
  
 使用 `/imports` 指定的命名空间中的成员可用于编译中的所有源代码文件。  使用 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 可以在单个源代码文件中使用命名空间。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/imports|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“引用”**选项卡。<br />3.  在**“添加用户导入”**按钮旁边的框中输入命名空间名称。<br />4.  单击**“添加用户导入”**按钮。|  
  
## 示例  
 当指定 `/imports:system` 时，下面的代码将会编译。  
  
 [!code-vb[VbVbalrCompiler#21](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/imports_1.vb)]  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)