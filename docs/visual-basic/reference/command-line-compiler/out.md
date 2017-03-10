---
title: "/out (Visual Basic) | Microsoft Docs"
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
  - "/out 编译器选项 [Visual Basic]"
  - "out 编译器选项 [Visual Basic]"
  - "-out 编译器选项 [Visual Basic]"
ms.assetid: 9f148c15-0909-4cb8-a2db-777f8a8b45ae
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /out (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定输出文件的名称。  
  
## 语法  
  
```  
/out:filename  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`filename`|必选。  编译器创建的输出文件的名称。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。|  
  
## 备注  
 指定要创建的文件的完整名称和扩展名。  如果不具体指定，.exe 文件将从包含 `Sub Main` 过程的源代码文件中获取它的名称，而 .dll 文件将从第一个源代码文件中获取它的名称。  
  
 如果指定不带 .exe 或 .dll 扩展名的文件名，则编译器将根据为 `/target` 编译器选项指定的值自动添加扩展名。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/out|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“应用程序”**选项卡。<br />3.  修改**“程序集名称”**框中的值。|  
  
## 示例  
 下面的代码编译 `T2.vb` 并创建输出文件 `T2.exe`。  
  
```  
vbc t2.vb /out:t3.exe  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)